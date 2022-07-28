
Nginx (engine x) 是一款轻量级的Web 服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器，在BSD-like 协议下发行。其特点是占有内存少，并发能力强.

## Nginx 安装

```shell
yum install -y nginx
```

## Nginx 配置

修改/etc/nginx/nginx.conf文件：

1. 修改启动者。 在nginx安装时，会新增nginx用户、组，故在conf文件下配置启动为root；

2. 修改端口号。默认80端口，修改为8081

3. 修改文件路径。 默认文件路径：/usr/share/nginx/html

```shell
# 修改启动者
user root;

# 修改端口号：
server{
    listen 9999;
    listen [::]:9999;

# 修改路径
    root /home/paul/...
    location / {
        index index.html;
    }
}

```

## Nginx:查看、启动、重启

```shell
# 查看
systemctl status nginx

# 启动
systemctl start nginx

# 重启
systemctl restart nginx

```

## Nginx:查看日志

nginx 的日志文件在 /var/log/nginx 中。

## 防火墙：开放端口

```shell

# 查看监听端口
netstat -lnpt

# 查看防火墙已经开放的端口
firewall-cmd --zone=public --list-ports

# 开放端口
firewall-cmd --zone=public --add-port=9999/tcp --permanent

# 关闭端口
firewall-cmd --zone=public --remove-port=8081/tcp --permanent

# 重新加载防火钱
firewall-cmd --reload

```

## 遇到的问题

1. Permission denied

通过查看日志信息 /var/log/nginx/error 发现报 Permission denied。

解决方案：
a. 修改/etc/nginx/nginx.conf中user信息，改为root
b. 关闭了SELinux 

```shell
setenfore 0
```

2. 拒绝访问问题

防火墙未开通端口号。
