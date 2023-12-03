---
title: "The Definitive Handbook: Essential Strategies for Strengthening Your Linux Server"
categories: [linux, linuxserver, hardening, privacy, security, sidsblog]
tags: [linux, linuxserver, hardening, privacy, security, sidsblog]
date: 2022-10-16T17:26:04+05:30
description: "This tutorial will help you understand how to harden the linux server for security."
author: Siddhant Mulajkar
draft: false
---



### Requirements

-   Computer, virtual private server (VPS) or dedicated server running Debian based server instance.
-   Linux or macOS computer for following the steps and hardening the server



#### Guide
--

##### Step 1. Create the SSH key pair for login (On Computer)

Using a root login password to login is good but not great from the security stand.

When asked for file in which to save key, enter **serverlog**.

When asked for passphrase, use output from **openssl rand -base64 24** (and store passphrase in password manager).

Use **serverlog.pub** public key when setting up server.

```
ubuntu@userver:~$ cd ~/.ssh
ubuntu@userver:~/.ssh$ ls
authorized_keys
ubuntu@userver:~/.ssh$ ssh-keygen -t rsa -C "serverlogin"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ubuntu/.ssh/id_rsa): serverlogin
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in serverlogin
Your public key has been saved in serverlogin.pub
The key fingerprint is:
SHA256:HT7IJjqOzX4u+bGX/TOfZuOwujuEv/dSqP56d7vGTS0 serverlogin
The key's randomart image is:
+---[RSA 3072]----+
|                 |
|                 |
|          .      |
|       . + .     |
|      . S.+  .  .|
|     . o. ... E o|
|    o..  = ....o.|
|   =o..oo = *o=+o|
|  ..==+. .B%+@*=o|
+----[SHA256]-----+
ubuntu@userver:~/.ssh$ ls
authorized_keys  serverlogin  serverlogin.pub
ubuntu@userver:~/.ssh$


ubuntu@userver:~/.ssh$
ubuntu@userver:~/.ssh$ cat serverlogin.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCfKyJnbvFXsZo2wBwIcOCyfzDPBxpzfV/r26jFZa7MLkdoXGpACUSL+wn0FFTBxE8XsduofHoDT5hsv1xIZjtrTbM0ZwCJVE8lxN8hkhiSOywEypTEUdFxafhQjD9BZSAwMCSp09t6iE7+dgB8P+InuNYstJLF/jTba9nD8U4QX3q9wZuMInB3+dMdP0Wf+3kc9cJxF/zsNxaiBUOABi4PGZg/w7ea5lxavtsWd0I59BtO2oq7XPVQBhzAz6FpSFf1UaZhFWYeE2r0FOU3hZUxHFrV8cv237Qnrs5cDYYaQsDfY9vY6C27nBVAo1GKK4jD65SDgGLET4gGUh5a2JO3Ya4XrdP/j4dDwWsyplz80Jsc9rm0bfaiaaqbkf/rWZ6a3moDW5SaP0pvVvxcF5ZRuRTQUj7q5/jwhm4h5/D9gaTtk7hJGfjWSTeNDvq6dG9JvA8er8DFuXm/nziGVaN9t/8mMbrxei37LZ+QDvkHzQVKemmeYE/6PwvSzKy4JGs= serverlogin
ubuntu@userver:~/.ssh$

```

Paste the cat command output in the ssh key section 
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCfKyJnbvFXsZo2wBwIcOCyfzDPBxpzfV/r26jFZa7MLkdoXGpACUSL+wn0FFTBxE8XsduofHoDT5hsv1xIZjtrTbM0ZwCJVE8lxN8hkhiSOywEypTEUdFxafhQjD9BZSAwMCSp09t6iE7+dgB8P+InuNYstJLF/jTba9nD8U4QX3q9wZuMInB3+dMdP0Wf+3kc9cJxF/zsNxaiBUOABi4PGZg/w7ea5lxavtsWd0I59BtO2oq7XPVQBhzAz6FpSFf1UaZhFWYeE2r0FOU3hZUxHFrV8cv237Qnrs5cDYYaQsDfY9vY6C27nBVAo1GKK4jD65SDgGLET4gGUh5a2JO3Ya4XrdP/j4dDwWsyplz80Jsc9rm0bfaiaaqbkf/rWZ6a3moDW5SaP0pvVvxcF5ZRuRTQUj7q5/jwhm4h5/D9gaTtk7hJGfjWSTeNDvq6dG9JvA8er8DFuXm/nziGVaN9t/8mMbrxei37LZ+QDvkHzQVKemmeYE/6PwvSzKy4JGs= serverlogin
```

--

#### Step 2: log in to the server as root

Caution: when asked for passphrase, enter passphrase used while creating the ssh key

```
ssh -i ~/.ssh/server root@123.567.344.115
```

save the fingerprint of the server for further use by typing **yes**, and change the **ip address** according to the server address


###### If you wanted to use this for internal server rather than hosting a server outside then we can simply send the copy of the ssh from the local machine to server.

```
ssh-copy-id -i /home/sid/.ssh/rasp.pub user@123.567.344.115
```

change the user to user created or using the server in the above command. 


Next sub-step is important for hardening the server, either hosted internally or outside

###### Change the sshd file configuration to restrict the password login to the server and also to restrict the empty password attempts

```
sudo nano /etc/ssh/sshd_config
```

```
# To disable tunneled clear text passwords, change to no here!
PasswordAuthentication no
PermitEmptyPasswords no
```

```
UsePAM no
```

we can also accept the traffic from the specific **ip's** using the **ListenAddress** section.

--

#### Step 3: disable root Bash history (Optional)

```
echo "HISTFILESIZE=0" >> ~/.bashrc
history -c; history -w
source ~/.bashrc
```

disabling the bash history to not have the previous command in the memory once the session is closed

--

#### Step 4: set root password

When asked for password, use output from **openssl rand -base64 24**(and store password in password manager).

```
ubuntu@userver:~/.ssh$ openssl rand -base64 24
WmwBSIQD7fZDNcm5be2RQ3lJLb8eYFcr
```

```
root@userver:/home/ubuntu# passwd
New password: 
Retype new password: 
passwd: password updated successfully
root@userver:/home/ubuntu#
```

--

#### Step 5: create server-admin user

When asked for password, use output from **openssl rand -base64 24** (and store password in password manager).

All other fields are optional, press enter to skip them and then press Y.

```
root@userver:/home/ubuntu# adduser saurabh
Adding user `saurabh' ...
Adding new group `saurabh' (1001) ...
Adding new user `saurabh' (1001) with group `saurabh' ...
Creating home directory `/home/saurabh' ...
Copying files from `/etc/skel' ...
New password: 
Retype new password: 
passwd: password updated successfully
Changing the user information for saurabh
Enter the new value, or press ENTER for the default
	Full Name []: 
	Room Number []: 
	Work Phone []: 
	Home Phone []: 
	Other []: 
Is the information correct? [Y/n] Y
root@userver:/home/ubuntu#
```

--

#### Step 6: copy root [authorized_keys] file to server-admin home directory

```
root@userver:/home/ubuntu# mkdir /home/saurabh/.ssh
root@userver:/home/ubuntu# cp /root/.ssh/authorized_keys /home/saurabh/.ssh/authorized_keys
root@userver:/home/ubuntu# chown -R saurabh:saurabh /home/saurabh/.ssh
root@userver:/home/ubuntu#
```

--

#### Step 7: log out

```
exit
```

--

#### Step 8: log in as server-admin

Replace **123.567.344.115** with IP of server.

Heads-up: when asked for passphrase, enter passphrase from step 1

```
ssh -i ~/.ssh/server saurabh@123.567.344.115
```

--

#### Step 9: disable server-admin Bash history

```
sed -i -E 's/^HISTSIZE=/#HISTSIZE=/' ~/.bashrc
sed -i -E 's/^HISTFILESIZE=/#HISTFILESIZE=/' ~/.bashrc
echo "HISTFILESIZE=0" >> ~/.bashrc
history -c; history -w
source ~/.bashrc
```

--

#### Step 10: switch to root

When asked, enter root password.

```
su -
```

--

#### Step 11: disable root login and password authentication

```
sed -i -E 's/^(#)?PermitRootLogin (prohibit-password|yes)/PermitRootLogin no/' /etc/ssh/sshd_config
sed -i -E 's/^(#)?PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config
systemctl restart ssh
```

--

#### Step 12: configure sysctl (if network is IPv4-only) [optional step]

**Only** run the following if network is **IPv4**-only.

```
cp /etc/sysctl.conf /etc/sysctl.conf.backup
cat << "EOF" >> /etc/sysctl.conf
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
EOF
sysctl -p
```

--

#### Step 13: enable nftables and configure firewall rules

##### Update APT index and install nftables

```shell-session
$ apt update

$ apt install -y nftables
```

##### Enable nftables

```
systemctl enable nftables
systemctl start nftables
```

##### Configure firewall rules

```
nft flush ruleset
nft add table ip firewall
nft add chain ip firewall input { type filter hook input priority 0 \; policy drop \; }
nft add rule ip firewall input iif lo accept
nft add rule ip firewall input iif != lo ip daddr 127.0.0.0/8 drop
nft add rule ip firewall input tcp dport ssh accept
nft add rule ip firewall input ct state established,related accept
nft add chain ip firewall forward { type filter hook forward priority 0 \; policy drop \; }
nft add chain ip firewall output { type filter hook output priority 0 \; policy drop \; }
nft add rule ip firewall output oif lo accept
nft add rule ip firewall output tcp dport { http, https } accept
nft add rule ip firewall output udp dport { domain, ntp } accept
nft add rule ip firewall output ct state established,related accept
```

--

#### If network is IPv4-only, run:

```
nft add table ip6 firewall
nft add chain ip6 firewall input { type filter hook input priority 0 \; policy drop \; }
nft add chain ip6 firewall forward { type filter hook forward priority 0 \; policy drop \; }
nft add chain ip6 firewall output { type filter hook output priority 0 \; policy drop \; }
```

--

#### If network is dual stack (IPv4 + IPv6) run:
```
nft add table ip6 firewall
nft add chain ip6 firewall input { type filter hook input priority 0\; policy drop\; }
nft add rule ip6 firewall input iif lo accept
nft add rule ip6 firewall input iif != lo ip6 daddr ::1 drop
nft add rule ip6 firewall input meta l4proto ipv6-icmp icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem } accept
nft add rule ip6 firewall input meta l4proto ipv6-icmp icmpv6 type { nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert, nd-redirect } ip6 hoplimit 255 accept
nft add rule ip6 firewall input tcp dport ssh accept
nft add rule ip6 firewall input ct state established,related accept
nft add chain ip6 firewall forward { type filter hook forward priority 0\; policy drop\; }
nft add chain ip6 firewall output { type filter hook output priority 0\; policy drop\; }
nft add rule ip6 firewall output oif lo accept
nft add rule ip6 firewall output meta l4proto ipv6-icmp icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem } accept
nft add rule ip6 firewall output meta l4proto ipv6-icmp icmpv6 type { nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert } ip6 hoplimit 255 accept
nft add rule ip6 firewall output tcp dport { http, https } accept
nft add rule ip6 firewall output udp dport { domain, ntp } accept
nft add rule ip6 firewall output ct state related,established accept
```

--

#### Step 14: log out and log in to confirm firewall is not blocking SSH

##### Log out

```shell-session
$ exit

$ exit
```

---

#### Log in
Caution: when asked for passphrase, enter passphrase used while creating the ssh key from **step 1**

```
ssh -i ~/.ssh/server saurabh@123.567.344.115
```

#### Switch to root

When asked, enter root password.

```
su -
```

---

#### Step 15: make firewall rules persistent

```
cat << "EOF" > /etc/nftables.conf
#!/usr/sbin/nft -f

flush ruleset

EOF
```

```
nft list ruleset >> /etc/nftables.conf
```

--

#### Step 16: update APT index and upgrade packages

```shell-session
$ apt update

$ apt upgrade -y
```

--

#### Step 17: set timezone (the following is for Kolkatta time)

See [https://en.wikipedia.org/wiki/List_of_tz_database_time_zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)

```
timedatectl set-timezone Asia/Kolkata
```

---

#### Step 18: log out and log in to system-admin to auto-update the security packages
```
sudo apt install unattended-upgrades
sudo apt install update-notifier-common
```

Set your automatic upgrade preferences in the

```
/etc/apt/apt.conf.d/50unattended-upgrades
```

file. These are the settings I use.

```
//Unattended-Upgrade::InstallOnShutdown "false"; 

// Send email to this address for problems or packages upgrades // If empty or unset then no email is sent, make sure that you 
// have a working mail setup on your system. A package that provides 
// 'mailx' must be installed. E.g. "user@example.com" Unattended-Upgrade::Mail "you@example.com"; 

// Set this value to one of: 
// "always", "only-on-error" or "on-change" 
// If this is not set, then any legacy MailOnlyOnError (boolean) value 
// is used to chose between "only-on-error" and "on-change" Unattended-Upgrade::MailReport "only-on-error"; 

// Remove unused automatically installed kernel-related packages 
// (kernel images, kernel headers and kernel version locked tools). Unattended-Upgrade::Remove-Unused-Kernel-Packages "true"; 

// Do automatic removal of newly unused dependencies after the upgrade Unattended-Upgrade::Remove-New-Unused-Dependencies "true"; 

// Do automatic removal of unused packages after the upgrade 
// (equivalent to apt-get autoremove) 
Unattended-Upgrade::Remove-Unused-Dependencies "true"; 

// Automatically reboot *WITHOUT CONFIRMATION* if 
// the file /var/run/reboot-required is found after the upgrade 
Unattended-Upgrade::Automatic-Reboot "true"; 

// Automatically reboot even if there are users currently logged in 
// when Unattended-Upgrade::Automatic-Reboot is set to true 
//Unattended-Upgrade::Automatic-Reboot-WithUsers "true"; 

// If automatic reboot is enabled and needed, reboot at the specific 
// time instead of immediately 
// Default: "now" 
Unattended-Upgrade::Automatic-Reboot-Time "03:00"; 

// Use apt bandwidth limit feature, this example limits the download 
// speed to 70kb/sec 
//Acquire::http::Dl-Limit "70"; 

// Enable logging to syslog. Default is False 
// Unattended-Upgrade::SyslogEnable "false"; 

// Specify syslog facility. Default is daemon 
// Unattended-Upgrade::SyslogFacility "daemon"; 

// Download and install upgrades only on AC power 
// (i.e. skip or gracefully stop updates on battery) 
// Unattended-Upgrade::OnlyOnACPower "true"; 

// Download and install upgrades only on non-metered connection 
// (i.e. skip or gracefully stop updates on a metered connection) 
// Unattended-Upgrade::Skip-Updates-On-Metered-Connections "true"; 

// Verbose logging 
// Unattended-Upgrade::Verbose "false"; 

// Print debugging information both in unattended-upgrades and 
// in unattended-upgrade-shutdown 
// Unattended-Upgrade::Debug "false"; 

// Allow package downgrade if Pin-Priority exceeds 1000 
// Unattended-Upgrade::Allow-downgrade "false";
```

In order to enable automatic upgrades, execute the following command where the **-plow** flag mean priority low.

```
dpkg-reconfigure -plow unattended-upgrades
```

In the resulting screen with a pink background, you will be asked “Automatically download and install stable updates?” 

Select the **Yes** option to continue.

---

#### Test it Out with a Dry Run

You can optionally do a dry run to see what will happen during an unattended upgrade with the following command.

```
unattended-upgrades --dry-run --debug
```

--

#### Look at the Daily Timer

If you look at the **/lib/systemd/system/apt-daily.timer** file, you will see the interval that the **apt update** command is executed. In this case it is twice a day with a random delay after 6 AM and 6 PM.

```
[Unit]

Description=Daily apt download activities

[Timer]

OnCalendar=*-*-* 6,18:00

RandomizedDelaySec=12h

Persistent=true

[Install]

WantedBy=timers.target
```


The corresponding service file at **/lib/systemd/system/apt-daily.service** contains the actual command (**ExecStart**) that will be executed based on that timer interval.

```
[Unit]

Description=Daily apt download activities

Documentation=man:apt(8)

ConditionACPower=true

After=network.target network-online.target systemd-networkd.service NetworkManager.service connman.service

[Service]

Type=oneshot

ExecStartPre=-/usr/lib/apt/apt-helper wait-online

ExecStart=/usr/lib/apt/apt.systemd.daily update
```

Timer and service files also exist for the **apt upgrade** command too. The timer file is at **/lib/systemd/system/apt-daily-upgrade.timer** .

```
[Unit]

Description=Daily apt upgrade and clean activities

After=apt-daily.timer

[Timer]

OnCalendar=*-*-* 6:00

RandomizedDelaySec=60m

Persistent=true

[Install]

WantedBy=timers.target
```

The service file is at **/lib/systemd/system/apt-daily-upgrade.service**.

```
[Unit]

Description=Daily apt upgrade and clean activities

Documentation=man:apt(8)

ConditionACPower=true

After=apt-daily.service network.target network-online.target systemd-networkd.service NetworkManager.service connman.service

[Service]

Type=oneshot

ExecStartPre=-/usr/lib/apt/apt-helper wait-online

ExecStart=/usr/lib/apt/apt.systemd.daily install

KillMode=process

TimeoutStopSec=900
```


---

### Read More Blogs related to:

***[db-concepts]({{< relref "/tags/database/">}}) / [linuxsubsystem(wsl)]({{< relref "/tags/wsl2">}}) / [flutter-installation]({{< relref "/tags/flutter">}}) / [networking]({{< relref "/tags/networking">}}) / [raspberry-pi]({{< relref "/tags/raspberry">}})***

--