<!--
  Author: omteja04
  Created on: 07-06-2024 09:58:49
  Description: PasswordBreak
-->
<!-- cSpell:disable -->

### Break Root Password

<hr>

**Not In Exam**

- Go to WorkStation
- password : `student`

```sh
lab start boot-resetting
```

<hr>

- Now Go to `servera`
- click `esc` and select 2nd line and then click `e`
- Now go to line **linux** click `end` button
- Give space

```sh
rd.break #To break the password
```

```sh
mount -o remount,rw /sysroot/
```

```sh
chroot /sysroot
```

```sh
passwd root
#click enter and Give Password
```

```sh
touch /.autorelabel
```

```sh
exit
exit
```
