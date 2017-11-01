## 验证 SSH 服务器证书（客户端）

和 [SSH 用户证书](#remote-ssh-authentication-via-user certificates) 类似，也可以使用客户端机构认证来验证主机。需要一个 SSH 服务器证书签发机构签发服务器证书，客户端只需要保存 CA 的公钥。

1. 使用一台气隙系统的计算机来生成服务器证书签发机构的根证书：

  ```sh
  ❯ ssh-keygen -C "SSH Server Certificate Authority" -f sshserver.root.ca
  ```

2. 使用服务器证书签发机构来对服务器的公钥进行签名：

  ```sh
  ❯ ssh-keygen -s sshserver.root.ca -I <identity> -h -n <hostname> -V +52w /etc/ssh/ssh_host_rsa_key.pub

  Signed host key /etc/ssh/ssh_host_rsa_key-cert.pub: id "foobar.com-key" serial 0 for foobar.com valid from 2016-12-10T00:10:00 to 2017-12-09T00:10:10
  ```

3. 修改 `/etc/ssh/sshd_config` 文件以包含新的主机证书：

  ```sh
  HostCertificate /etc/ssh/ssh_host_rsa_key-cert.pub
  ```

4. 把 CA 添加到本地 SSH（`~/.ssh/known_hosts`）：

  ```
  @cert-authority *.foobar.com <content of sshserver.root.ca.pub>
  ```
