# ubuntu_nginx_gunicorn_django

```linux
#########
# 环境搭建
#########
sudo apt-get update
sudo apt-get upgrade
# 安装django和gunicorn所需要的库和nginx
sudo apt-get install python3-dev python3-pip nginx gcc
# 升级pip和安装django和gunicorn
sudo pip3 install --upgrade pip
sudo pip3 install django gunicorn
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
################################
# 在项目中创建demo_nginx.conf文件
################################
# 定义服务器组
upstream demo {
    server unix:/home/dabolau/demo/demo.sock fail_timeout=0;
}

# 虚拟主机
server {
    # 监听端口
    listen          80;
    # 访问域名
    server_name     demo.com;
    # 编码格式，若网页格式不同，将被自动转码
    charset         utf-8;
    # 虚拟主机访问日志
    access_log      /home/dabolau/demo/logs/access.log;
    error_log      /home/dabolau/demo/logs/error.log;
    # 对url进行匹配
    location / {
        # 重定向
        try_files $uri @proxy_to_demo;
    }
    # 配置静态文件
    location /static/ {
        alias /home/ubuntu/demo/static/;
    }
    # 配置媒体文件
    location /media/ {
        alias /home/ubuntu/demo/media/;
    }
    # 根据用户请求执行不同的应用
    location @proxy_to_demo {
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect off;
        proxy_pass http://demo;
    }
}
```

```linux
###########
# 建立软链接
###########
sudo ln -s /home/dabolau/demo/demo_nginx.conf /etc/nginx/sites-enabled/
```

```linux
#################################
# 检查配置文件正确性和重新加载nginx
#################################
sudo nginx -t
sudo nginx -s reload
```

```linux
###############################
# 在项目中创建demo_gunicorn.conf文件
###############################
import multiprocessing
bind = 'unix:///home/dabolau/demo/demo.sock'
workers = multiprocessing.cpu_count() * 2 + 1
reload = True
daemon = True
```

```linux
##############
# 运行gunicorn
##############
gunicorn -c demo_gunicorn.conf demo.wsgi
```

```linux
#########
# 开机启动
#########
# 创建开机启动文件目录
sudo mkdir /usr/lib/systemd/system
# 创建开机启动文件
sudo nano /usr/lib/systemd/system/demo.service
# 添加以下内容
[Unit]
After=syslog.target network.target remote-fs.target nss-lookup.target
[Service]
# 配置用户
User=dabolau
# 配置目录
WorkingDirectory=/home/dabolau/demo
# 启动命令
ExecStart=/usr/local/bin/gunicorn --bind unix:/home/dabolau/demo/demo.socket de$
Restart=on-failure
[Install]
WantedBy=multi-user.target
# 保存文件
# 启动服务
sudo systemctl start demo.service
# 添加服务开机启动
sudo systemctl enable demo.service
# 取消服务开机启动（不使用就取消服务）
sudo systemctl disable demo.service
# 验证启动（如果有进程表示已经启动）
ps -ef|grep gunicorn
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
http://docs.gunicorn.org/en/stable/deploy.html?highlight=nginx
```
