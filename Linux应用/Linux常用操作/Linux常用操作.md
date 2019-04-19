# Linux常用操作
## 一、宝塔Linux面板登录信息显示（本地vagrant）
```
在终端输入命令：
#  /etc/init.d/bt default

显示如下信息：
Bt-Panel: http://192.168.33.10:8888/e937db4e
username: fihq9pmi
password: cf99d8a1
Warning:
If you cannot access the panel, 
release the following port (8888|888|80|443|20|21) in the security group

在浏览器地址栏粘贴：http://192.168.33.10:8888/e937db4e


```

---
```
Bt-Panel: http://192.168.33.10:8888/462c7d08
username: jexcrsi4
password: ce87dc0c
Warning:
If you cannot access the panel,
release the following port (8888|888|80|443|20|21) in the security group
==================================================================
Time consumed: 3 Minute!

FTP账号资料
用户：lottery_front_com
密码：dXexEi3y8Ndha5NN
 

```
---
宝塔Linux面板管理常用命令：[https://www.bt.cn/btcode.html](https://www.bt.cn/btcode.html)

## 二、实战

![添加网站.png](添加网站.png)
![成功创建站点.png](成功创建站点.png)

FTP用户名  
   gk_test1_com
密码  
   n5D5ApwfsHbHjsX7


## 三、实例
众筹后台：
```

```

## 四、站点服务器配置文件

```
server
{
    listen 80;
	listen 443 ssl http2;
    server_name 7988z.com 6988z.com m.589ty.cn m.fmf3.cn m.fma2.cn 1699z.com 1299z.com 2988z.com;
    index index.php index.html index.htm default.php default.htm default.html;
    root /www/wwwroot/qt;
    
    #SSL-START SSL相关配置，请勿删除或修改下一行带注释的404规则
    #error_page 404/404.html;
    ssl_certificate    /etc/letsencrypt/live/7988z.com/fullchain.pem;
    ssl_certificate_key    /etc/letsencrypt/live/7988z.com/privkey.pem;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE;
    ssl_prefer_server_ciphers on;
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 10m;
    error_page 497  https://$host$request_uri;


    #SSL-END
    
    #ERROR-PAGE-START  错误页配置，可以注释、删除或修改
    error_page 404 /404.html;
    error_page 502 /502.html;
    #ERROR-PAGE-END
    
    #PHP-INFO-START  PHP引用配置，可以注释或修改

	include enable-php-00.conf;
    #PHP-INFO-END
    
    #REWRITE-START URL重写规则引用,修改后将导致面板设置的伪静态规则失效
    include /www/server/panel/vhost/rewrite/7988z.com.conf;
    #REWRITE-END
    
    #禁止访问的文件或目录
    location ~ ^/(\.user.ini|\.htaccess|\.git|\.svn|\.project|LICENSE|README.md)
    {
        return 404;
    }
    
    #一键申请SSL证书验证目录相关设置
    location ~ \.well-known{
        allow all;
    }
    
    location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$
    {
        expires      30d;
        error_log off;
        access_log /dev/null; 
    }
    location ~ .*\.(js|css)?$
    {
        expires      12h;
        error_log off;
        access_log /dev/null; 
    }
    
        location ~ ^/api/{
        	
        	rewrite ^/api/(.*)$  /$1  break;
            proxy_pass  https://djycpgk.362e.cn;
            proxy_set_header Host djycpgk.362e.cn;
                    #Proxy Settings
        proxy_redirect     off;
        proxy_set_header   X-Real-IP        $remote_addr;
        proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
        proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;
        proxy_max_temp_file_size 0;
        proxy_connect_timeout      90;
        proxy_send_timeout         90;
        proxy_read_timeout         90;
        proxy_buffer_size          4k;
        proxy_buffers              4 32k;
        proxy_busy_buffers_size    64k;
        proxy_temp_file_write_size 64k;
        }
   
	access_log  /www/wwwlogs/7988z.com.log;
    error_log  /www/wwwlogs/7988z.com.error.log;
}

```
众筹前台：
1299z.com
7988z.com

---

## 五、Vagrant Linux中应用宝塔Linux面板

### 文件说明
 * cjq.tar.gz 是采集器 上传到服务器的home下，解压，npm i
 * djycpgk.zip是网站后台管理代码
 *  front.zip是网站前台代码
 *  sb28_.sql是mysql数据库备份数据，在bt中导入
 
---

### vagrangt中使用BTLinux面板部署站点

#### 1、在bt面板安装成功且LNMP安装完成后
#### 2、在linux 的 /etc/hosts中要做映射

```
192.168.33.10  xxxx.xxxx.com #网站后台 lottery.front.com
192.168.33.10  xxxx.xxxx.com #网站前台  lottery.manage.com
```

#### 3、在宿主机win10中做C:\Windows\System32\drivers\etc\hosts

```
192.168.33.10  xxxx.xxxx.com #网站后台 lottery.front.com
192.168.33.10  xxxx.xxxx.com #网站前台 lottery.manage.com
```

#### 4、在bt面板中做反向代理
  * 步骤一、

 
![bt中反向代理设置-1.png](bt中反向代理设置-1.png)

  * 步骤二、

 
![bt中反向代理设置-2.png](bt中反向代理设置-2.png)

  * 步骤三、在配置文件中添加如下代码： 

```
 location ~ ^/api/{
        	
        	rewrite ^/api/(.*)$  /$1  break;
            proxy_pass  https:/xxxx.xxxx.com;
            proxy_set_header Host xxxx.xxxx.com;
                    #Proxy Settings
        proxy_redirect     off;
        proxy_set_header   X-Real-IP        $remote_addr;
        proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
        proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;
        proxy_max_temp_file_size 0;
        proxy_connect_timeout      90;
        proxy_send_timeout         90;
        proxy_read_timeout         90;
        proxy_buffer_size          4k;
        proxy_buffers              4 32k;
        proxy_busy_buffers_size    64k;
        proxy_temp_file_write_size 64k;
        }
```
