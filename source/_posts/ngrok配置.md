---
title: ngrok的配置
date: 2017-06-13 16:17:18
tags: ['ngrok','apache','查询端口号']
---
[ngrok官网](http://ngrok.2bdata.com)

``` bash
//修改httpd.conf的指向路径（可修改）  Finder →️/etc/apache2

Listen 81
DocumentRoot "/Library/WebServer/Documents"

// apache的开启和关闭
sudo apachectl -k start    开启apache
sudo apachectl -k restart   重新启动apache
// 查询端口号
lsof -iTCP:80 | grep LISTEN          If you are going to find the process listening on 80 port:
sudo lsof -i -P | grep -i "listen"       Mac下使用这个命令即可查看所有占用的端口
// ngrok 的使用
$ cd Applications/ngrok
~/Applications/ngrok$ ls
ngrok     ngrok.cfg ngrok.txt
/Applications/ngrok$ ./ngrok -config=./ngrok.cfg -subdomain=qq467527309 80
```