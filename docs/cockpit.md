<pre>
<!--  <span style="color: #3366ff;"> -->

<p>To install Cockpit on Fedora, first update your system with <br /><span style="color: #3366ff;">sudo dnf -y update</span>, then install the Cockpit package using <br /><span style="color: #3366ff;">sudo dnf -y install cockpit</span>. Next, enable and start the Cockpit service with<br /> <span style="color: #3366ff;">sudo systemctl enable --now cockpit.socket</span>. Finally, allow Cockpit through <br />the firewall with <br /><span style="color: #3366ff;">sudo firewall-cmd --add-service=cockpit --permanent</span> and <br /><span style="color: #3366ff;">sudo firewall-cmd --reload</span>, then access it in your browser at <br /><span style="color: #3366ff;">https://your-server-ip:9090</span>.</p>

</pre>