# letsencrypt_certbot

0. 官方网站
```linux
https://certbot.eff.org/
```

1. 添加Certbot PPA
```linux
sudo apt-get update
sudo apt-get install software-properties-common
sudo add-apt-repository universe
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
```

2. 安装Certbot
```linux
sudo apt-get install certbot python-certbot-nginx
```

3. 选择您想如何运行Certbot
+ 获取并安装您的证书
```linux
sudo certbot --nginx
```
+ 只获取证书
```linux
sudo certbot certonly --nginx
```

4. 测试自动续订证书
+ 系统上的Certbot带有计时器会自动更新证书，您可以通过运行以下命令来测试证书的自动续订
```linux
sudo certbot renew --dry-run
```


