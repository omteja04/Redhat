<!--
  Author: omteja04
  Created on: 07-06-2024 10:32:51
  Description: Swap
-->

<!-- cSpell:disable -->

### Create a new SWAP

```sh
free -mh # TO check the exiting swaps
```

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
1
# Enter
+512M
t
1
82
w
```

```sh
# To Update
partprobe
```

```sh
# To view the disk details
lsblk
```

```sh
# to make partition as swap
mkswap /dev/vdb1
```

```sh
# To see the block attributes
blkid
```

```sh
# To on the swap
swapon /dev/vdb1
```

```sh
# To see details
swapon
```

```sh
free -mh
```

```sh
# For permanent mounting
vim /etc/fstab
```

go to last line and add
`/dev/vdb1`&emsp;`swap`&emsp;`swap`&emsp; `defaults`&emsp;`0 0`

```sh
free -mh
```

```sh
# To check if there are any errors
mount -a
```
