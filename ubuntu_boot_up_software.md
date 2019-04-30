ubuntu_boot_up_software
===

方法一（rc.local）：
---

```linux
sudo nano /etc/rc.local
```
脚本具体格式为下：
```linux
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

exit 0
```

> 注意：要执行的命令必须添加在 exit 0 之前，里面可以直接执行命令或执行shell脚本文件。
