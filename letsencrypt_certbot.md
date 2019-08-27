# letsencrypt_certbot

```linux
###
# 安装certbot
###
sudo apt-get update
sudo apt-get install software-properties-common
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install python-certbot-nginx 
```

```linux
###
# 生成证书
###
# 证书存放目录/etc/letsencrypt/live/demo.com/
sudo certbot --nginx certonly -m demo@demo.com -d demo.com -d www.demo.com
```

```linux
###
# 续期证书
###
# 证书时效为90天，在快到期的30天内可以续期
sudo certbot renew
# 测试命令
sudo certbot renew --dry-run
```

```linux
###
# 官方网站
###
https://certbot.eff.org/
```
