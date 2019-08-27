# nginx命令及配置详解

## 命令参数详解

```linux
# 安装nginx
sudo apt install nginx
```

```linux
# 查看nginx进程
ps -ef|grep nginx
```

```linux
# 启动nginx
sudo nginx
# 停止nginx
sudo nginx -s stop
# 退出nginx
sudo nginx -s quit
# 重启nginx
sudo nginx -s reopen
# 重新加载配置文件
sudo nginx -s reload
```

```linux
# 查看帮助信息
sudo nginx -h
```

```linux
# 查看帮助详情
nginx [-?hvVtTq] [-s signal] [-c filename] [-p prefix] [-g directives]

Options:
  -?,-h         : this help
  -v            : show version and exit
  -V            : show version and configure options then exit
  -t            : test configuration and exit
  -T            : test configuration, dump it and exit
  -q            : suppress non-error messages during configuration testing
  -s signal     : send signal to a master process: stop, quit, reopen, reload
  -p prefix     : set prefix path (default: /usr/share/nginx/)
  -c filename   : set configuration file (default: /etc/nginx/nginx.conf)
  -g directives : set global directives out of configuration file
```

```linux
# 查看帮助中文详情
nginx [-?hvVtTq] [-s signal] [-c filename] [-p prefix] [-g directives]

Options:
  -?,-h         : 打开帮助信息
  -v            : 显示版本信息并退出
  -V            : 显示版本和配置选项信息，然后退出
  -t            : 检测配置文件是否有语法错误并退出
  -T            : 检测配置文件是否有语法错误显示配置文件，然后退出
  -q            : 在检测配置文件期间屏蔽非错误信息
  -s signal     : 给一个 nginx 主进程发送信号：stop（停止）, quit（退出）, reopen（重启）, reload（重新加载配置文件）
  -p prefix     : 设置前缀路径（默认路径: /usr/share/nginx/）
  -c filename   : 设置配置文件（默认路径: /etc/nginx/nginx.conf）
  -g directives : 设置配置文件外的全局指令
```

## 配置文件详解

### 虚拟主机基本配置（HTTP）

```linux
# 虚拟主机
server {
  # 监听端口
  listen 80;
  # 访问域名
  server_name demo.com;
  # 编码格式，若网页格式不同，将被自动转码
  charset utf-8;
  # 虚拟主机访问日志
  access_log /home/dabolau/demo/log/access.log;
  error_log /home/dabolau/demo/log/error.log;
  # 对url进行匹配
  location / {
    # 访问路径，可以是相对路径也可以是绝对路径
    root /home/dabolau/demo;
    # 首页文件，按先后顺序匹配
    index index.html index.htm;
  }
}
```

### 虚拟主机基本配置（跳转）

```linux
# 虚拟主机
server {
  # 监听端口
  listen 80;
  # 访问域名
  server_name www.demo.com;
  # 跳转（301）
  return 301 http://demo.com$request_uri;
}
```

### 虚拟主机基本配置（HTTPS）

```linux
# 虚拟主机
server {
  # 监听端口
  listen 443 ssl;
  # 访问域名
  server_name demo.com;
  # 证书配置
  ssl_certificate /etc/letsencrypt/live/demo.com/fullchain.pem;
  ssl_certificate_key /etc/letsencrypt/live/demo.com/privkey.pem;
  # 编码格式，若网页格式不同，将被自动转码
  charset utf-8;
  # 虚拟主机访问日志
  access_log /home/dabolau/demo/log/access.log;
  error_log /home/dabolau/demo/log/error.log;
  # 对url进行匹配
  location / {
    # 访问路径，可以是相对路径也可以是绝对路径
    root /home/dabolau/demo;
    # 首页文件，按先后顺序匹配
    index index.html index.htm;
  }
}
```
