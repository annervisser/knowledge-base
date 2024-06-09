## Preparation

### Installing an android emulator (AVD)
- Install android studio, this is the easiest way to get all the android tools set up
- Make sure adb and aapt are in your path:
  - `PATH="$HOME/Android/Sdk/platform-tools:$PATH"`
  - `PATH="$HOME/Android/Sdk/build-tools/34.0.0:$PATH"`


#### Objection
- install objection: `pip install -U objection` (-U upgrades to the latest version in case it's installed)
- check install: `objection version`

### Install a proxy:
https://mitmproxy.org

- right click download button and copy link
- `wget <URL>`
- `tar -xzf mitmproxy*.tar.gz`
- run the proxy: `./mitmweb`
- A browser will open, and the proxy will be running at port 8080


## Execution

### Patching apk
#### Getting a play store app
- Install emulator
- Install Aurora Store: https://files.auroraoss.com/AuroraStore/Stable/
- Installed app from aurora store

#### Patching APK
- Find package name: `adb shell cmd package list packages`
- Find apk path: `adb shell pm com.app.package`
- Pull apk: `adb pull /data/app/....../base.apk com.app.package.apk`
- Patch apk: `objection patchapk com.app.package.apk`

#### Installing patched APK
- Uninstall app in emulator (`adb uninstall com.app.package`)
- Install patched apk: `adb install com.app.package.apk`

#### Capturing request data
- Run mitmproxy (DISABLE HTTP/2): `mitmweb --no-http2`
- set proxy configuration:
  - Emulator configuration seems not to work properly, use android wifi settings or adb: `adb shell settings put global http_proxy 192.168.x.x:8080` (use computer LAN address, not localhost)
- Install certificate by going to mitm.it in emulator
- Open app
- app wont load, until you run `objection explore`
- run `android sslpinning disable`
- You should now be able to see requests in mitmproxy

<details>
  <summary>Old</summary>

  ### Installing patchapk dependencies
  - `sudo apt install aapt apksigner zipalign`
  - apktool: [https://ibotpeaches.github.io/Apktool/install/](https://ibotpeaches.github.io/Apktool/install/)
    
  ### Install patch-apk
  - `gh repo clone annervisser/patch-apk`
  - `cd patch-apk`192.168.8.230
  - `git checkout switch-jarsigner-to-objection-signapk`
  - `pip install setuptools`
</details>
