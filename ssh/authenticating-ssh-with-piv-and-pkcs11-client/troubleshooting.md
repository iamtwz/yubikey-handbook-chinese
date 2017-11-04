### 故障排除

**Could not add card "/usr/local/opt/opensc/lib/pkcs11/opensc-pkcs11.so": agent refused operation**

对于缺乏肯定的诊断，运行 `pkill ssh-agent` 然后物理插拔一下 Yubikey 即可。
