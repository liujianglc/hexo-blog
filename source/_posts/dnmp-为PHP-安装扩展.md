---
title: dnmp 为PHP 安装扩展
tags: 
	- dnmp
	- docker
categories: 
	- Docker
abbrlink: 26567
date: 2019-05-29 22:24:55
---

本地使用 dnmp 作为开发环境, 结果某一个项目使用的环境为 php56, 连接数据库使用的 mysql_connect, 当服务启动起来后, 
缺少mysql extension , 造成无法运行. 

解决办法:

# 第一种 进入容器内部修改
```
docker exec -it dnmp_php56_1 /bin/bash
```

进入镜像后, 运行
```
docker-php-ext-install mysql
```

然后在php.ini 文件中 , 添加

```
[Mysql]
mysql.allow_local_infile = On
mysql.allow_persistent = On
mysql.cache_size = 2000
mysql.connect_timeout = 60
mysql.default_host = ""
mysql.default_password = ""
mysql.default_port = ""
mysql.default_socket = ""
mysql.default_user = ""
mysql.max_links = -1
mysql.max_persistent = -1
mysql.trace_mode = Off
```

重启 php56, nginx 镜像. 
可以在根目录执行 

```
docker-compose restart 
```
或者只单独重启php的 container
```
docker container restart containerid
```

#  第二种 修改docker-compose 文件

在extensions 目录下的 install.sh 

添加 

```
if [ ${version} -lt 70200 ]; then
    docker-php-ext-install $mc mysql
fi
```
然后
```
docker-compose up -d
```


