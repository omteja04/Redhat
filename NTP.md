<!--
  Author: omteja04
  Created on: 08-06-2024 22:28:32
  Description: NTP
-->
<!-- cSpell:disable
 -->

```sh
yum install chrony

vim /etc/chrony.conf

# put '#' for existing iburst argument line (or)
# put '#' for existing server or pool line

server classroom.example.com iburst

systemctl restart chronyd

chronyc sources -v

timedatectl #to check
```

if system clock not syncronized & NTP service inactive
&emsp;&emsp;&emsp;&emsp;&darr;

```sh
timedatectl set-ntp true
```
