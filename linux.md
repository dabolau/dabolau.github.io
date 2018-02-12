使用dd命令制作linux系统启动盘
===
```linux
#查出u盘名称及路径（/dev/sdc1）
df -h
#卸载已挂载的u盘
umount /dev/sdc1
#制作u盘启动盘，if=为系统的iso文件，of=为u盘路径
sudo dd bs=4M if=/home/dabolau/iso/ubuntu-17.10-desktop-amd64.iso of=/dev/sdc1   
```

