[Source: ](https://www.server-world.info/en/note?os=CentOS_7&p=selinux&f=7)
[Source: ](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/7/html/selinux_users_and_administrators_guide)

###Places to search for AVC messages:
Messages via Rsyslog are generated with "kern" facility. CentOS default Rsyslog setting is written as "*.info;xxx /var/log/messages", so AVC Denial Log is recorded to /var/log/messages.

```
	grep "avc: .denied" /var/log/messages
```

Messages via Auditd are generated to /var/log/audit/audit.log.

```
	grep "avc: .denied" /var/log/audit/audit.log
```

For Messages via Auditd, it's possible to search them with ausearch command.

```
	ausearch -m AVC
```

For Messages via Auditd, it's possible to show summary reports with aureport command.

```
	aureport --avc --summary
```

STAT command to show SE_Linux status:

```
	stat -c "%a %n %C" *
```

To view what actions SELinux denies, enter the following command as root:

```
	ausearch -m AVC,USER_AVC,SELINUX_ERR,USER_SELINUX_ERR -ts today
```

Alternatively, with the setroubleshoot-server package installed, enter:

```
	grep "SELinux is preventing" /var/log/messages
```

If SELinux is active and the Audit daemon (auditd) is not running on your system, then search for certain SELinux messages in the output of the dmesg command:

```
	dmesg | grep -i -e type=1300 -e type=1400
```

View the available types that can be used with SELinux:
https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/7/html/selinux_users_and_administrators_guide/sect-managing_confined_services-the_apache_http_server-types
```
	First install: dnf -y install setools-console
	Then run: seinfo -t
```

Allow apache to receive files to an uploads folder/directory:

```
sudo chown apache:apache -R /uploads
sudo chcon -Rv --type=httpd_sys_rw_content_t uploads/
```

```
With /srv/ as the base directory you must adjust the SELinux labels.
htdocs is where the index.php/html file goes.

[…]# /usr/sbin/semanage fcontext -a -t httpd_sys_content_t  -s system_u  "/srv/SITENAME/htdocs(/.*)?"
[…]# /sbin/restorecon -R -vF /srv/SITENAME/htdocs
Relabeled /srv/SITENAME/htdocs from unconfined_u:object_r:var_t:s0 to system_u:object_r:httpd_sys_content_t:s0
Source: https://docs.fedoraproject.org/en-US/fedora-server/services/httpd-basic-setup/#_installation
```

Change the SE Linux properties of a file: (Source: https://www.thegeekstuff.com/2017/07/chcon-command-examples/)
Example: this Test2a.php file was displaying "Access Denied" error on my website.

Check and change the SELinux properties:
```
	Check the current SELinux properties with: ls -Z
		The properties were: unconfined_u:object_r:user_home_t:s0 Test2a.php

	I changed the SELinux properties using:
		sudo chcon unconfined_u:object_r:httpd_user_content_t:s0 Test2a.php
```

If you want to copy the SE_Linux settings from one directory that is working to another:
```
	# semanage fcontext --add --equal /var/www/html /opt/www/html
	# restorecon -rv /opt/www/html
```

If you are using a non-standard directory for web files, like /opt/www/html, then you may not be able to use restorecon to automatically fix the SELinux context. You will have to set the context using chcon and save the change using semanage to make the change permanent:
```
	# chcon -R system_u:object_r:httpd_sys_content_t:s0 /opt/www
	# semanage fcontext -a -t httpd_sys_content_t "/opt/www(/.*)?"
	# restorecon -rv /opt/www
```

If you get "SQLSTATE[HY000] [2002] Permission denied" message. You need to enable the httpd service to network connect.
You must check in the SELinux if port 80 is managed in. You can check it by typing # semanage port -l | grep http_port_t for a list and check:
```
		semanage port -l | grep http_port_t
```

If you need to add the required port, just type:
```
		# semanage port -a -t http_port_t -p tcp 80
```

		Stop the httpd service set the SE_Linux permission and start the http service.

		Down the httpd service #
```
		service httpd stop
```
		Enable the httpd service to connect to the network:
```
		# setsebool -P httpd_can_network_connect 1
		# setsebool -P httpd_can_network_connect_db 1
```
		Check if the service is enabled:
```
		getsebool httpd_can_network_connect
		getsebool httpd_can_network_connect_db
```
		Up the httpd service #
```
		service httpd start
```

```
Webmin vs Usermin (minisrv.pid)
journalctl -t setroubleshoot --since=09:54 > x.txt <-- showed a miniserv.pid denial issue.
You can specify a date and time for journalctl: journalctl -t setroubleshoot --since="2025-12-04 10:55:00"
https://forum.virtualmin.com/t/selinux-issue-with-miniserv-pid-on-redhat-8/116597
chcon --recursive --reference=/var/webmin /var/usermin
```
Testing various software updates to my RedHat 8 servers and came across a new issue.

I realize its my own headache, but my agency really likes SELinux and we run it in enforcing mode as much as we can :slight_smile:

My template system I use to clone VirtualMin servers has for a long time had /var/usermin set to the SELinux context of var_t while the corresponding directory /var/webmin has the context of var_log_t (as well as all the files in each directory). This never caused me any issues (not sure I even noticed) until today when I applied a bunch of RedHat updates along with updating webmin and usermin and virtualmin; now there is an issue with the miniserv.pid file used by usermin.

Note again this was not an issue last week or last month – and is not an issue with the similar miniserv.pid file used by webmin. In researching this, I came across an actual webmin rule distributed by RedHat/Centos in the SELinux policies targeting /var/webmin !! I was very surprised and excited to see that as I did not know it was there.

Sadly there is not a similar context rule for /var/usermin :frowning:

so … for now I just relabeled /var/usermin to match /var/webmin with

chcon --type=var_log_t --recursive /var/usermin

for completeness I should post another way to adjust it (assuming /var/webmin is correct):

chcon --recursive --reference=/var/webmin /var/usermin

of course to make things ‘stick’, I really should create a local policy (and apply it), to mimic the policy already in place for /var/webmin with

semanage fcontext --add --type=var_log_t “/var/usermin(/.*)?”
restorecon -R /var/usermin

OR … as today’s issue is about just the PID file, I wonder if a redesign is in order?? That is, have the PID file stored in /var/run, or a subdirectory such as /var/run/webmin and /var/run/usermin ???

But that could be much more work; since /var/webmin is set to var_log_t already, /var/usermin I believe should match it :slight_smile:

As this took me some time to diagnose, I wanted to share in case it can help others !!

Verne
