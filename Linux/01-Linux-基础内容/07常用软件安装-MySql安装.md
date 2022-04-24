
# 常用软件安装-MySql安装

常用软件安装，将在CentOS7环境逐步完成，anaconda、python（配置jupyterlab）、redis、mysql、nginx、mongodb安装，是之前各个章节知识的实践。主要目标：

- 1、熟悉Linux的命令；
- 2、熟悉Linux下目录结构；
- 3、 安装思维导图.

<img src="./res/070201.png" alt="0701" style="zoom:50%;" />

# 1. MySQL数据库

MySQL所使用的 SQL 语言是用于访问数据库的最常用标准化语言。MySQL 软件采用了双授权政策，分为社区版和商业版，由于其体积小、速度快、总体拥有成本低，一般中小型网站的开发都选择 MySQL 作为网站数据库。

# 2. MySQL数据库的特点

- MySQL数据库是用C和C++语言编写的，以保证源码的可移植性
- 支持多个操作系统例如：Windows、Linux、Mac OS等等
- 支持多线程，可以充分的利用CPU资源
- 为多种编程语言提供API，包括C语言，Java，PHP。Python语言等
- MySQL优化了SQL算法，有效的提高了查询速度
- MySQL开放源代码且无版权制约，自主性强、使用成本低。
- MySQL历史悠久、社区及用户非常活跃，遇到问题，可以很快获取到帮助。

# 3. 二进制包安装

## .1 安装

- 下载

  ```shell
  wget https://downloads.mysql.com/archives/get/p/23/file/mysql-5.7.36-linux-glibc2.12-x86_64.tar
  
  yum search libaio
  
  yum install libaio
  ```

​	[下载MYSQL GLIBC版本](https://downloads.mysql.com/archives/community/)

- 解压并移至指定目录

  ```shell
  tar -xvf mysql-5.7.36-linux-glibc2.12-x86_64.tar.gz
  
  mv mysql-5.7.36-linux-glibc2.12-x86_64 /usr/local/mysql
  
  cd /usr/local/mysql
  ```

- 创建mysql用户和用户组

  ```shell
  useradd -r -s /sbin/nologin mysql
  ```

   

- 创建mysql-files文件夹，并修改权限

  ```shell
  mkdir mysql-files
  
  chown mysql:mysql mysql-files
  
  chmod 750 mysql-files
  ```

- 清除系统中原有/etc/my.cnf

  ```shell
  rm -rf /etc/my.cnf
  ```

- 初始化数据库

  ```shell
  bin/mysqld --initialize --user=mysql --basedir=/usr/local/mysql
  ```

  > 初始化成功后，在/etc/local/mysql下生成文件夹data；
  >
  > 初始化结束后，系统将为root用户生存随机密码；

- 设置安全加密链接SSL

  ```shell
  bin/mysql_ssl_rsa_setup --datadir=/usr/local/mysql/data
  ```

- 配置/etc/init.d

  ```shell
  cp support-files/mysql.server /etc/init.d/mysql
  ```

- 启动mysql

  ```shell
  service mysql start
  ```

## .2 更改数据库管理员密码

```
bin/mysqladmin -uroot password 'passw0rd' -p
```

## .3 配置环境变量

```shell
echo $PATH

echo 'export PATH=$PATH:/usr/local/mysql/bin' >> /etc/profile

source /etc/profile
```

## .4 手工定义mysql配置文件

```shell
vim /usr/local/mysql/my.cnf

service mysql restart
```

## .5 设置远程访问数据库

- 网络设置

  - 查看mysql端口号

    ```shell
    netstat -anpt | grep mysqld
    ```

  - 查看防火墙状态

    ```shell
    systemctl status firewalld		 			#查看firewall防火墙状态
    firewall-cmd --list-ports					#查看firewall防火墙开放端口
    systemctl start firewalld.service			#打开firewall防火墙
    systemctl stop firewalld.service			#关闭firewall防火墙
    firewall -cmd --reload						#重启firewal防火墙
    systemctl disable firewalld.service			#禁止firewall开机启动  
    
    #开放firewall防火墙端口，需重启防火墙生效
    firewall-cmd --zone=public --add-port=80/tcp --permanent 
    #删除端口
    firewall-cmd --zone=public --remove-port=80/tcp --permanent 
    
    命令含义:
    –zone #作用域
    –add-port=80/tcp #添加端口，格式为：端口/通讯协议
    –permanent #永久生效，没有此参数重启后失效
    ```

    > firewall和iptable都是Linux的防火墙，firewall调用了iptable的command去执行内核的netfilter，也就是底层还是使用 iptables 对内核命令动态通信包过滤，firewall是Centos7里的新防火墙命令，相当于iptables 的孩子。

- mysql账号授权

  ​	用户（root）使用密码（passw0rd）从任何主机连接到mysql服务器的话。

  ```sql
  GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'passw0rd' WITH GRANT OPTION;
  
  FLUSH PRIVILEGES;
  ```

# 4. 参考资料

  - [官网安装MySQL binary的命令顺序:](https://dev.mysql.com/doc/refman/5.7/en/binary-installation.html)

    > $> groupadd mysql 
    >
    > $> useradd -r -g mysql -s /bin/false mysql 
    >
    > $> cd /usr/local $> tar zxvf */path/to/mysql-VERSION-OS*.tar.gz 
    >
    > $> ln -s *full-path-to-mysql-VERSION-OS* mysql 
    >
    > $> cd mysql 
    >
    > $> mkdir mysql-files 
    >
    > $> chown mysql:mysql mysql-files 
    >
    > $> chmod 750 mysql-files 
    >
    > $> bin/mysqld --initialize --user=mysql 
    >
    > $> bin/mysql_ssl_rsa_setup 
    >
    > $> bin/mysqld_safe --user=mysql & 
    >
    > -# Next command is optional 
    >
    > $> cp support-files/mysql.server /etc/init.d/mysql.server

  - [官方文档-MySQL on Unix/Linux Using Generic Binaries](https://dev.mysql.com/doc/refman/5.7/en/binary-installation.html)

  - [Linux防火墙、查看端口等](https://blog.csdn.net/weixin_42188441/article/details/116720925)

  - [远程访问数据库](https://zhuanlan.zhihu.com/p/51848402)