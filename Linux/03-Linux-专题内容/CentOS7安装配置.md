
此文为centos安装后，记录初始化系统需要操作的事项：

## root账号密码修改

```shell
[centos@centos7 ~]# passwd

```

## CentOS界面切换

1. 切换到图形界面

ctrl + alt + f1+(fn)

2. 切换成命令界面

ctrl + alt + f2+(fn)

## Linux配置普通用户具有root权限

```shell
# 1. vim 修改 /etc/sudoers文件

vim /etc/sudoer

# 2. 修改文件

root  ALL=(ALL)
username ALL=(ALL) #username 为需要增加权限的普通用户名。如此修改使用sudo需要输入密码

#username ALL=(ALL) NOPASSWD:ALL #如此每次使用sudo无需输入密码

```

## 参考

[linux语句汇总](https://blog.csdn.net/weixin_43671437/article/details/102817254)