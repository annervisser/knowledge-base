# TL;DR
## F-Keys don't work

Fix temporarily: `sudo bash -c "echo 2 > /sys/module/hid_apple/parameters/fnmode"`
Make permanent:
```bash
echo options hid_apple fnmode=2 | sudo tee -a /etc/modprobe.d/hid_apple.conf
sudo update-initramfs -u -k all
```



# Full gist
---
Original source: https://gist.github.com/vladak/b005b0446eeb049a8b4cd546bf11dbbc

# Mechanical keyboards

nice infographics on https://www.reddit.com/r/MechanicalKeyboards/comments/jihbhi/custom_mechanical_keyboard_infographic_v30_is_now/

# My Varmilo VA87M

Cherry MX Brown - to make it similar to the Sun Type 7 keyboard I was using previously (excellent keyboard however too wide).

Fn key - the "house/home" key

review: https://www.rtings.com/keyboard/reviews/varmilo/va87m

## Manual

retyped from the booklet:

### Preface

Varmilo comes from Esperanto 'Via' 'armilo', which means the unique keyboard customized for you.

### Backlight adjustment

Fn + -> : swapping between "full backlit" mode and "breathing mode"
Caps Lock, Scroll lock, Number Lock do not operate in light effects
Under Breath, press Fn + down to slow down a light effect or Fn + up to speed it up
Under Always on, press Fn + down to decrease light brightness or Fn + up to increase it
The above functions are available only for the keyboards with LEDs

### Multi-media functions

To enable multi-media function, press Fn and the key corresponding to the function

| Combination | Effect |
| --------- | --------- |
| `Fn + <<` | last song |
| `Fn + >\|\|` | pause/play |
| `Fn + >>` | next song |
| `Fn + striked speaker` | mute |
| `Fn + speaker with low volume` | Volume - |
| `Fn + speaker with high volume` | Volume + |

### Other functions:

| Combination | Effect |
| ----------- | ------ |
| Fn + right Ctrl | menu |
| Fn + Win | enable/disable Win key |
| Fn + left Win (more than 3 seconds) | Caps Lock flashes 3 times, Fn and Win key swapped |
| Fn + left Ctrl (more than 3 seconds) | Caps Lock flashes 3 times, Caps Lock and left Ctrl key swapped |
| Pressing Fn + Esc 3 seconds | keyboard will become defaulted version (Caps Lock flashes 3 times) |

NKRO under Windows mode

# Function keys

The F1-F5 keys only work on Linux with the Fn key by default.

https://forums.servethehome.com/index.php?threads/varmilo-keyboard-fn-keys-under-linux.29041/ mentions the keyboard uses `hid_apple` to handle the input events and has even some hypothesis on the default behavior:

> A little bit of digging around later and it seems that linux defaults to expecting apple users to press a Fn key before being able to access the functions. News to me, but I'm not a mac user. Thankfully it seems the hid_apple module takes a parameter called fnmode to control behaviour of the function keys; the default value of 1 is what's causing the unexpected behaviour.

## Workaround

https://wiki.archlinux.org/index.php/Apple_Keyboard has verbose info on how to change the default behavior, specifically:

```
hid_apple module options

    fnmode - Mode of top-row keys

   0 = disabled
   1 = normally media keys, switchable to function keys by holding Fn key (Default)
   2 = normally function keys, switchable to media keys by holding Fn key
```

and 

```
Function keys do not work

If your F<num> keys do not work, this is probably because the kernel driver for the keyboard has defaulted to using the media keys and requiring you to use the Fn key to get to the F<num> keys. To change the behavior temporarily, append 2 to /sys/module/hid_apple/parameters/fnmode.

# echo 2 >> /sys/module/hid_apple/parameters/fnmode

To make the change permanent, set the hid_apple fnmode option to 2:

/etc/modprobe.d/hid_apple.conf

options hid_apple fnmode=2

To apply the change to your initial ramdisk, in your mkinitcpio configuration (usually /etc/mkinitcpio.conf), make sure you either have modconf included in the HOOKS variable or /etc/modprobe.d/hid_apple.conf in the FILES variable. You would then need to regenerate the initramfs. 
```

https://askubuntu.com/a/7553/1019013 has this all in one package:

```
You can try:

sudo bash -c "echo 2 > /sys/module/hid_apple/parameters/fnmode"

If it works you can change this permanently (per the linked wiki page):

echo options hid_apple fnmode=2 | sudo tee -a /etc/modprobe.d/hid_apple.conf
sudo update-initramfs -u -k all
sudo reboot # optional
```

## Solution

https://www.reddit.com/r/Varmilo/comments/g4sabk/fn_lock_on_va87m/ has a link to Dropbox that has a Windows program with updated firmware that changes the default behavior.

Downloaded locally as `VA87M 88M 108M 109M.zip`
