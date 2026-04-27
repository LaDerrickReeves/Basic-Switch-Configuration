<h1>Lab: Router Configuration, SSH Access, and Network Verification</h1>

<h2>Description</h2>
<p>
In this lab, I configured a Cisco router with both IPv4 and IPv6 addressing, secured remote management using SSH, and verified full connectivity between multiple devices. I also used Cisco IOS troubleshooting commands to inspect routing tables, startup configurations, interface status, and system hardware details.
</p>

<h2>Technologies & Tools</h2>
<ul>
  <li>Cisco IOS CLI</li>
  <li>IPv4 / IPv6 Networking</li>
  <li>SSH Remote Access</li>
  <li>Tera Term</li>
  <li>Windows Command Prompt</li>
  <li>Router & Switch Hardware / NetLab</li>
</ul>

<h2>Key Skills Demonstrated</h2>
<ul>
  <li>Router hostname and security configuration</li>
  <li>SSH remote management setup</li>
  <li>IPv4 and IPv6 interface addressing</li>
  <li>Password encryption and login security</li>
  <li>Routing table verification</li>
  <li>Interface troubleshooting</li>
  <li>Ping testing and connectivity validation</li>
  <li>Startup and running configuration management</li>
</ul>

<h2>Lab Walkthrough</h2>

<p align="center">
<b>1. Basic Router Security Configuration</b><br/>
I configured the router hostname, disabled DNS lookup, encrypted passwords, created local user accounts, and set secure password requirements.
</p>

<pre>
enable
configure terminal
hostname R1
ip domain-name ccna-lab.com
no ip domain-lookup
service password-encryption
security passwords min-length 12
username SSHadmin secret 55Hadm!n2020
enable secret $cisco!PRIV*
banner motd Unauthorized access prohibited
</pre>

<p align="center">
<b>2. Configuring Console and VTY Access</b><br/>
I secured console and remote login access using passwords, inactivity timers, and local authentication.
</p>

<pre>
line console 0
password $cisco!!CON*
login
exec-timeout 4 0

line vty 0 4
password $cisco!!VTY*
login local
transport input ssh
exec-timeout 4 0
</pre>

<p align="center">
<b>3. Enabling SSH for Secure Remote Access</b><br/>
I generated RSA encryption keys and configured the router to allow secure SSH logins instead of insecure Telnet.
</p>

<pre>
crypto key generate rsa
1024
ip ssh version 2
login block-for 120 attempts 3 within 60
</pre>

<p align="center">
<b>4. IPv4 and IPv6 Interface Configuration</b><br/>
I configured multiple router interfaces with dual-stack networking (IPv4 + IPv6), descriptions, and enabled each port.
</p>

<pre>
ipv6 unicast-routing

interface g0/0/0
description LAN to PC-B
ip address 192.168.0.1 255.255.255.0
ipv6 address 2001:db8:acad::1/64
ipv6 address fe80::1 link-local
no shutdown

interface g0/0/1
description LAN to PC-A
ip address 192.168.1.1 255.255.255.0
ipv6 address 2001:db8:acad:1::1/64
ipv6 address fe80::1 link-local
no shutdown

interface loopback0
description Management Loopback
ip address 10.0.0.1 255.255.255.0
ipv6 address 2001:db8:acad:2::1/64
</pre>

<p align="center">
<b>5. Saving Configuration</b><br/>
After completing the setup, I saved the running configuration so settings would remain after a reboot.
</p>

<pre>
copy running-config startup-config
</pre>

<p align="center">
<b>6. Connectivity Testing</b><br/>
I verified communication between PCs using both IPv4 and IPv6 with ping tests.
</p>

<pre>
ping 192.168.0.10
ping 2001:db8:acad::10
</pre>

<p align="center">
<b>7. Remote SSH Management</b><br/>
I remotely accessed the router using SSH through both IPv4 and IPv6 management addresses.
</p>

<pre>
ssh -l SSHadmin 10.0.0.1
ssh -l SSHadmin 2001:db8:acad:2::1
</pre>

<p align="center">
<b>8. System Information & Troubleshooting Commands</b><br/>
I used Cisco IOS show commands to inspect router hardware, software version, routes, interface status, and saved configs.
</p>

<pre>
show version
show startup-config
show ip route
show ip interface brief
show ipv6 interface brief
show startup-config | section vty
show version | include register
</pre>

<h2>Security Knowledge Applied</h2>
<ul>
  <li>Used SSH instead of Telnet because Telnet sends usernames/passwords in plaintext</li>
  <li>Configured encrypted local credentials</li>
  <li>Enabled login lockout after failed attempts</li>
  <li>Protected privileged EXEC mode with secret password</li>
</ul>

<h2>Summary</h2>
<p>
This lab strengthened my hands-on networking skills by combining router hardening, remote administration, IPv4/IPv6 deployment, and troubleshooting. It demonstrates my ability to configure enterprise network devices, secure access methods, verify connectivity, and analyze system output using Cisco IOS commands.
</p>
