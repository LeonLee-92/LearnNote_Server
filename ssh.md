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
> 将本机的公钥复制到 autorized\_keys 文件
>
> ```
> cat ~/.ssh/id_rsa.pub    // 本机
> ```





