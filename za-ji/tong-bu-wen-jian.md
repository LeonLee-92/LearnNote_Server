### tip:如果没有connect成功，打开远程的密码ssh访问

> ```
> sudo vi /etc/ssh/sshd_config
>
> ->  PasswordAuthentication no --> yes
> ```

---

#### 

#### 

#### 安装remote-ftp

![](/assets/imporsdft.png)

#### 在本地生成文件夹，并生成配置文件

![](/assets/impor23erfdt.png)

#### 修改远程主机登录信息

```
{
    "protocol": "sftp",
    "host": "192.168.1.110",
    "port": 22,
    "user": "vagrant",
    "pass": "vagrant",
    "promptForPass": false,
    "remote": "/etc/nginx",
    "agent": "",
    "privatekey": "",
    "passphrase": "",
    "hosthash": "",
    "ignorehost": true,
    "connTimeout": 10000,
    "keepalive": 10000,
    "keyboardInteractive": false,
    "watch": []
}
```

#### 挂载远程目录

![](/assets/impsdfdfort.png)

![](/assets/imporsdfdsfsdft.png)

![](/assets/impor123xaft.png)

