# ubuntu_nginx_uwsgi_django

```linux
#########
# 环境搭建
#########
sudo apt-get update
sudo apt-get upgrade
# 安装django和uwsgi所需要的库和nginx
sudo apt-get install python-dev python-pip nginx gcc
# 升级pip和安装django和uwsgi
sudo pip install --upgrade pip
sudo pip install django uwsgi
```

```linux
###############
# 修改用户和组权限
###############
sudo nano /etc/nginx/nginx.conf
# 将user www-data;修改为user dabolau; （重要）
user dabolau;
```

```linux
###########################
# 在项目中创建uwsgi_params文件
###########################
uwsgi_param  QUERY_STRING       $query_string;
uwsgi_param  REQUEST_METHOD     $request_method;
uwsgi_param  CONTENT_TYPE       $content_type;
uwsgi_param  CONTENT_LENGTH     $content_length;

uwsgi_param  REQUEST_URI        $request_uri;
uwsgi_param  PATH_INFO          $document_uri;
uwsgi_param  DOCUMENT_ROOT      $document_root;
uwsgi_param  SERVER_PROTOCOL    $server_protocol;
uwsgi_param  REQUEST_SCHEME     $scheme;
uwsgi_param  HTTPS              $https if_not_empty;

uwsgi_param  REMOTE_ADDR        $remote_addr;
uwsgi_param  REMOTE_PORT        $remote_port;
uwsgi_param  SERVER_PORT        $server_port;
uwsgi_param  SERVER_NAME        $server_name;
```

```linux
################################
# 在项目中创建hanhan_nginx.conf文件
################################
# the upstream component nginx needs to connect to
upstream hanhan {
    server unix:///home/dabolau/hanhan/hanhan.sock; # for a file socket
    # server 127.0.0.1:8001; # for a web port socket (we'll use this first)
}

# configuration of the server
server {
    # the port your site will be served on
    listen      80;
    # the domain name it will serve for
    server_name hanhan.com; # substitute your machine's IP address or FQDN
    charset     utf-8;

    # max upload size
    client_max_body_size 64M;   # adjust to taste

    # Django media
    location /media  {
        alias /home/dabolau/hanhan/media;  # your Django project's media files - amend as required
    }

    location /static {
        alias /home/dabolau/hanhan/static; # your Django project's static files - amend as required
    }

    # Finally, send all non-media requests to the Django server.
    location / {
        uwsgi_pass  hanhan;
        include     /home/dabolau/hanhan/uwsgi_params; # the uwsgi_params file you installed
    }
}
```

```linux
###########
# 建立软链接
###########
sudo ln -s /home/dabolau/hanhan/hanhan_nginx.conf /etc/nginx/sites-enabled/
```

```linux
###############################
# 在项目中创建hanhan_uwsgi.ini文件
###############################
# hanhan_uwsgi.ini file
[uwsgi]

# Django-related settings
# the base directory (full path)
chdir           = /home/dabolau/hanhan
# Django's wsgi file
module          = hanhan.wsgi
# the virtualenv (full path)
# home          = /path/to/virtualenv

# process-related settings
# master
master          = true
# maximum number of worker processes
processes       = 4
# the socket (use the full path to be safe
socket          = /home/dabolau/hanhan/hanhan.sock
# uWSGI Stat Server
stats           = /home/dabolau/hanhan/stats.sock
# ... with appropriate permissions - may be needed
# chmod-socket    = 664
# clear environment on exit
vacuum          = true
```

```linux
###########
# 运行UWSGI
###########
uwsgi --ini hanhan_uwsgi.ini
```

```linux
#########
# 开机启动
#########
# 进入/etc/rc.local文件
sudo nano /etc/rc.local
# 在exit 0前输入以下内容
/usr/local/bin/uwsgi /home/dabolau/hanhan/hanhan_uwsgi.ini
```

```linux
###########
# 多网站部署
###########
# 完成上述各步骤后将各网站目录中的配置文件软链接即可
ln -s /home/dabolau/mystie/mysite_nginx.conf /etc/nginx/sites-enabled/
```

```linux
###############
# 详细配置参考网站
###############
https://uwsgi.readthedocs.io/en/latest/tutorials/Django_and_nginx.html
```
