#### 在atom中安装remote atom插件![](/assets/isdmport.png)

#### 开启start server

![](/assets/asdfimport.png)

#### 在远程安装rmate工具

```
sudo curl -o /usr/local/bin/rmate  https://raw.githubusercontent.com/aurora/rmate/master/rmate
sudo chmod +x /usr/local/bin/rmate
```

#### 重新登录远程

```
ssh -R 52698:localhost:52698 vagrant@[ip]
```

#### 开始使用，在远程打开文件

```
rmate hello.txt
```



