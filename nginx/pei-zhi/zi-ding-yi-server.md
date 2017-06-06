### 添加server

> ![](/assets/dlfkjglimport.png)
>
> ##### 在远程添加对应的文件夹和页面
>
> ```
> mkdir -p /mnt/app/hello
> touch /mnt/app/hello/index.html
> ```
>
> #### Tip:出现403错误解决\(SELinux开启导致\)
>
> > ##### 检查SELinux是否开启
> >
> > ```
> > getenforce
> >
> > --> 如果是Enforcing表示开启，需要修改目录的安全上下文
> > --> 如果是disable表示关闭，说明是其他问题导致
> > ```
> >
> > ##### 修改安全上下文
> >
> > ```
> > sudo chcon -Rt httpd_sys_content_t /mnt/app
> > ```

### 自定义默认server

> ##### 创建自定义配置文件
>
> ```
> sudo touch /etc/nginx/custom_default.conf
> ```
>
> ##### 编辑配置文件
>
> ```
> sudo vi /etc/nginx/custom_default.conf
>
> /**
> server {
>     listen         80 default_server;
>     root        /mnt/app/hello;
> }      
> */
> ```
>
> ##### 重启nginx

### location匹配地址区块

> #### 改造一下hello.conf
>
> ```
> server {
>       listen       80;
>       server_name  leon.com;
>      
>
>       location / {
>             root /mnt/app/hello;
>             index index.html index.htm;
>       }
>       
>       # 重新定义了v2区块下的资源目录
>       # nginx会优先匹配更具体的location
>       # 修改之后访问leon.com/v2/，会在/mnt/app/v2/下查找资源
>       location /v2 {
>             root      /mnt/app;      
>       }      
>       
>       
>       # ~* 表示不区分大小写
>       # expires 定义资源过期时间
>       location ~* \.(gif|jpg|png)$ {
>             expires 30d;
>       }
>
>       error_page 500 502 503 504 /50x.html;
>       location = /50x.html {
>             root /usr/share/nginx/html;
>       }
> }
> ```
>
> #### 创建v2和图片区块下所需的资源
>
> ```
> sudo cp -R /mnt/app/hello/ /mnt/app/v2
> sudo vi /mnt/app/v2/index.html   修改一下展示文字
>
> sudo mkdir /mnt/app/hello/img
> curl -o /mnt/app/hello/img/smile.jpg https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1496658871862&di=be450aaaf267ab27085c10547a92f282&imgtype=0&src=http%3A%2F%2Farticle.fd.zol-img.com.cn%2Ft_s640x2000%2Fg1%2FM02%2F00%2F0B%2FCg-4jlSHn_SIJNxUAAGaKW9F2ksAAOwPwPnsSAAAZpB771.jpg
> ```
>
> #### 重启nginx验证



