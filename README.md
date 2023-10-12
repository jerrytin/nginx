# nginx
## 简介
Nginx (engine x) 是一个高性能的HTTP和反向代理web服务器，同时也提供了IMAP/POP3/SMTP服务。它是由俄罗斯人Igor Sysoev（伊戈尔·塞索耶夫）编写的。  
Nginx是一款轻量级的Web 服务器，因它的稳定性、丰富的功能集、示例配置文件和低系统资源消耗而闻名。其特点是占用内存少，并发能力强，事实上Nginx的并发能力在同类型的web服务器中表现较好。  
在国内，已经有百度、京东、新浪、网易、腾讯、淘宝等多家网站使用Nginx作为Web服务器或反向代理服务器。

## 选择Nginx的理由
1.高并发连接:官方测试Nginx能够支持5万并发连接，在实际生产环境中可支撑2-4万并发连接数。  
2.消耗内存少:在同等硬件环境下，Nginx的处理能力相当于Apache的5-10倍。  
3.成本低廉:Nginx作为开源软件，可以免费使用，并且可用于商业用途。  
4.其它理由  
配置文件非常简单  
支持Rewrite重写规则  
内置健康检查功能  
节省带宽  
稳定性高  
...  

## 安装与配置
### 安装
> Mac如何安装nginx

由于mac自带brew，所以mac下安装nginx相对比较简单。 查看版本号：brew -v  
更新Homebrew : brew update  
搜索nginx：brew search nginx  
安装：brew install nginx  
查看nginx版本：nginx -v  
查看nginx信息：brew info nginx  
启动nginx：nginx  
访问网址：http://localhost:8080  
重启nginx：nginx -s reload  

    sudo kill -QUIT 进程号
1、查看brew版本

    brew -v
2、更新Homebrew（如果版本比较老）

    brew update
3、安装nginx

    brew search nginx
    brew install nginx
4、安装完成查看版本

    nginx -v
可通过以下命令查看nginx信息，如安装路径等

    brew info nginx
#### 启动nginx

    nginx
#### 重启

    nginx -s reload
#### 关闭

    sudo kill -QUIT 进程号
#### 输入

`ps -ef|grep nginx`

    501 44255     1   0  6:37下午 ??         0:00.00 nginx: master process nginx
    501 44256 44255   0  6:37下午 ??         0:00.00 nginx: worker process
    501 11397 11355   0 一06下午 ttys004    0:00.03 docker pull nginx
    501 11466 11355   0 一06下午 ttys004    0:00.02 docker pull nginx
    501 44266 44114   0  6:37下午 ttys006    0:00.00 grep --color=auto --exclude-dir=.bzr --exclude-dir=CVS --exclude-dir=.git --exclude-dir=.hg --exclude-dir=.svn nginx

可以看到第一个是我们当前启动的nginx 名称也要nginx

> 关闭nginx，直接杀死进程

    nginx -s stop
#### 设置环境变量

    vim /etc/profile
shift+G到最后一行 更改模式为insert->i

    export NGINX_HOME=/usr/local/nginx
    export PATH=$PATH:$NGINX_HOME/sbin
保存  
1.按下esc键  
2.输入":wq"(保存退出) 输入":q!"(不保存退出)  

#### 刷新环境变量  

    source /etc/profile
重新启动nginx，查看他的进程

`nginx
ps -ef|grep nginx`
    

    501 45002     1   0  6:58下午 ??         0:00.00 nginx: master process nginx
    501 45003 45002   0  6:58下午 ??         0:00.00 nginx: worker process
    501 11397 11355   0 一06下午 ttys004    0:00.03 docker pull nginx
    501 11466 11355   0 一06下午 ttys004    0:00.02 docker pull nginx
    501 45091 44114   0  7:00下午 ttys006    0:00.00 grep --color=auto --exclude-dir=.bzr --exclude-dir=CVS --exclude-dir=.git --exclude-dir=.hg --exclude-dir=.svn nginx


可以看到也正常启动起来了。
mac中默认的路径

    /usr/local/etc/nginx/nginx.conf （配置文件路径）
可以通过

    open /usr/local/etc/nginx/
来查看配置文件所在的文件夹

“html”的相对路径在哪里？此相对路径在编译时设置。可以通过命令检查路径：

`nginx -V`
    
    TLS SNI support enabled  
    configure arguments: --prefix=/usr/local/Cellar/nginx/1.17.3_1 --sbin-path=/usr/local/Cellar/nginx/1.17.3_1/bin/nginx --with-cc-opt='-I/usr/local/opt/pcre/include -I/usr/local/opt/openssl@1.1/include' --with-ld-opt='-L/usr/local/opt/pcre/lib -L/usr/local/opt/openssl@1.1/lib' --conf-path=/usr/local/etc/nginx/nginx.conf --pid-path=/usr/local/var/run/nginx.pid --lock-path=/usr/local/var/run/nginx.lock --http-client-body-temp-path=/usr/local/var/run/nginx/client_body_temp --http-proxy-temp-path=/usr/local/var/run/nginx/proxy_temp --http-fastcgi-temp-path=/usr/local/var/run/nginx/fastcgi_temp --http-uwsgi-temp-path=/usr/local/var/run/nginx/uwsgi_temp --http-scgi-temp-path=/usr/local/var/run/nginx/scgi_temp --http-log-path=/usr/local/var/log/nginx/access.log --error-log-path=/usr/local/var/log/nginx/error.log --with-compat --with-debug --with-http_addition_module --with-http_auth_request_module --with-http_dav_module --with-http_degradation_module --with-http_flv_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_mp4_module --with-http_random_index_module --with-http_realip_module --with-http_secure_link_module --with-http_slice_module --with-http_ssl_module --with-http_stub_status_module --with-http_sub_module --with-http_v2_module --with-ipv6 --with-mail --with-mail_ssl_module --with-pcre --with-pcre-jit --with-stream --with-stream_realip_module --with-stream_ssl_module --with-stream_ssl_preread_module  
    


--prefix=/usr/local/Cellar/nginx/1.17.3_1  
然后就可以打开了

    open /usr/local/Cellar/nginx/1.17.3_1  
### nginx一些简单的命令
nginx -s stop # 关闭nginx，直接杀死进程
nginx -s quit # 平缓停止 将当前正在处理的网络请求处理完成之后关闭连接
nginx -s reload # 重新加载配置文件
nginx -t # 检查默认配置文件

### 基本配置与优化
配置文件默认在Nginx程序安装目录下的conf二级目录，主配置文件nginx.conf

    # 使用的用户和组
    user www www;

    # 指定工作衍生进程数
    worker_processes 8;

    # 指定错误日志存放路径
    # 错误日志记录级别可选： [debug | info | notice | warn | error |crit]
    error_log logs/error.log info;

    # 指定pid存放的路径
    pid log/nginx.pid;

    # 指定文件描述符数量
    worker_rlimit_nofile 51200;

    events {
	    # 使用网络I/O模型，linux系统推荐采用epoll模型
	    use epoll;
	
	    # 允许连接数
	    worker_connections 51200;
    }

    http {
	    include		mime.types;
	    defualt_type application/octet-stream;
	
	    # 设置使用字符集
	    # 一般在HTML代码中通过meta标签设置
	    charset gb2312;
	
	    server_names_hash_bucket_size 128;
	    client_header_buffer_size 32k;
	    large_client_header_buffers 4 32k;
	
	    # 设置客户端能够上传文件大小
	    client_max_body_size 8m;
	
	    sendfile on;
	    tcp_nopush on;
	
	    keepalive_timeout 60;
	
	    tcp_nodelay on;
	
	    fastcgi_connect_timeout 300;
	    fastcgi_send_timeout 300;
	    fastcgi_read_timeout 300;
	    fastcgi_buffer_size 64k;
	    fastcgi_buffers 4 64k;
	    fastcgi_busy_buffers_size 128k;
	    fastcgi_temp_file_write_size 128k;
	
	    # 开启gzip
	    gzip on;
	    gzip_min_length 1k;
	    gzip_buffers 4 16k;
	    gzip_http_version 1.1;
	    gzip_comp_level 2;
	    gzip_types text/plain application/x-javascript text/css application/xml;
	    gzip_vary on;
	
	    server {
		    listen 80;
		    server_name www.xxx.com xxx.com;
		    index index.html index.html index.php;
		    root html;
		
		    # limit_conn crawler 20;
		    location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$ {
			    expires 30d;
		    }
		    location ~ .*\.(js|css)?$ {
			    expires 1h;
		    }
		
		    log_format access '$remote_addr - $remote_user [$time_local] "$request" '
			    '$status $body_bytes_send "$http_refrer" '
			    '"$http_user_aget" $http-x-forwarded_for';
		    access_log logs/access.log access;
	    }
    }


#### 虚拟主机配置
虚拟主机使用特殊的软硬件技术，把一台服务器主机分成一台台“虚拟”主机，每台虚拟主机都可以是一个独立网站，可以具有独立域名，同一台主机上的虚拟主机之间是完全独立的。

﻿

    http {
	    # 第一个虚拟主机
	    server {
		    # 监听端口
		    listen 80;
		    # 主机名称
		    server_name aaa.domain.com;
		    # 访问日志存放路径
		    access_log logs/aaadomain.com.access.log combined;
		    location / {
			    # 默认首页文件，从左到右
			    index index.html;
			    # 网站文件存放目录
			    root /data0/htdocs/aaa.domain.com;
		    }
	    }
	
	    # 第二个虚拟主机
	    server {
		    # 监听端口
		    listen 80;
		    # 主机名称
		    server_name aaa.domain.com;
		    # 访问日志存放路径
		    access_log logs/aaadomain.com.access.log combined;
		    location / {
			    # 默认首页文件，从左到右
			    index index.html;
			    # 网站文件存放目录
			    root /data0/htdocs/aaa.domain.com;
		    }
	    }
    }



#### 日志配置与切割
与Nginx日志相关指令主要有两条，一条是log_format，用于设置日志格式；另一条是access_log，用来指定日志文件存放路径、格式和缓存大小。这两条指令可以在Nginx配置文件中的位置可以在http之间也可以在server之间。

• log_format  
`log_format name format [format ...] `

其中 name 表示定义的格式名称，format 表示定义的格式样式。

    log_format mylogformat '$http_x_forwarded_for - $remote_user [$time_local] '
	    '"$request" $status $body_byte_sent '
	    '"$http_referer" "$http_user_agent"';

• access_log  
`access_log path [format [buffer=size | off]] `

其中path表示日志文件存放路径，format 表示使用log_format指令设置的日志格式名称，buffer=size 表示设置内存缓冲区大小，如果不想记录日志，可以关闭日志 access_log off;

    # 使用自定义日志格式
    access_log log/filename.log mylogformat buffer=32k; 
    # Nginx 0.7.4 之后 access_log指令中可以包含变量
    access_log log/$server_name.log mylogformat;

> 如果日志文件中含有变量：  
> 1.Nginx进程设置的用户和组必须由对该路径创建文件的权限。  
> 2.缓冲区将不会被使用。  
> 3.对于每一条日志记录，日志文件将先打开文件，再写入日志，然后马上关闭。为了提高包含变量日志文件存放路径性能，须使用open_log_file_cache指令设置经常呗使用日志文件描述符缓存。  
>  
> open_log_file_cache max=1000 inactive=20s min_uses=2 valid=1m;

• 日志文件切割  

    # 先通过mv命令重命名日志文件 
    mv logs/access.log /logs/20200312.log 
    # 然后发送kill -USER1信号给主进程，让Nginx重新生成一个新的日志文件 
    # kill -USE1 Nginx主进程号 
    kill -USR1 `cat /usr/local/nginx/logs/nginx.pid` # 注意不是USER1 而是USR1 
    # 重新生成新日志文件，也可以借助nginx 发送信号 
    ngixn -s reopen 
    # reopen 内部调用的就是kill命令 
    # 每天定时切割，须借助crontab 然后写一个 shell 脚本 
#### 压缩输出配置
gzip是一种压缩技术。经过gzip压缩后页面大小可以变成原来的30%甚至更小。gzip压缩页面需要浏览器和服务器双方都支持，实际上就是服务端压缩，传到浏览器解压并解析。现在绝大多数浏览器都支持解析gzip过的页面。

	gzip on;
	gzip_min_length 1k;
	gzip_buffers 4 16k;
	gzip_http_version 1.1;
	gzip_comp_level 2;
	gzip_types text/plain application/x-javascript text/css application/xml;
	gzip_vary on;
## 高级应用
### Rewrite 应用
Rewrite主要功能就是实现URL重写。通过Rewrite规则，可以实现规范的URL，根据变量来做URL转向及选择配置。

    server{
	    location / {
		rewrite ^(.*).htmp$ /rewrite.html;
	    }	
    }

访问****.htmp重写到rewrite.html

### 负载均衡和反向代理
#### 负载均衡
    由多台服务器以对称的方式组成一个服务器集合，每台服务器都具有等价的地位，都可以单独对外提供服务而无需其它服务器的辅助。
#### 反向代理
    指以代理服务器来接收Internet上的连接请求，然后将请求转发给网络上的服务器，并将从该服务器得到的结果返回给Internet上请求连接的客户端，此时代理服务器对外就表现为一个服务器。
#### 负载均衡与反向代理配置
    
    # 反向代理配置
    # 直接配置
    server { 
        ... 
        location / { 
            proxy_pass http://xxx.com; 
         } 
         ...
    } 
    # 通过别名配置 
    http { 
    ... 
    upstream 别名 { 
        server ip:端口; 
    } 
    server { 
        ... 
        location / { 
            proxy_pass http://别名; 
        } 
        ... 
    } 
    ... 
    }   
