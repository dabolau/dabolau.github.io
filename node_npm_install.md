# node和npm安装步骤

1、下载linux的node压缩包（ https://nodejs.org/en/download ）将压缩包解压到/opt中并重命名为node，在/node/bin中有node和npm执行文件，最后在/usr/local/bin中创建软链接
```linux
sudo ln -s /opt/node/bin/node /usr/local/bin/node
sudo ln -s /opt/node/bin/npm /usr/local/bin/npm
```
2、验证安装是否成功
```linux
node -v
npm -v
```
3、用淘宝cnpm代替npm源
```linux
npm install -g cnpm --registry=https://registry.npm.taobao.org
```
4、将node添加到环境变量中
```linux
export PATH=$PATH:/opt/node/bin
```
