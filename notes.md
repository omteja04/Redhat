<!--
  Author: omteja04
  Created on: 06-06-2024 09:47:10
  Description: notes
-->

<!-- cSpell:disable -->

Normal Terminal
&darr;

```bash
rht-vmctl status all
rht-vmctl reset all
rht-vmctl start all
# Activate all VMs
#{Not For Exam}
```

Go to Workstation &rarr; Login (password: student)

Open serverB &rarr; root logi (password: redhat)

### Check hostname or set hostname (serverb.lab.example.com)

```bash
hostnamectl set-hostname serverb.lab.example.com
```

### Check IP address

```bash
ip addr
```

> If the question is to modify IP address then modify it

to view connection name

```bash
nmcli con show
```

### modify IP

```bash
nmcli con mod "Connection-Name" ipv4.addresses 172.25.250.11/24 ipv4.gateway  172.25.250.254 ipv4.dns  172.25.250.254 ipv4.method static
```

connection up

```bash
nmcli con up "Connection-Name"
```

to check

```bash
ping ipAddressOfServerB
# ctrl + C
```

Go to Workstation and establish connection with serverb

```bash
ssh root@IPaddressOfServerB
```

### Repository configuration

```bash
 vi /etc/yum.repos.d/app.repo
```

```bash
[repo-id]
name=repoName
baseurl=url
gpgcheck=0
enabled=1

[repo-id]
name=repoName
baseurl=url
gpgcheck=0
enabled=1
```

```bash
yum clean all
yum repolist
```

To check

```bash
yum install vim -y
```

### Configure SELinux

```bash

semanage port -l | grep http
semanage port -a -t http_port_t -p tcp 82
semanage port -l | grep http # To Verify

firewall-cmd --permanent --add-port=82/tcp
firewall-cmd --reload
firewall-cmd --list-ports # To Check port

yum install httpd -y

systemctl start httpd.service
systemctl enable httpd.service

vim /etc/httpd/conf/httpd.conf


<virtualhost 172.25.250.11:82>
servername serverb.lab.example.com
documentroot /var/www/html
</virtualhost>

httpd -t
systemctl restart httpd.service

curl 172.25.250.11:82/file1
```

### grep

```bash
grep home /etc/passwd
grep home /etc/passwd > /root/searh.txt
cat /root/searh.txt
```

### UID and Password Setting

```bash

useradd -u 1101 levi
passwd --stdin levi
#password levi1234
```

### archive

```bash
tar -zcvf /root/test.tar.gz var/tmp # gzip compression

tar -jcvf /root/test.tar.bz2 var/tmp # bzip2 compression
```


