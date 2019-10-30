# sftp_config

1. 安装软件

   ```bash
   sudo apt install openssh-server
   ```

2. 配置sftp指定用户目录

   ```bash
   # 创建用户，目录，密码，其中yourname改为自己的用户名，这时可以ssh和sftp登录了
   sudo adduser yourname
   # 备份sshd_config
   sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
   # 配置sshd_config
   sudo nano /etc/ssh/sshd_config
   ```

3. 配置sshd_config文件

   ```bash
   # 要屏蔽的内容
   # Subsystem sftp /usr/lib/openssh/sftp-server
   
   # 在文件的最末尾输入下面内容，其中yourname改为自己的用户名，yourname需要是root权限
   Subsystem sftp internal-sftp
   Match user yourname
   ChrootDirectory /home/yourname/
   ForceCommand internal-sftp
   ```

4. 重新启动ssh服务

   ```bash
   sudo service ssh restart
   ```

5. 测试登录

   ```bash
   sftp yourname@ip
   ```

   

