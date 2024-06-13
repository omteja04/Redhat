<!--
  Author: omteja04
  Created on: 07-06-2024 11:40:00
  Description: TunedProfile
-->

```sh
yum install tuned -y
```

```sh
systemctl start tuned.service
```

```sh
systemctl enable tuned.service
```

```sh
# To check current active profile
tuned-adm active
```

```sh
tuned-adm recommend
```

`virtual-guest` &rarr; (This one is recommended)

```sh
tuned-adm profile virtual-guest
```

```sh
tuned-adm active
```
