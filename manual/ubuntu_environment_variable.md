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
