# 环境变量

### 环境变量的三种方法

1. 临时设置
```linux
export PATH="$PATH:/opt/node/bin"
```

2. 当前用户的全局设置
+ 打开文件~/.profile
```linux
$ nano .profile
```
+ 在末尾添加行：
```linux
export PATH="$PATH:/opt/node/bin"
```
+ 使环境变量生效
```linux
$ source .profile
```

3. 所有用户的全局设置
+ 打开文件/etc/profile
```linux
$ nano /etc/profile
```
+ 在末尾添加行：
```linux
export PATH="$PATH:/opt/node/bin"
```
+ 使环境变量生效
```linux
$ source /etc/profile
```

4. Flutter的环境变量配置
```linux
###
# dart
###
export PATH="$PATH:/opt/flutter/bin/cache/dart-sdk/bin"

###
# Flutter
###
export PATH="$PATH:/opt/flutter/bin"
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn

###
# Android SDK
###
export ANDROID_HOME=/opt/android/sdk
export PATH=${PATH}:${ANDROID_HOME}/tools
export PATH=${PATH}:${ANDROID_HOME}/platform-tools

###
# 管理员权限找不到命令时使用
###
alias sudo="sudo env PATH=$PATH"
```