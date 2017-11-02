#### 预备条件（仅限演示）

你需要一个包含 OpenSSH 的 Linux 操作系统（例如 Ubuntu）：

```sh
❯ docker run --name yubico-ubuntu -p 2222:22 -it ubuntu
```

在 Docker 容器内：

```sh
❯ apt-get update
❯ apt-get install -y openssh-server vim
❯ mkdir -p /root/.ssh
```

为测试过程新建账户：

```sh
❯ adduser foobar
❯ usermod -G sudo foobar
❯ mkdir -p /home/foobar/.ssh
```

为两个用户新增 SSH 公钥，首先是本地用户:

```sh
❯ cat ~/.ssh/id_rsa.pub | pbcopy
```

然后:

```sh
❯ echo "<pubkey>" >> /home/foobar/.ssh/authorized_keys
❯ echo "<pubkey>" >> /root/.ssh/authorized_keys
```

如果你想使用 `root` 用户进行 SSH 操作，别忘了设置一个密码:

```sh
❯ passwd root
```
