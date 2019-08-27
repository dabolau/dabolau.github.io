ubuntu beautify
===

主题美化
---

1. 安装sudo apt install gnome-tweak-tool和chrome-gnome-shell
```linux
$ sudo apt install gnome-tweak-tool
$ sudo apt install chrome-gnome-shell
```
2. 进入gnome的插件中心安装浏览器扩展
> https://extensions.gnome.org/

3. 进入gnome的插件中心安装User Themes，Dash to Dock
> https://extensions.gnome.org/extension/19/user-themes/
> https://extensions.gnome.org/extension/307/dash-to-dock/

4. 进入gnome-look找到GTK3 themes中下载主题
> https://www.gnome-look.org/p/1241688/

5. 进入用户目录，选择显示隐藏文件，找到.themes文件夹（没有此文件夹就创建一个.themes文件夹）将下载下来的主题放入.themes文件夹中

6. 进入gnome-tweak-tool，外观，主题，应用程序中选择刚刚放入.themes的主题名称

图标美化
---

1. 进入gnome-look找到Icon Themes中下载图标
> https://www.gnome-look.org/p/1218021/

2. 进入用户目录，选择显示隐藏文件，找到.icons文件夹（没有此文件夹就创建一个.icons文件夹）将下载下来的图标放入.icons文件夹中

3. 进入gnome-tweak-tool，外观，主题，图标中选择刚刚放入.icons文件夹的图标名称

控制板美化
---

1. 进入gnome-look找到Gnome Shell Themes中下载控制板
> https://www.gnome-look.org/p/1213208/
> https://www.gnome-look.org/p/1215571/

2. 进入用户目录，选择显示隐藏文件，找到.themes文件夹（没有此文件夹就创建一个.themes文件夹）将下载下来的控制板放入.themes文件夹中

3. 进入gnome-tweak-tool，外观，主题，shell中选择刚刚放入.themes文件夹的控制板名称，扩展，Dash to dock，选择设置符号，勾选所有显示器上都显示和屏幕中的位置选择底部

4. 进入下载下来的控制板文件夹中的全部字体放入~/.local/share/fonts中（没有fonts文件夹就创建fonts文件夹）

登录界面美化
---

1. 进入gnome-look找到GDM Themes中下载登录界面
> https://www.gnome-look.org/p/1207015/

2. 备份系统原始ubuntu.css样式
```linux
$ sudo cp /usr/share/gnome-shell/theme/ubuntu.css /usr/share/gnome-shell/theme/ubuntu.css.bak
```

3. 将下载下来的登录界面文件夹中的样式high_ubunterra.css重命名为ubuntu.css后拷贝到/usr/share/gnome-shell/theme/中替换原有ubuntu.css文件
```linux
$ sudo mv high_ubunterra.css ubuntu.css
$ sudo cp ubuntu.css /usr/share/gnome-shell/theme/
```

4. 将下载下来的登录界面文件夹中SetAsWallpaper拷贝到~/.local/share/nautilus/scripts/ *拷贝到此目录后可以修改SetAsWallpaper文件名为设置墙纸*
```linux
$ cp SetAsWallpaper ~/.local/share/nautilus/scripts/
```

5. 设置/usr/share/backgrounds/为最高权限
```linux
$ sudo chmod 777 /usr/share/backgrounds/
```

登录背景和壁纸美化
---

1. 到图片文件夹中选择中你喜欢的图片右键点击脚本，SetAsWallpaper（设置墙纸）设置桌面的背景图片

重新启动感受美化的主题吧


