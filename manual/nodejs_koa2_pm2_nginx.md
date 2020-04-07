# 服务开发和服务器部署（nodejs_koa2_pm2_nginx）

1. 下载并安装nodejs
```
https://nodejs.org/
```

2. 安装并使用koa2
```
http://koajs.com/
```
```
$ mkdir demoproject && cd demoproject && npm init -y
$ npm install koa
$ touch index.js
```

index.js:
```
const Koa = require('koa');
const app = new Koa();

app.use(async ctx => {
  ctx.body = 'Hello World';
});

app.listen(3000);
```

启动服务
```
$ touch index.js
```

3. 安装并使用pm2
```
https://pm2.keymetrics.io/
```
```
$ npm install -g pm2
```

启动服务
```
$ pm2 start index.js -i max -n demoproject
```

重启服务
```
$ pm2 restart index.js
$ pm2 restart all
```

查看服务状态
```
$ pm2 list
```

查看服务消耗资源情况
```
$ pm2 monit
```

停止服务
```
$ pm2 stop index.js
$ pm2 stop all
```

删除服务
```
$ pm2 delete index.js
$ pm2 delete all
```

4. 安装并使用nginx
```
http://nginx.org/
```
```
$ sudo apt install nginx
$ touch demoproject_nginx.conf
```

demoproject_nginx.conf:
```
# 定义服务器组，实现负载均衡
upstream demoproject {
    server 127.0.0.1:3000;
}

# 虚拟主机
server {
    # 监听端口
    listen 80;
    # 访问域名
    server_name demoproject.com;
    # 编码格式，若网页格式不同，将被自动转码
    charset utf-8;
    # 对url进行匹配
    location / {
        proxy_pass http://demoproject;
    }
}
```

建立软链接
```
$ sudo ln -s /home/dabolau/demoproject/demoproject_nginx.conf /etc/nginx/sites-enabled/
```

检查配置文件正确性和重新加载nginx
```
$ sudo nginx -t
$ sudo nginx -s reload
```