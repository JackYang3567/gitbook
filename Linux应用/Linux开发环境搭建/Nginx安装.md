#  Nginx安装

## Nginx安装所需环境
Nginx 是 C语言 开发，建议在 Linux 上运行，当然，也可以安装 Windows 版本，本篇则使用 CentOS 7 作为安装环境。

### 一. gcc 安装
cd /usr/local
安装 nginx 需要先将官网下载的源码进行编译，编译依赖 gcc 环境，如果没有 gcc 环境，则需要安装：
```
yum install gcc-c++
```
### 二. PCRE pcre-devel 安装
PCRE(Perl Compatible Regular Expressions) 是一个Perl库，包括 perl 兼容的正则表达式库。nginx 的 http 模块使用 pcre 来解析正则表达式，所以需要在 linux 上安装 pcre 库，pcre-devel 是使用 pcre 开发的一个二次开发库。nginx也需要此库。命令：
```
yum install -y pcre pcre-devel
```
### 三. zlib 安装
zlib 库提供了很多种压缩和解压缩的方式， nginx 使用 zlib 对 http 包的内容进行 gzip ，所以需要在 Centos 上安装 zlib 库。
```
yum install -y zlib zlib-devel
```
### 四. OpenSSL 安装
OpenSSL 是一个强大的安全套接字层密码库，囊括主要的密码算法、常用的密钥和证书封装管理功能及 SSL 协议，并提供丰富的应用程序供测试或其它目的使用。
nginx 不仅支持 http 协议，还支持 https（即在ssl协议上传输http），所以需要在 Centos 安装 OpenSSL 库。
```
yum install -y openssl openssl-devel
```
官网下载
1.直接下载.tar.gz安装包，地址：[https://nginx.org/en/download.html](https://nginx.org/en/download.html)

2.使用wget命令下载（推荐）。
```
wget -c https://nginx.org/download/nginx-1.15.8.tar.gz
```
解压
依然是直接命令：
```
tar -zxvf nginx-1.15.8.tar.gz
cd nginx-1.15.8
```
配置
其实在 nginx-1.15.8 版本中你就不需要去配置相关东西，默认就可以了。当然，如果你要自己配置目录也是可以的。
1.使用默认配置

./configure
2.自定义配置（不推荐）
```
./configure \
--prefix=/usr/local/nginx \
--conf-path=/usr/local/nginx/conf/nginx.conf \
--pid-path=/usr/local/nginx/conf/nginx.pid \
--lock-path=/var/lock/nginx.lock \
--error-log-path=/var/log/nginx/error.log \
--http-log-path=/var/log/nginx/access.log \
--with-http_gzip_static_module \
--http-client-body-temp-path=/var/temp/nginx/client \
--http-proxy-temp-path=/var/temp/nginx/proxy \
--http-fastcgi-temp-path=/var/temp/nginx/fastcgi \
--http-uwsgi-temp-path=/var/temp/nginx/uwsgi \
--http-scgi-temp-path=/var/temp/nginx/scgi
```
注：将临时文件目录指定为/var/temp/nginx，需要在/var下创建temp及nginx目录


编译安装
```
make
make install
```
查找安装路径：
```
whereis nginx
```

开机自启动
即在rc.local增加启动代码就可以了。
```
vi /etc/rc.local
```
增加一行 /usr/local/nginx/sbin/nginx
设置执行权限：
```
chmod 755 rc.local
```

### 启动nginx时就报错！
- 启动nginx
 ```
 /usr/local/nginx/sbin/nginx
 ```
报错: nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)

解决办法：
```
$ sudo fuser -k 80/tcp 

-bash: fuser: command not found #找不到fuser命令

```
安装：psmisc
```
yum install psmisc 
```
再运行：
```
fuser -k 80/tcp
/usr/local/nginx/sbin/nginx
````
```
Job for nginx.service failed because the control process exited with error code.

See "systemctl status nginx.service" and "journalctl -xe" for details.
```
你修改的语句末尾少了分号;


## Nginx/Tengine服务器安装SSL证书

在证书控制台下载Nginx版本证书。下载到本地的压缩文件包解压后包含：

.crt文件：是证书文件，crt是pem文件的扩展名。
.key文件：证书的私钥文件（申请证书时如果没有选择自动创建CSR，则没有该文件）。
友情提示： .pem扩展名的证书文件采用Base64-encoded的PEM格式文本文件，可根据需要修改扩展名。

以Nginx标准配置为例，假如证书文件名是a.pem，私钥文件是a.key。

在Nginx的安装目录下创建cert目录，并且将下载的全部文件拷贝到cert目录中。如果申请证书时是自己创建的CSR文件，请将对应的私钥文件放到cert目录下并且命名为a.key；
```
/usr/local/nginx/cert/a.key
/usr/local/nginx/cert/a.pem
```
打开 Nginx 安装目录下 conf 目录中的 nginx.conf 文件，找到：
```
# HTTPS server
# #server {
# listen 443;
# server_name localhost;
# ssl on;
# ssl_certificate cert.pem;
# ssl_certificate_key cert.key;
# ssl_session_timeout 5m;
# ssl_protocols SSLv2 SSLv3 TLSv1;
# ssl_ciphers ALL:!ADH:!EXPORT56:RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2:+EXP;
# ssl_prefer_server_ciphers on;
# location / {
#
#
#}
#}
```
将其修改为 (以下属性中ssl开头的属性与证书配置有直接关系，其它属性请结合自己的实际情况复制或调整) :
```
#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       80;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
	   proxy_pass http://127.0.0.1:29970;
          # proxy_pass http://127.0.0.1:8899;
	    proxy_set_header Host $host;
 	    proxy_set_header X-Forwarded-For $remote_addr;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
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


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    server {
        listen       443 ssl;
        server_name  localhost;

        ssl_certificate      ../cert/1533397779500.pem;
        ssl_certificate_key  ../cert/1533397779500.key;

        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;

       # ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
       # ssl_protocols TLSv1 TLSv1.1 TLSv1.2;        

        ssl_ciphers  HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers  on;

        location / {
       	    proxy_pass http://127.0.0.1:29970/;
	    proxy_set_header Host $host;
	    proxy_set_header X-Forwarded-For $remote_addr;
	}
    }

}
```
保存退出。

重启 Nginx。


## 在启动nginx的可能会报错
```
nginx: [emerg] the "ssl" parameter requires ngx_http_ssl_module in /usr/local/nginx/conf/nginx.conf
```
意思就是你的nginx未开启ssl模块

解决也比较容易，我们在编译的时候开启http_ssl_module模块就可以了
切换到源码包：
```
cd /usr/local/src/nginx-1.15.7
```
查看nginx原有的模块
```
/usr/local/nginx/sbin/nginx -V
```
在configure arguments:后面显示的原有的configure参数如下：
--prefix=/usr/local/nginx --with-http_stub_status_module 也可能会空哦

那么我们的新配置信息就应该这样写：
```
./configure --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module
```
运行上面的命令即可，等配置完

配置完成后，运行命令
make这里不要进行make install，否则就是覆盖安装

然后备份原有已安装好的nginx
```
cp /usr/local/nginx/sbin/nginx /usr/local/nginx/sbin/nginx.bak
```
然后将刚刚编译好的nginx覆盖掉原有的nginx（这个时候nginx要停止状态）
```
cp ./objs/nginx /usr/local/nginx/sbin/
```
然后启动nginx，仍可以通过命令查看是否已经加入成功