# shadowsocks
## install

[网站](https://shadowsocks.org/en/download/clients.html)
[github](https://github.com/shadowsocks/shadowsocks-qt5/wiki)

上面已经有详细的安装地址了
```
sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install shadowsocks-qt5
```
然后编辑。。。但是发现重启之后才能上网。。。

## configure
配置PAC 模式

* 打开系统设置 -》网络 -》网络代理
* 选择自动
然后URL 为对应的pac文件地址
` /home/xxxuser/ss/ss.pac`
