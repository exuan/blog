title: centos 搭建 jetbrains-license-server
date: 2018-03-06 21:10:20
categories: jetbrains
tags: [jetbrains, License-Server]
---

>   步骤简单 ，直接走就可以
>   lz 的服务器是centos

## 金玉良言
如果您不差钱，请购买正版https://www.jetbrains.com/idea/buy

## 画重点
 account.jetbrains.com 一定要加到你的本地host里
```bash
0.0.0.0 account.jetbrains.com
```

## 安装
下载 [IntelliJ IDEA License Server v1.6](http://blog.lanyus.com/archives/326.html)  (lz 现在用是v1.6，新版本还请及时关注 [lanyus](blog.lanyus.com))

解压到 某个目录下(任意即可), IntelliJIDEALicenseServer 目录下涵盖了很多平台(mac linux windows)。lz的服务器是x86_64 GNU/Linux，so 给IntelliJIDEALicenseServer_linux_amd64 赋可执行权限
```bash
$ chmod +x IntelliJIDEALicenseServer_linux_amd64
```

<!--more--> 

运行
```bash
$ ./IntelliJIDEALicenseServer_linux_amd64
2018/03/06 21:12:20 *************************************************************
2018/03/06 21:12:20 ** IntelliJ IDEA License Server                            **
2018/03/06 21:12:20 ** by: ilanyu                                              **
2018/03/06 21:12:20 ** http://www.lanyus.com/                                  **
2018/03/06 21:12:20 ** Alipay donation: lanyu19950316@gmail.com                **
2018/03/06 21:12:20 ** Please support genuine!!!                               **
2018/03/06 21:12:20 ** listen on 0.0.0.0:1027...                               **
2018/03/06 21:12:20 ** You can use http://127.0.0.1:1027 as license server     **
2018/03/06 21:12:20 *************************************************************
```

nginx

```bash
#vim /usr/local/nginx/conf/nginx.conf
server {
    listen 80;
    server_name jetbrains.yourdomain.com;
    root /usr/local/nginx/html;

    location / {
        proxy_pass http://127.0.0.1:1027;
        proxy_redirect off;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;

        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
    access_log /dev/null; #access_log end
    error_log /dev/null; #error_log end
}
```

systemd

```bash
# vim /etc/systemd/system/intellij.service
[Unit]
Description= IntelliJIDEALicenseServe Service
After=network.target

[Service]
ExecStart=/IntelliJIDEALicenseServer_linux_amd64
PrivateTmp=true

[Install]
WantedBy=default.target

# systemctl daemon-reload # 重载
# systemctl start intellij # 启动
# systemctl enable intellij # 开机启动
# systemctl disable intellij # 撤销开机启动
```

IntelliJIDEALicenseServer 帮助

```bash
 ./IntelliJIDEALicenseServer_linux_amd64 -h
 -l string 绑定的host，基本默认
        bind on host (default "0.0.0.0")
  -p int 监听端口，建议改下
        port (default 1027)
  -prolongationPeriod string 过期时间
        prolongationPeriod (default "607875500")
  -u string 当未设置-u参数，且计算机用户名为^[a-zA-Z0-9]+$时，使用计算机用户名作为idea用户名
        username (default "ilanyu")
```