---
layout: post
title: CentOS使用nginx配置PHP并让http与https共存
---

iOS9引入了新特性App Transport Security (ATS)。详情：App Transport Security (ATS)新特性要求App内访问的网络必须使用HTTPS协议。今天，在腾讯云上面开了一台CentOS6 64位机器【CentOS 7在腾讯云上有一些源还没有，相对来说CentOS6会更方便】

### 安装php和nginx

安装相关软件，一条命令完成

```
yum -y install nginx mysql-server php php-mysql php-gd php-fpm memcached php-pecl-memcache
```

### 配置nginx
```
vi /etc/nginx/conf.d/default.conf
```

```
#
# The default server
#
server {
    listen       80 default_server;
    listen       443 ssl;
    server_name  _;

    ssl_certificate /usr/share/nginx/server.crt;
    ssl_certificate_key /usr/share/nginx/server_nopwd.key;

    #charset koi8-r;

    #access_log  logs/host.access.log  main;

    # Load configuration files for the default server block.
    include /etc/nginx/default.d/*.conf;
    root /usr/share/nginx/html;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php$is_args$args;
    }

    error_page  404              /404.html;
    location = /404.html {
        root   /usr/share/nginx/html;
    }

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
    location ~ \.php$ {
        root           /usr/share/nginx/html;
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name; #！！！注意
        include        fastcgi_params;
    }

    include /etc/nginx/rewrite.d/*.conf;

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}
```

### 创建rewrite规则

```
mkdir /etc/nginx/rewrite.d
vim /etc/nginx/rewrite.d/wordpress.conf
```

### wordpress.conf内容
```
if (-f $request_filename/index.html){
	rewrite (.*) $1/index.html break;
}
if (-f $request_filename/index.php){
	rewrite (.*) $1/index.php;
}
if (!-f $request_filename){
	rewrite (.*) /index.php;
}

rewrite /wp-admin$ $scheme://$host$uri/permanent;
```


### 生成ssl

```
yum install openssl openssl-devel
```

### 生成key

```
openssl genrsa -des3 -out server.key 1024
openssl req -new -key server.key -out server.csr
openssl rsa -in server.key -out server_nopwd.key
openssl x509 -req -days 365 -in server.csr -signkey server_nopwd.key -out server.crt
```

并在nginx的配置文件default.conf中引用、

### 总结

现在你就可以去html文件夹部署你的php网站。第一次使用nginx，总的体验是非常棒！
