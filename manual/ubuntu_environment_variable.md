# 环境变量

### 环境变量的三种方法

1. 临时设置
```linux
export PATH="$PATH:/home/dabolau/snap"
```

2. 当前用户的全局设置
+ 打开文件~/.bashrc或者~/.profile
```linux
$ nano .bashrc
```
+ 在末尾添加行：
```linux
export PATH="$PATH:/home/dabolau/snap"
```
+ 使环境变量生效
```linux
$ source .bashrc
```

3. 所有用户的全局设置
+ 打开文件/etc/profile
```linux
$ nano /etc/profile
```
+ 在末尾添加行：
```linux
export PATH="$PATH:/home/dabolau/snap"
```
+ 使环境变量生效
```linux
$ source /etc/profile
```

4. 环境变量配置
```linux
###
# nodejs
###
export PATH="$PATH:$HOME/snap/node/bin"

###
# golang
###
export GOROOT="$HOME/snap/go"
export GOPATH="$HOME/snap/space/go"
export PATH="$PATH:$GOROOT/bin"

###
# dart
###
export PATH="$PATH:$HOME/snap/flutter/bin/cache/dart-sdk/bin"

###
# dart package
###
export PATH="$PATH:$HOME/.pub-cache/bin"

###
# Flutter
###
export PATH="$PATH:$HOME/snap/flutter/bin"
export PUB_HOSTED_URL="https://pub.flutter-io.cn"
export FLUTTER_STORAGE_BASE_URL="https://storage.flutter-io.cn"

###
# Android SDK
###
export ANDROID_HOME="$HOME/snap/android/sdk"
export PATH="$PATH:$ANDROID_HOME/tools"
export PATH="$PATH:$ANDROID_HOME/platform-tools"

###
# 管理员权限找不到命令时使用（可选）
###
alias sudo="sudo env PATH=$PATH"
```
