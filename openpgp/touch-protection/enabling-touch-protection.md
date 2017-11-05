#### 启用触摸保护

把 [Yubikey-manager](https://developers.yubico.com/yubikey-manager/) 安装在一个绝对路径：【译者注：homebrew 是 macOS 平台的包管理软件】

```sh
❯ brew install libu2f-host libusb swig ykpers
❯ git clone git@github.com:Yubico/Yubikey-manager.git
❯ git submodule update --init --recursive
❯ pip install -e .
```

安装工具会自动把 `ykman` 文件链接到 `/usr/local/bin/ykman` ，但是原始 git 文件夹必须保留在硬盘上。

然后，为验证（`aut`）， 加密（`enc`）和签名（`sig`）打开触摸验证：

```sh
❯ ykman openpgp touch aut on
❯ ykman openpgp touch enc on
❯ ykman openpgp touch sig on
```

确保触摸验证已经打开：

```sh
❯ ykman openpgp touch aut
Current touch policy of AUTHENTICATE key is ON.

❯ ykman openpgp touch enc
Current touch policy of ENCRYPT key is ON.

❯ ykman openpgp touch sig
Current touch policy of SIGN key is ON.
```
