<!--
  Author: omteja04
  Created on: 09-06-2024 06:33:44
  Description: PasswordExpiry
-->

```bash
# Edit /etc/login.defs
vim /etc/login.defs
```

(In `vim`, find the line `PASS_MAX_DAYS` and change its value from `99999` to `20`. Then save and exit with `:wq!`)

```bash
# Reboot the system
reboot
```
