# F-Keys don't work

- Fix temporarily: `sudo bash -c "echo 2 > /sys/module/hid_apple/parameters/fnmode"`

- Make permanent:
    ```bash
    echo options hid_apple fnmode=2 | sudo tee -a /etc/modprobe.d/hid_apple.conf
    sudo update-initramfs -u -k all
    ```
# Key combinations
| Combination | Effect |
| ------------------------------------ | ------------------------------------------------------------------ |
| Fn + right Ctrl                      | menu                                                               |
| Fn + Win                             | enable/disable Win key                                             |
| Fn + left Win (hold 3 seconds)       | Caps Lock flashes 3 times, Fn and Win key swapped                  |
| Fn + left Ctrl (hold 3 seconds)      | Caps Lock flashes 3 times, Caps Lock and left Ctrl key swapped     |
| Fn + Esc (hold 3 seconds)            | keyboard will become defaulted version (Caps Lock flashes 3 times) |
| Fn + -> (Right Arrow)                | swap between "full backlit" mode and "breathing mode"              |
| Fn + /\ (Up Arrow)                   | Increase brightness (backlit mode) or  speed (breathing mode)      |
| Fn + \/ (Down Arrow)                 | Decrease brightness (backlit mode) or  speed (breathing mode)      |
 
\
\
\
\
\
\
\
Sources:
- https://gist.github.com/vladak/b005b0446eeb049a8b4cd546bf11dbbc
- https://askubuntu.com/a/7553/1019013
- https://www.reddit.com/r/Varmilo/comments/g4sabk/fn_lock_on_va87m/
