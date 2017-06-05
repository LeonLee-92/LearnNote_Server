创建仓库

```
rmate /etc/yum.repos.d/nginx.repo

写入：
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/mainline/centos/7/$basearch/
gpgcheck=0
enabled=1
```

安装

```
sudo yum install nginx -y
```

启动并开机自启动

```
sudo systemctl start nginx
sudo systemctl reload nginx
```

访问主机ip验证

```
ip addr
```



