# 在ubuntu中编译安装nginx和nginx_rmtp_module模块

1. 更新系统
```linux
sudo apt update
sudo apt upgrade
```

2. 安装依赖包和工具包
```linux
sudo apt install make gcc libpcre3 libpcre3-dev libssl-dev zlib1g-dev
sudo apt install git curl wget
```

3. 下载nginx和nginx_rtmp_modue
```linux
wget http://nginx.org/download/nginx-1.14.2.tar.gz
git clone https://github.com/arut/nginx-rtmp-module.git
```

4. 编译安装nginx和nginx_rtmp_modle
```linux
tar -zxvf nginx-1.14.2.tar.gz
cd nginx-1.14.2
./configure --add-module=/path/to/nginx-rtmp-module --with-http_ssl_module
sudo make && sudo make install
```

5. 查看安装情况
```linux
sudo ln -s /usr/local/nginx/sbin/nginx /usr/bin/nginx
nginx -V
```

6. 查看启动情况
```linux
sudo nginx -s stop
sudo nginx
curl htt://127.0.0.1
```

7. 配置模块信息修改nginx.conf（默认路径为/usr/local/nginx/conf/nginx.conf），注意需要在http{}外添加
```linux
rtmp {
    server {
        listen 1935;
        application rtmplive {
            live on;
            record off;
        }
        application vod {
        play /opt/video/vod;
        }
    }
}
```

8. 完整的配置文件如下
```linux
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

        location /stat {     #第1处添加的location字段。
            rtmp_stat all;
            rtmp_stat_stylesheet stat.xsl;
        }

        location /stat.xsl { #第2处添加的location字段。
           root /usr/local/nginx/nginx-rtmp-module/;
        }

        location / {
            root   html;
            index  index.html index.htm;
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
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}

rtmp {
    server {
        listen 1935;
        application rtmplive {
            live on;
            record off;
        }
        application vod {
        play /opt/video/vod;
        }
    }
}
```

9. 重启nginx，用浏览器打开 http://127.0.0.1/stat ，如果看到页面内容说明配置成功
```linux
sudo nginx -s reload
curl http://127.0.0.1/stat
```

10. OBS Studio推流，VLC拉流
```linux
# OBS推流，进入软件，设置，流，服务选择自定义，服务器输入rtmp://localhost/rtmplive，应用，确定，开始推流
# VLC拉流，进入软件，媒体，打开网络串流，网络中输入rtmp://localhost/rtmplive，播放
```
