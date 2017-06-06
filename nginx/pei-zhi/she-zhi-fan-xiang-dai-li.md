#### 添加需要反向代理的location

> ```
> server {
>
>       listen 80;
>       server_name leon.com;
>             
>       location / {
>             root /mnt/app/hello;
>             index index.html index.htm;
>       }
>       
>       location /v2 {
>             root /mnt/app;
>       }
>       
>       location ~* \.(gif|jpg|png)$ {
>             root /mnt/app/hello;
>             expires 30d;
>       }
>       
>       # 将包含 /api 的请求，移交监听api.leon.com的服务器处理
>       location /api {
>             proxy_pass http://api.leon.com;
>       }
> }
> ```

#### 添加代理服务器

> ```
> # 代理服务器监听api.leon.com请求
> server {
>         listen          80;
>         server_name     api.leon.com;
>         root            /mnt/app;
>         access_log      /var/log/nginx/api_access.log main;
> }
> ```

#### 添加所需资源

> ```
> sudo mkdir -p /mnt/app/api
> sudo vi /mnt/app/api/index.json
>
> 添加：        
> {
>     "data": "hello"
> }
> ```

---

### 在日志中显示访问用户的真实IP

> ##### 目前，在/var/log/nginx/api\_access.log的日志中没有用户访问的真实IP
>
> ![](/assets/kdfngkimport.png)
>
> #### 解决：【我并没有解决】
>
> ##### 在需要代理的区块中添加header
>
> ```
> ...
>
> location /api {
>     proxy_pass http://api.leon.com;
>     proxy_set_header X-Real-IP $remote_addr;
>     proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
> }
>
> ...
> ```



