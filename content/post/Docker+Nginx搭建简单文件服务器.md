---
title: "Docker+Nginx搭建简单文件服务器"
date: 2018-06-24T18:48:57+08:00
draft: true
---

<!--more-->

## `安装Docker`
> [Ubuntu16.04安装Docker](http://www.xiaozefeng.xyz/post/ubuntu16.04%E5%AE%89%E8%A3%85docker/)  
> 其他平台安装docker请参考 [Docker官网](https://training.docker.com/)
## `配置加速`
> [Dcoker配置阿里云加速](http://www.xiaozefeng.xyz/post/ubuntu16.04%E5%AE%89%E8%A3%85docker/)


## `拉取nginx镜像`
```bash
docker pull nginx
```

## `准备工作`
### `找一个空文件夹`
```sh
mkdir file_system
cd file_system
```
### `创建存放nginx配置文件和需要存放的文件`
```sh
# conf 下存放一些自定义的nginx配置
# public 是你想要被外部访问的目录和文件
mkdir conf public
```

### `在conf目录下创建nginx配置文件 default.conf`
文件内容:  
```conf
server {
    listen       80;
    server_name  localhost;
    #charset koi8-r;
    #access_log  /var/log/nginx/log/host.access.log  main;

	autoindex on;# 显示目录
    autoindex_exact_size on;# 显示文件大小
    autoindex_localtime on;# 显示文件时间
	charset utf-8;# 解决文件乱码文件


    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    #location ~ \.php$ {
    #    root           html;
    #    fastcgi_pass   127.0.0.1:9000;
    #    fastcgi_index  index.php;
    #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
    #    include        fastcgi_params;
    #}

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}

```

### `配置文件说明`
> 除了这几行，其他内容时容器中nginx的默认配置

```conf
	autoindex on;# 显示目录
    autoindex_exact_size on;# 显示文件大小
    autoindex_localtime on;# 显示文件时间
	charset utf-8;# 解决文件乱码文件
```


## `创建容器`
```sh
docker run -d -p 80:80  --name fileSystem -v $PWD/conf:/etc/nginx/conf.d -v $PWD/public:/usr/share/nginx/html nginx
```

## `体验效果`
> 到public 目录下创建文件和目录, 然后访问

![](http://7xv4mv.com1.z0.glb.clouddn.com/blog/2018-06-24-110602.png)

