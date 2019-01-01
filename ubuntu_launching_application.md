ubuntu launching application
===

1. 在桌面文件夹中创建一个datagrip.desktop的文件，其中datagrip为你的应用程序的名称
```linux
$ touch datagrip.desktop
```

2. 在文件中写入如下固定格式的内容
```linux
[Desktop Entry]
Name=DataGrip
Comment=DataGrip for Databese
Exec=/home/dabolau/Documents/DataGrip/bin/datagrip.sh
Icon=/home/dabolau/Documents/DataGrip/bin/datagrip.png
Terminal=false
Type=Application
```

> 每个项目的具体说明

项目|说明
-|-
[Desktop Entry]|#应用程序桌面入口
Name=DataGrip|#应用程序名称
Comment=DataGrip for Databese|#应用程序说明
Exec=/home/dabolau/Documents/DataGrip/bin/datagrip.sh|#应用程序的执行文件，请使用绝对路径
Icon=/home/dabolau/Documents/DataGrip/bin/datagrip.png|#应用程序的图标
Terminal=false|#应用程序启动时是否显示终端
Type=Application|#应用程序的类型

3. 在桌面文件夹中打开终端输入以下内容
```linux
$ sudo chmod 777 datagrip.desktop
```

4. 双击运行datagrip.desktop程序

5. 把启动应用程序放在起动器中在桌面文件夹中打开终端输入以下内容
```linux
$ sudo cp datagrip.desktop /usr/share/applications/
```
