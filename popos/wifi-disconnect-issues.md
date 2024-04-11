Problem: During Zoom calls in the office the internet randomly disconnect or hangs.


Pop!OS comes with powermode enabled by default (`/etc/NetworkManager/conf.d/default-wifi-powersave-on.conf`)

```shell
# Create our own config
printf "[connection]\nwifi.powersave = 0\n" | sudo tee /etc/NetworkManager/conf.d/custom-wifi-powersave-off.conf

# Disable system-provided config (but keep it around)
sudo mv /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf.bak
```


### Sources

- https://gist.github.com/jcberthon/ea8cfe278998968ba7c5a95344bc8b55
