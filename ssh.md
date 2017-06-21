### 本机生成SSH

> ```
> ssh-keygen
> ```
>
> 执行后再 ~/.ssh 目录下回生成一对秘钥

### 配置服务器

> #### 在用户主目录下创建 .ssh 目录和 authorized\_keys 文件
>
> ```
> cd ~
> mkdir .ssh
> touch .ssh/authorized_keys
> ```
>
> #### 将本机的公钥复制到 autorized\_keys 文件
>
> ```
> cat ~/.ssh/id_rsa.pub    // 本机
> ```
>
> #### 设置文件权限
>
> ```
> chmod 700 ~/.ssh
>
> chmod 600 ~/.ssh/authorized_keys
> ```

### 修改服务器配置文件

> ```
> vi /etc/ssh/sshd_config
> ```
>
> #### 配置如下：
>
> ```
> #禁用root账户登录，如果是用root用户登录请开启
> PermitRootLogin yes
> ```
>
> ```
> # 是否让 sshd 去检查用户家目录或相关档案的权限数据，
> # 这是为了担心使用者将某些重要档案的权限设错，可能会导致一些问题所致。
> # 例如使用者的 ~.ssh/ 权限设错时，某些特殊情况下会不许用户登入
> StrictModes no
> ```
>
> ```
> # 是否允许用户自行使用成对的密钥系统进行登入行为，仅针对 version 2。
> # 至于自制的公钥数据就放置于用户家目录下的 .ssh/authorized_keys 内
> RSAAuthentication yes
> PubkeyAuthentication yes
> AuthorizedKeysFile  .ssh/authorized_keys
> ```
>
> ```
> # 有了证书登录了，就禁用密码登录吧，安全要紧
> PasswordAuthentication no
> ```

### 重启ssh服务



