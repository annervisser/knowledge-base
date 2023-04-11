# Lock Screen when yubikey is removed

> ⚠️ Replace `YOUR_USER_NAME` with your username

Create a script to lock your current session:

`vi ~/.local/gnome-lock-on-yubikey.sh`
```shell
#!/usr/bin/env bash

logger "YubiKey Removed or Changed"
sessionids=`/bin/loginctl list-sessions | grep YOUR_USER_NAME | awk '{print $1}'`
for id in $sessionids; do
        logger "Locking session id:" $id
        /bin/loginctl lock-session $id
done
```

Call the above script when a yubikey is removed (based on vendor and model id)

`sudo vi /etc/udev/rules.d/85.yubikey.rules`
```shell
# Yubikey Udev Rule: running a bash script in case your Yubikey is removed 
ACTION=="remove", ENV{ID_VENDOR_ID}=="1050", ENV{ID_MODEL_ID}=="0407", RUN+="/home/YOUR_USER_NAME/.local/gnome-lock-on-yubikey.sh"
```

Reload udev rules:
```shell
sudo udevadm trigger
```
