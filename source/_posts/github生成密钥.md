---
title: github生成密钥
date: 2017-05-24 13:29:27
tags: github
---


``` bash

$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
$ vi .ssh/id_rsa.pub     查看自己的公钥

```