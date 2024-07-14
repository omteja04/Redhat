<!--
  Author: omteja04
  Created on: 14-07-2024 15:28:34
  Description: Node - 1

  cSpell:disable

-->

**Important Configuration**

- Node 1 Password
- Hostname
- Registry Login
- Repo Links

**Node 1**

- [ ] **Hostname**

```bash

hostname ctl set-hostname serverb.lab.example.com


# To check
hostname
```

- [ ] **IP Address**

```bash
# To see the connection
nmcli connection show

# To modify
nmcli connection modify "Wired Connection 1" ipv4.addresses 172.25.250.11/24 ipv4.gateway 172.25.250.254 ipv4.dns 172.25.250.254 ipv4.method static

# Make the connection up
nmcli connection up

# To verify
ping 172.25.250.11

# ctrl + c

```

- [ ] **Repos**

```bash
vim /etc/yum.repos.d/app.repo
```

```bash
# in VIM
# click I

[123]
name=app
baseurl=http://classroom.example.com/content/rhel9.0/x86_64/dvd/AppStream
gpgcheck=0
enabled=1

[456]
name=base
baseurl=http://classroom.example.com/content/rhel9.0/x86_64/dvd/BaseOS
gpgcheck=0
enabled=1


# TO exit from vim
# click esc
:wq!
```

```bash
yum clean all

yum repolist

# TO verify


yum install vim -y

```

- [ ] **Configure webserver**

```bash
# To see the name
semanage port -l | grep http

# http_port_t

semanage port -a -t http_port_t -p tcp 82

# To check
semanage port -l | grep http

# To add the port to firewall
firewall-cmd --permanant --add-port=82/tcp

# Reload the firewall
firewall-cmd --reload

# To list the ports in firewall
firewall-cmd --list-ports
# 82/tcp

# to install httpd service
yum install httpd -y

systemctl start httpd

systemctl enable httpd

vim /etc/httpd/conf/httpd.conf
```

```bash
# in VIM
# click I

# Go to bottom line

<virtualhost 172.25.250.11:82>
servername serverb.lab.example.com
documentroot /var/www/html
</virtualhost>

# to exit vim
# click esc
:wq!

```

```bash


httpd -t
# Syntax OK


systemctl restart httpd


curl 172.25.250.11:82/file1
# Desired Output
```

- [ ] **Users and groups management**

```bash
# Create a group

groupadd admin

# Create Users
useradd -G admin harry
useradd -G admin natasha
useradd -s /sbin/nologin sarah

# password

passwd --stdin harry
# redhat
passwd --stdin natasha
# redhat
passwd --stdin sarah
# redhat

# To verify
tail /etc/passwd
tail /etc/group
tail /etc/shadow

```

- [ ] **Create a directory and assign the basic permissions**

```bash
mkdir -p /common/admin
chmod 770 /common/admin
chgrp admin /common/admin
chmod g+s /common/admin

ls -ld /common/admin
# drwxrws---

```

- [ ] **Configure the auto filesystem**

```bash

yum install autofs -y
systemctl start autofs
systemctl enable autofs

vim /etc/auto.master

# In vim
/localhome <TAB_SPACE> /etc/auto.misc
# exit vim ':wq!'

vim /etc/auto.misc

# In VIM
production5 -rw,soft,intr servera.lab.example.com/user-homes/prodution5
# exit vim ':wq!'
systemctl restart autofs

getent passwd production5 # To check whether there is an entry of prodution5

su - production5 # Switch to production5

```

```bash

# To check whether it is mounted or not...
df -hT
exit

```

- [ ] **Configure crontab**

```bash
crontab -eu harry

*/2 * * * * /bin/echo "Hello, Idiot!"


#  This is to print log message hello for every 2 minutes
*/2 * * * * logger user.debug "Hello, Idiot!"

systemctl restart crond

crontab -lu harry
```

- [ ] **NTP configuration**

```bash
systemctl start chronyd
systemctl enable chronyd

vim /etc/chrony.conf

# In VIM

server classroom.example.com iburst

# exit vim

systemctl restart chronyd
chronyc sources -v
timedatectl

# timedatectl set-ntp true
# (Use this command if ntp is not showing yes)
```

- [ ] **find the owner of the file**

```bash

mkdir /root/find.user

find / -user sarah -type f -exec cp {} /root/find.user \;

ls -a /root/find.user

```

- [ ] **grep the "home" string from /etc/passwd**

```bash
grep home /etc/passwd >> /root/mysearch.txt
```

- [ ] **Create a user account with UID 1326**

```bash
useradd -u 1326 alies
```

- [ ] **Backup the /var/tmp as /root/test.tar.gz**

```bash

# For gzip files
tar -zcvf /root/test.tar.gz /var/tmp

# For bzip files
tar -jcvf /root/test.tar.bz2 /var/tmp

```

- [ ] [**Set the Permission**](https://github.com/omteja04/Redhat/blob/main/Umask.md)

```bash
# a) All new creating files for user natasha as -r-------- as default permission.
# b) All new creating directories for user natasha as dr-x------ as default permission.

su - natasha

vim .bash_profile
# in vim
umask 277

:wq!

source .bash_profile

```

- [ ] **Password Expiry**

```bash
vim /etc/login.defs

# in VIM (Search PASS_MAX_DAYS) -> To search Type /PASS_MAX_DAYS

# Place curson at  PASS_MAX_DAYS  and click i

PASS_MAX_DAYS 20

:wq!

# To restart the system
init 6
```

- [ ] **Assign Sudo Privilege**

```bash
vim /etc/sudoers
# Go To Line 111
# :111

%admin ALL=(ALL)  NOPASSWD: ALL
```

- [ ] **Configure the application**

```bash
su - alies

vim .bash_profile

# In VIM

RHCSA="Welcome to Advantage Pro"
export RHCSA
echo $RHCSA

:wq!

source .bash_profile
```

- [ ] **Create the script file**

```bash

mkdir /root/myfiles

vim myscript
# in VIM
```

```sh
#!/bin/sh
find /usr/share -type f -size -1M -exec cp {} /root/myfiles \; #Less Than 1M Files

find /usr/share -type f -size +1M -size -2M -exec cp {} /root/myfiles \; #between 1M and 2M Files

# u+s -perm /4000
# g+s -perm /2000

# exit vim
:wq!
```

```bash
chmod +x myscript
./myscript
ls -a /root/myfiles
```

> After Completion of Node 1 type `init 6` to reboot
