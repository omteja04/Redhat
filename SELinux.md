<!--
  Author: omteja04
  Created on: 06-06-2024 21:48:05
  Description: SELinux
-->

<!-- cSpell:disable -->

### Modes

```sh
getenforce # Enforcing

setenforce 0

getenforce # Permissive

setenforce 1

getenforce # Enforcing

# To Disable We have to it manually

vim /etc/sysconfig/selinux
# change to disabled
# Restart System
```

### SELinux Booleans

```sh
getsebool -a | grep httpd

setsebool -P servicename on/off # Acc. to que

#Example

getsebool -a | grep httpd

setsebool -P httpd_enable_homedirs on

getsebool -a | grep httpd #To check
```

### SELinux Port

The system is not able to connet to httpd service ar port 82. It should be accessible ar port 82 and should start at boot time.

```sh
semanage port -l | grep http

semanage port -a -t http_port_t -p tcp 82

firewall-cmd --permanent --add-port=82/tcp

firewall-cmd --reload

firewall-cmd --list-ports

yum install httpd -y

systemctl start httpd.service
systemctl enable httpd.service
vim /etc/httpd/conf/httpd.conf


<virtualhost 172.25.250.11:82>
servername serverb.lab.example.com
DocumentRoot /var/www/html
</virtualhost>

httpd -t
systemctl restart httpd.service
curl 172.25.255.11:82/file1
```

### SELinux Context

```sh

mkdir /test
touch /test/index.html
vim /test/index.html # Add Some content
ls -lZ /test
ls -lZ /var/www/html
semanage fcontext -a -t httpd_sys_context_t "/test(.*)?"
restorecon -Rv /test
ls -lZ /test
ls -ldZ /test

vim /etc/httpd/conf/httpd.conf

# DocumentRoot change to "/test"
# <Directory "/test">

systemctl restart httpd.service

curl localhost/index.html
```
