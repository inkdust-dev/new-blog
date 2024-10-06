---
abbrlink: ''
categories:
- - 技术教程
index_img: https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/blog-image/wordpress-deploy.png
date: '2023-07-19T20:07:30+08:00'
tags:
- Docker
- Oneinstack
- WordPress
title: 以多种方式部署WordPress博客
updated: '2024-08-07T22:32:10.443+08:00'
---
今天来总结一下几种WordPress博客的部署方式。不说废话，直接开始!

## 部署到服务器/VPS

这里有几种常见的部署方式。

### 使用Oneinstack部署

首先确保服务器没有安装任何PHP和数据库环境。

然后使用一键安装命令安装 `Oneinstack`。

```shell
sudo wget -c http://mirrors.linuxeye.com/oneinstack-full.tar.gz && tar xzf oneinstack-full.tar.gz && ./oneinstack/install.sh --nginx_option 1 --php_option 9 --phpcache_option 1 --phpmyadmin  --db_option 2 --dbinstallmethod 1 --dbrootpwd jtrof057 --node  --pureftpd  --redis  --memcached  --iptables  --reboot
```

安装可能需要 `1~3`个小时，请耐心等待。

安装完成后目录里会多出一个 `oneinstack文件夹`

进入文件夹并开始创建虚拟主机。

```shell
cd oneinstack && sudo ./vhost.sh
```

按照以下参考以此配置HTTPS,域名,网站根目录,防盗链,伪静态。

这里为了测试方便并不开启HTTPS和防盗链，但是在正式环境中应该开启。

![IMG_20220403_141613.jpg](https://alpha-q3.sourcegcdn.com/2022/04/03/UMqEq5mS.jpg/webp)

然后进入你设置的网站根目录下载WordPress文件。

在网站根目录下执行:

```shell
sudo wget https://cn.wordpress.org/latest-zh_CN.zip && sudo apt install unzip && sudo unzip latest-zh_CN.zip && sudo mv -r ./wordpress/* ./
```

接着添加数据库。

首先查看数据库密码

```shell
cd ~/oneinstack 
sudo grep dbrootpwd options.conf
```

`dbrootpwd`项后的值即为你的MySQL数据库root用户的密码

然后使用 `公网IP:80`进入 `oneinstack管理页面`,然后进入 `PhpMyAdmin`,使用用户名 `root`,刚刚查看的密码登录。

在终端控制台输入:

```sql
create user wordpress@'%' identified by 'yourpassword'
```

创建一个名为 `wordpress`,密码为 `yourpassword`的账户,账户账号和密码可以自行输入。

随后创建一个名为 `wordpress`的数据库,并授权,数据库名称可自定。

```sql
create database wordpress
```

```继续sql
grant all privileges on wordpress.* to wordpress@'%' with grant option
```

然后进入网站根目录进行授权:

```shell
cd /data/wwwroot
sudo chown -R www test.example.com
sudo chmod -R 777 test.example.com
```

最后重启 `NGINX`:

```shell
sudo systemctl reload nginx
```

打开网站就可以安装你的WordPress博客了，按照数据库账号,密码完成安装。

### 使用Docker部署

#### 环境安装

##### Docker安装

为了方便，推荐使用官方脚本安装。此脚本适用于常用 Linux 发行版。

```shell
curl -fsSL https://get.docker.com | sudo sh
```

默认情况下，Docker 只能通过 root 用户运行，普通用户通常要加 `sudo`。如果觉得麻烦，可以启用 Docker 的 rootless 模式。使用普通用户执行下面这条命令即可安装：

```shell
dockerd-rootless-setuptool.sh install
```

##### 安装 Docker Compose

下载二进制文件

```shell
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

赋予执行权限

```shell
sudo chmod +x /usr/local/bin/docker-compose
```

#### 设置容器

##### 创建项目

1.新建项目目录，这里以 `~/my_wordpress`为例。

```shell
mkdir ~/my_wordpress
```

2.进入项目目录

```shell
cd ~/my_wordpress
```

3.编辑配置文件

```shell
nano docker-compose.yml
```

文件内容:

```yml
version: "3.9"
 
services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: somewordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
 
  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    volumes:
      - wordpress_data:/var/www/html
    ports:
      - "80:80"
      - "443:443"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress
volumes:
  db_data: {}
  wordpress_data: {}
```

注意:

这里用到了 `mysql:5.7` 和 `wordpress:latest` 两个 Docker 镜像，WordPress 镜像依赖于 `MySQL`镜像。

`restart: always` 参数表明容器服务宕机后会自动重启。

`MYSQL_ROOT_PASSWORD `为数据库的 root 密码，`MYSQL_PASSWORD` 为数据库的普通用户密码，请自行修改，对应的 `WORDPRESS_DB_PASSWORD` 也要同时修改。`MYSQL_USER` 为数据库普通用户的用户名，如果有需要也可以修改，对应的 `WORDPRESS_DB_USER` 也要同时修改。

`80:80` 的意思是把宿主机的 80 端口映射到容器内部的 80 端口。如需通过其他端口访问，只需修改前面的 80。比如，我要通过 8080 端口访问 WordPress，填写 `8080:80`即可。

执行 `Ctrl + O `保存文件，回车，再执行 `Ctrl + X` 退出。

##### 启动容器

在 `~/my_wordpress`目录中执行以下命令启动 WordPress：

```shell
sudo docker-compose up -d
```

构建完成后就可以通过 `http://ip:port `来访问 WordPress（请将ip替换为 VPS 的 IP，`port` 替换为你使用的端口，如果是 80 端口则可以省略）。如果提示 `Error establishing a database connection`，说明配置尚未完成，等待 1～2 分钟，刷新网页即可进入安装界面。

##### 配置SSL

进入容器

```shell
sudo docker-compose exec wordpress bash
```

`注意：本章中后续命令都要在容器中执行！`

安装 cron 及 nano

```shell
apt update && apt install -y cron nano
```

安装 acme.sh 用于签发 SSL 证书（请把 my@example.com 改为你的邮件地址）

```shell
curl  https://get.acme.sh | sh -s email=my@example.com
```

将域名解析至 VPS 的 IP，然后执行以下命令签发证书（请把 example.com 改为你的域名）

```shell
bash ~/.acme.sh/acme.sh --issue -d example.com --apache  --tlsport 56789
```

启用模块

```shell
a2enmod rewrite
a2enmod ssl
```

创建证书目录

```
mkdir -p /etc/apache2/ssl
```

复制证书（请把 `example.com` 改为你的域名1

创建站点（将以下全部内容粘贴进终端 )

启用站点

```
a2ensite wordpress
service apache2 restart
```

编辑 `/var/www/html/.htaccess`，在顶部加入以下内容：

```
# BEGIN SSL Redirect
<IfModule mod_rewrite.c>
RewriteEngine on
RewriteCond %{HTTPS} !=on [NC]
RewriteRule ^(.*)$ https://%{HTTP_HOST}/$1 [R=301,L]
</IfModule>
# END SSL Redirect
```

最后一步，访问域名，进入 WordPress 后台，打开 「设置」-「常规选项」，并把 **WordPress地址** 和 **站点地址** 中的 `http` 改为 `https`，并保存。

至此，SSL 配置已完成。

该部署方法转载自

[Tony's Blog:通过 Docker Compose 部署 WordPress](https://blog.iamsjy.com/2022/03/29/deploy-wordpress-with-docker-compose/)

`遵循CC BY-NC-SA 4.0开源协议进行转载，已获原作者授权`
