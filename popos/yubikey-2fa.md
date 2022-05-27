- https://support.system76.com/articles/yubikey-login/
- https://developers.yubico.com/yubico-pam/Authentication_Using_Challenge-Response.html

XPS15 config in /etc/pam.d/common-auth:
```
# here are the per-package modules (the "Primary" block)
auth    required        pam_yubico.so mode=challenge-response chalresp_path=/var/yubico
auth    [success=2 default=ignore]      pam_unix.so nullok try_first_pass
auth    [success=1 default=ignore]      pam_sss.so use_first_pass
```
