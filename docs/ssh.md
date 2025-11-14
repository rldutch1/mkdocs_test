#SSH
Enable service to run at boot:
  <span style="color: #3366ff;">systemctl enable sshd.service</span><br />

Start the SSH service:
  <span style="color: #3366ff;">systemctl start sshd.service</span><br />

Offending ECDSA key in /home/someuser/.ssh/known_hosts:4<br />
  Remove with:<br />
  <span style="color: #3366ff;">ssh-keygen -f "/home/someuser/.ssh/known_hosts" -R "theservername.com"</span><br />

Copy SSH public key to remote computer:
  <br />
  <span style="color: #3366ff;">ssh-copy-id -i ~/.ssh/id_rsa.pub user@hostname</span>
  <br />
  <span style="color: #3366ff;">cat .ssh/id_rsa.pub | ssh username@servername.com "cat > .ssh/authorized_keys"

## SSH: Broadcast message: The system will suspend now! client_loop: send disconnect: Broken pipe
### You can display the current sleep/suspend settings with a command like this one:

  <span style="color: #3366ff;">sudo -u gdm dbus-run-session gsettings list-recursively org.gnome.settings-daemon.plugins.power | grep sleep</span><br />

### The problem of getting kicked out of the remote computer when the computer goes into hybernate mode was solved with the following:<br />
  <span style="color: #3366ff;">systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target</span><br />
[Source:](https://pagure.io/fedora-workstation/issue/360)<br />

##SSH Port Forwarding
### Local port forwarding:
To access a web server running on port 80 on a remote server (accessible from ssh_server) from your local machine on port 8080.
Example: The url https://localhost:8080 on your local computer will be forwarded to port 80 on the remote server.
  <br />
  <span style="color: #3366ff;">ssh -L 8080:localhost:80 user@ssh_server</span>

### Remote port forwarding:
Using -R forwards a port on the remote server to a port on your local machine, or to a port on another machine accessible from your local machine.
Example: The url https://destination_host:3333 will get forwarded to 1234 on my computer or some other computer accessible from my computer.
  <br />
  <span style="color: #3366ff;">ssh -R remote_port:destination_host:destination_port user@ssh_server</span>
  <br />
  <span style="color: #3366ff;">ssh -R 3333:destination_host:1234 user@ssh_server</span>

## Run a command on a remote computer using SSH:
  <span style="color: #3366ff;">ssh username@servername.com "ls -al"</span>

## Compress and send a file from your local computer to a remote computer using SSH:
  <span style="color: #3366ff;">tar zcvf - TheLocalFile.txt | ssh username@servername.com "cat > SomeRemoteFilename.txt"</span>

## Offending ECDSA key in /home/rob/.ssh/known_hosts:XXX
Remove with
  <br />
	<span style="color: #3366ff;">ssh-keygen -f "/home/username/.ssh/known_hosts" -R "TheHostName.com"</span>
  <br />
Example:
  <br />
	<span style="color: #3366ff;">ssh-keygen -f "/home/username/.ssh/known_hosts" -R "192.168.1.1"</span>
  <br />