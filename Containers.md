<!--
  Author: omteja04
  Created on: 06-06-2024 15:16:20
  Description: Containers
-->
<!-- cSpell:disable -->

### Containers

```bash
# in workstation
lab start containers-services
# Only in practice not required in lab
```

```bash
ssh student@servera
```

```bash

wget https://raw.githubusercontent.com/Prithivrajgankai/Ascii2pdf-Containerfile/main/Containerfile

# Only in practice not required in lab
```

```sh
ls
# In important configuration we will get registry link
podman login registry.lab.example.com

# username : admin

# password : redhat321

podman build -t monitor .

podman images # to check the images that are running

exit
```

```bash

ssh root@servera

mkdir /opt/files /opt/processed

chmod 777 /opt/files /opt/processed

ls -ld /opt/files /opt/processed

chown student:student /opt/files /opt/processed #To change owner

ls -ld /opt/files /opt/processed # To check

exit
```

```bash
# Back to root

ssh student@servera

podman ps

podman run -d --name ascii2pdf -v /opt/files:/opt/incoming:Z -v /opt/processed:/opt/outcoming:Z localhost/monitor:latest

podman ps # To see containers that are running


# Make container as service

mkdir -p ~/.config/systemd/user

cd ~/.config/systemd/user

podman generate systemd --name ascii2pdf --files --new

ls # To check

podman stop ascii2pdf

podman ps

podman rm ascii2pdf


systemctl --user daemon-reload

podman ps

systemctl --user start container-ascii2pdf.service

podman ps

systemctl --user enable container-ascii2pdf.service

podman ps

exit
```

```bash

ssh root@servera

loginctl enable-linger student

loginctl show-user student


```
