# github

配置用户名和电子邮件
```
$ git config --global user.name "username"
$ git config --global user.email "email"
```

生成新的SSH密钥
```
ssh-keygen -t rsa -C "email"
```

在后台启动SSH代理
```
eval "$(ssh-agent -s)"
```

加载密钥到SSH代理中
```
ssh-add
```

测试您的SSH连接（测试前需要把～/.ssh/id_rsa.pub文件里的SSH密钥复制到github网站）
```
ssh -T git@github.com
```

命令创建新的存储库
```
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:dabolau/demo.git
git push -u origin master
```

命令推送现有存储库
```
git remote add origin git@github.com:dabolau/demo.git
git push -u origin master
```
