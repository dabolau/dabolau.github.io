# ubuntu_boot_up_software

### 方法一（/etc/rc.local）：

> 创建并编辑/etc/rc.local文件

```bash
sudo nano /etc/rc.local
```
> 配置如下：

```bash
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.

###
# 开机执行格式
# /bin/su - 用户名 -c "要执行的命令"
###

/bin/su - dabolau -c "nohup python3 /home/dabolau/django/jobproject/manage.py runserver 0:8001 &"

###
# 注意：要执行的命令必须添加在 exit 0 之前。
###
exit 0
```

> 给/etc/rc.local文件添加权限

```bash
sudo chmod a=rwx /etc/rc.local
```

> 重启系统，验证开机启动是否设置成功



### 方法二（systemd）

Systemd 是 Linux 系统工具，用来启动守护进程，已成为大多数发行版的标准配置。

而 systemctl 是 Systemd 的主命令，用于管理系统。

> 参考资料

```bash
# 阮一峰的 Systemd 入门教程
http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html
```

> 创建并编辑服务文件md.service

```bash
# 服务目录
cd /etc/systemd/system/
# 创建并编辑服务文件
sudo nano md.service
```

> 配置如下：

```bash
[Unit]
# 单元描述
Description=md
# 在什么服务启动之后再执行本程序
# After=mysql.service

[Service]
Type=simple
# 程序目录
WorkingDirectory=/home/dabolau/md
# 启动命令
ExecStart=/home/dabolau/md/md
# 重启条件
Restart=alway
# 几秒后重启
RestartSec=5

[Install]
WantedBy=multi-user.target
```

> 常用命令（systemd）

```bash
# 重新加载服务
sudo systemctl daemon-reload
# 启动服务
sudo systemctl start md.service
# 停止服务
sudo systemctl stop md.service
# 重启服务
sudo systemctl restart md.service
# 查看服务
sudo systemctl status md.service
# 添加到开机启动项中
sudo systemctl enable md.service
# 从开机启动项中移除
sudo systemctl disable md.service
```

> 重启系统，验证开机启动是否设置成功