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
