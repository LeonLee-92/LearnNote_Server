### 挂载远程/etc/nginx文件夹

![](/assets/imdfsdport.png)

### 主配置文件结构

```ruby
#运行nginx的用户和群组
user  nginx nginx;
#工作进程的数量，一般设置为服务器cpu核心数量
worker_processes  1;

#错误日志位置
error_log  /var/log/nginx/error.log warn;
#保存主进程的进程id文件所在的位置
pid        /var/run/nginx.pid;

#和连接有关的指令
events {
    #一个工作进程可以接收的连接数量
    worker_connections  1024;
}


http {
    #导入mime类型
    include       /etc/nginx/mime.types;
    #mime类型列表中没有，默认当做二进制数据处理
    default_type  application/octet-stream;
    #定义日志的格式
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';
    #指定访问日志的位置
    access_log  /var/log/nginx/access.log  main;

    #经过优化的数据传输方法
    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    #导入service服务配置
    include /etc/nginx/conf.d/*.conf;
}
```

### .conf文件中server结构

```ruby
server {
    #监听的端口和ip地址
    listen       80;
    server_name  localhost;

    #定义匹配模式
    location / {
        #资源目录
        root   /usr/share/nginx/html;
        #默认依次打开的页面
        index  index.html index.htm;
    }


    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
```

### 

#### 



