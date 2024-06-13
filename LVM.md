<!--
  Author: omteja04
  Created on: 07-06-2024 10:54:53
  Description: LVM
-->

<!-- cSpell:disable
 -->

```sh
lsblk # TO know the disk and their size
```

```sh
# To create partition
fdisk /dev/vdb
```

```sh
n
p
2
# Enter
+2G
t
2
8e
w
```

```sh
# To ckeck details
lsblk
```

```sh
# to create physical volume
pvcreate /dev/vdb2
```

```sh
# to change extent size from 4 to 8 we use -s
# to create volume group
vgcreate -s 8 datastore /dev/vdb2
```

```sh
# to display volume group
vgdisplay datastore
```

```sh
# -l if extents are  given
# -L if size is given
lvcreate -l 50 -n database datastore
```

```sh
# to display lv
lvdisplay /dev/datastore/database
```

```sh
# To change the file system to ext3
mkfs.ext3 /dev/datastore/database
```

```sh
# to see details
blkid
```

```sh
# to create directory
mkdir /mnt/database
```

```sh
# For permanent mounting
vim /etc/fstab
```

go to last line and add
`/dev/datastore/database`&emsp;`/mnt/databse`&emsp;`ext3`&emsp;`defaults`&emsp;`0 0`

```sh
mount -a
```

```sh
lsblk
```

### Change size of lv

```sh
#  -l for extents
#  -L for size

lvextend -l +50 /dev/datastore/database
```

```sh
lsblk
```

```sh
# To view real time disk information
df -hT
```

```sh
# Other than xfs
resize2fs /dev/datastore/database
# for xfs
xfs_growfs /dev/datastore/database
```

```sh
# To view real time disk information
df -hT
```
