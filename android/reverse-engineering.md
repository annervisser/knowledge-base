## Preparation

### Installing an android emulator (AVD)
- Install android studio, this is the easiest way to get all the android tools set up

#### Objection
- install objection: `pip install -U objection` (-U upgrades to the latest version in case it's installed)
- check install: `objection version`

### Installing patchapk dependencies
- `sudo apt install aapt apksigner zipalign`
- apktool: [https://ibotpeaches.github.io/Apktool/install/](https://ibotpeaches.github.io/Apktool/install/)

### Install a proxy:
https://mitmproxy.org

- right click download button and copy link
- `wget <URL>`
- `tar -xzf mitmproxy*.tar.gz`
- run the proxy: `./mitmweb`
- A browser will open, and the proxy will be running at port 8080

### Install patch-apk
- `gh repo clone annervisser/patch-apk`
- `cd patch-apk`
- `git checkout switch-jarsigner-to-objection-signapk` 

## Execution

### Patching apk
- Install emulator
- Install Aurora Store: https://files.auroraoss.com/AuroraStore/Stable/
- Installed app from aurora store
- Find package name: `adb shell cmd package list packages`
- Patch apk: `python3 patch-apk.py com.app.package`
- Run mitmproxy (DISABLE HTTP/2)
- set proxy configuration via emulator (or in wifi settings)
- Install certificate by going to mitm.it
- Open app
- app wont load, until you run `objection explore`
- run `android sslpinning disable`
- You should now be able to see requests in mitmproxy
