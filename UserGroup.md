<!--
  Author: omteja04
  Created on: 06-06-2024 22:32:37
  Description: UserGroup
-->

<!-- cSpell:disable -->

```sh
groupadd newgroup # To create a new group
tail /etc/group # To check
useradd harsh -G newgroup # To add user and to make newgroup as secondary group
tail /etc/group # To check
useradd nitin -s /sbin/nologin
tail /etc/passwd # To check

passwd --stdin harsh
redhat

```

```sh
mkdir -p /common/admin

ls -ld /common/admin

chown nitin /common/admin # Change ownership
chgrp newgroup /common/admin # Change group ownership
```

```sh
cp /etc/fstab /var/fstab
ls -ld /var/fstab

useradd natasha

# Since the permission are changed for one particular user we use ACL

setfacl -m u:natasha:rw- /var/fstab
getfacl /var/fstab


groupadd mac

setfacl -m g:mac:--- /var/fstab
getfacl /var/fstab

```

```sh
mkdir /linux

ls -ld /linux

chgrp mac /linux
# or
chown :mac /linux

ls -ld /linux

touch /linux/file
mkdir /linux/dir

ls -ld /linux

# For changing the ownership of existing files
chgrp -R mac /linux
# or
chown -R :mac /linux


# for changing ownership of future files
chmod g+s /linux
ls -l /linux


```
