#### 安装 libpam-yubico

`libpam-yubico` 提供了将 Yubico 软件集成到 PAM（Linux Pluggable Authentication Modules，Linux 可插拔身份验证模块）所需要的依赖。

可以通过添加 PPA 仓库的方式安装：

```sh
❯ apt-get install -y vim software-properties-common
❯ add-apt-repository -y ppa:yubico/stable
❯ apt-get update
❯ apt-get install -y libpam-yubico
```
