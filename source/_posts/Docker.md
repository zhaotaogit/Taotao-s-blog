---
title: Docker
top: true
cover: true
toc: true
mathjax: false
date: 2021-11-18 17:04:26
author:
img: https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/Docker.png
coverImg:
password:
summary: Docker
tags: Docker
categories: Docker
---

# Docker

## 1.配置虚拟机IP

```shell
# 编辑网络配置文件
[root@localhost ~]# vim /etc/sysconfig/network-scripts/ifcfg-ens33
TYPE=Ethernet
# 静态IP
BOOTPROTO=static
NAME=ens33
DEVICE=ens33
# 开机自启
ONBOOT=yes
# IP地址
IPADDR=192.168.1.202
# 子网掩码
NETMASK=255.255.255.0
# 网关
GATEWAY=192.168.1.1
# DNS
DNS1=114.114.114.114
DNS2=1.2.4.8

```

![image-20211023155716216](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Docker/image-20211023155716216.png)

```shell
# 重启网卡
[root@localhost ~]# systemctl restart network
```

## 2.安装Docker引擎

```shell
[root@localhost ~]# sudo yum install -y yum-utils	# 安装yum-utils包
# 设置仓库地址-阿里云
[root@localhost ~]# sudo yum-config-manager \
    --add-repo \
    http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
# 安装docker引擎
[root@localhost ~]# sudo yum install docker-ce docker-ce-cli containerd.io
# 启动docker
[root@localhost ~]# sudo systemctl start docker
# 查看docker版本
[root@localhost ~]# docker -v
Docker version 20.10.9, build c2ea9bc
# 通过run hello-world 验证 Docker Engine 是否已正确安装。
[root@localhost ~]# sudo docker run hello-world
```

![image-20211023163223998](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Docker/image-20211023163223998.png)

## 3.Doker的启动与停止命令

```shell
[root@localhost ~]# sudo systemctl start docker	# 启动docker
[root@localhost ~]# sudo systemctl stop docker	# 停止docker
[root@localhost ~]# sudo systemctl restart docker	# 重启docker
[root@localhost ~]# sudo systemctl enable docker	# 设置开机自启docker
[root@localhost ~]# sudo systemctl status docker	# 查看docker状态
[root@localhost ~]# sudo docker info	# 查看docker的概要信息
[root@localhost ~]# sudo docker --help	# 查看docker的帮助信息
```

## 4.配置镜像加速

> Docker 从 Docker Hub 拉取镜像，因为是从国外获取，所以速度较慢
> 可以通过配置国内镜像源的方式，从国内获取镜像，提高拉取速度。

```shell
# 编辑文件
vim /etc/docker/daemon.json
```

![image-20211023164554380](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Docker/image-20211023164554380.png)

设置163和中国科技大学的镜像

- 重新加载配置信息及重启docker服务

  ```shell
  # 重新加载文件
  [root@localhost ~]# sudo systemctl daemon-reload
  # 重启docker
  [root@localhost ~]# sudo systemctl restart docker
  ```

  

## 5.镜像相关命令

### 1.查看镜像

```shell
[root@localhost ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
hello-world   latest    feb5d9fea6a5   4 weeks ago   13.3kB
```

- **REPOSITORY** : 镜像在仓库中的名称

- **TAG**：镜像标签，latest代表最新版本

- **IMAGE ID**：镜像ID

- **CREATED**：镜像创建的日期

- **SIZE**：镜像大小

  这些镜像都是存储在宿主机**/etc/lib/docker**目录下的

### 3.搜索镜像

语法:

```shell
docker search 镜像名称	
```

实例：

```shell
[root@localhost ~]# docker search redis	# 搜索名为redis的镜像
NAME                             DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
redis                            Redis is an open source key-value store that…   10076     [OK]       
sameersbn/redis                                                                  83                   [OK]
grokzen/redis-cluster            Redis cluster 3.0, 3.2, 4.0, 5.0, 6.0, 6.2      79                   
rediscommander/redis-commander   Alpine image for redis-commander - Redis man…   66                   [OK]
redislabs/redisearch             Redis With the RedisSearch module pre-loaded…   40                   
redislabs/redisinsight           RedisInsight - The GUI for Redis                35                   
oliver006/redis_exporter          Prometheus Exporter for Redis Metrics. Supp…   31                   
redislabs/redis                  Clustered in-memory database engine compatib…   31                   
redislabs/rejson                 RedisJSON - Enhanced JSON data type processi…   29                   
arm32v7/redis                    Redis is an open source key-value store that…   25                   
redislabs/redisgraph             A graph database module for Redis               16                   [OK]
arm64v8/redis                    Redis is an open source key-value store that…   16                   
redislabs/rebloom                A probablistic datatypes module for Redis       16                   [OK]
redislabs/redismod               An automated build of redismod - latest Redi…   15                   [OK]
webhippie/redis                  Docker image for redis                          11                   [OK]
redislabs/redistimeseries        A time series database module for Redis         10                   
s7anley/redis-sentinel-docker    Redis Sentinel                                  10                   [OK]
insready/redis-stat              Docker image for the real-time Redis monitor…   10                   [OK]
goodsmileduck/redis-cli          redis-cli on alpine                             9                    [OK]
centos/redis-32-centos7          Redis in-memory data structure store, used a…   5                    
clearlinux/redis                 Redis key-value data structure server with t…   3                    
wodby/redis                      Redis container image with orchestration        1                    [OK]
tiredofit/redis                  Redis Server w/ Zabbix monitoring and S6 Ove…   1                    [OK]
xetamus/redis-resource           forked redis-resource                           0                    [OK]
centos/redis-5-centos7           Redis in-memory data structure store, used a…   0                    
[root@localhost ~]# 

```

### 4.拉取镜像

​	语法：

```docker
docker pull 镜像名称
```

​	假如我们要拉去centos镜像到本地，如果不声明镜像TAG标签信息则默认拉取latest版本，也可以通过hub.docker.com搜索该镜像，查看支持的TAG信息。

```shell
[root@localhost ~]# docker pull redis
Using default tag: latest
latest: Pulling from library/redis
7d63c13d9b9b: Pull complete 
a2c3b174c5ad: Pull complete 
283a10257b0f: Pull complete 
7a08c63a873a: Pull complete 
0531663a7f55: Pull complete 
9bf50efb265c: Pull complete 
Digest: sha256:a89cb097693dd354de598d279c304a1c73ee550fbfff6d9ee515568e0c749cfe
Status: Downloaded newer image for redis:latest
docker.io/library/redis:latest
[root@localhost ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
redis         latest    7faaec683238   12 days ago   113MB
hello-world   latest    feb5d9fea6a5   4 weeks ago   13.3kB
[root@localhost ~]# docker pull redis:5
5: Pulling from library/redis
7d63c13d9b9b: Already exists 
a2c3b174c5ad: Already exists 
283a10257b0f: Already exists 
54ac4e97e390: Pull complete 
0d3ede1e63a5: Pull complete 
878bf2d7168d: Pull complete 
Digest: sha256:8217ee751b6a72bc4b3ef757c18aa9619e939d5073d5a26ce2074905385000b0
Status: Downloaded newer image for redis:5
docker.io/library/redis:5
[root@localhost ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
redis         5         02fee89f17ad   12 days ago   110MB
redis         latest    7faaec683238   12 days ago   113MB
hello-world   latest    feb5d9fea6a5   4 weeks ago   13.3kB
[root@localhost ~]# 
```

### 5.删除镜像

```shell
docker rmi 镜像名/镜像id
```

```shell
[root@localhost ~]# docker rmi redis
Untagged: redis:latest
Untagged: redis@sha256:a89cb097693dd354de598d279c304a1c73ee550fbfff6d9ee515568e0c749cfe
Deleted: sha256:7faaec68323851b2265bddb239bd9476c7d4e4335e9fd88cbfcc1df374dded2f
Deleted: sha256:e6deb90762475cda72e21895911f830ed99fd1cc6d920d92873270be91235274
Deleted: sha256:2649acad13241d9c8d81e49357bc66cce459b352ded7f423d70ede7bd3bb7b89
Deleted: sha256:64007bba5fc220df4d3da33cecdc2d55dd6a73528c138b0fa1acd79fd6a9c217
[root@localhost ~]# docker rmi redis:5
Untagged: redis:5
Untagged: redis@sha256:8217ee751b6a72bc4b3ef757c18aa9619e939d5073d5a26ce2074905385000b0
Deleted: sha256:02fee89f17adc8213b560b929d5ac585137612651f8eeb26423aadfe39dc3847
Deleted: sha256:f92e4de257018a916bd0715da7b1dd39a3540fa393799c2219a82f0ce99d57e2
Deleted: sha256:b13f2ab83d74b48551107876f35dcdaa7197a557fd4769cd4bfeb56bc4f031b6
Deleted: sha256:58ca4126d8128345fc58de904cb9029f2a1deb1f88b1fa0ac3f3f0e707f099b9
Deleted: sha256:b2cc2f1bf8b1cca8ba7c19e1697f7b73755903ad8f880b83673fd6a697aca935
Deleted: sha256:fbd1283ab782925be4d990bd4bebe9ad5e5cf9a525abfb6fa87465e072da9d31
Deleted: sha256:e8b689711f21f9301c40bf2131ce1a1905c3aa09def1de5ec43cf0adf652576e
[root@localhost ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
hello-world   latest    feb5d9fea6a5   4 weeks ago   13.3kB
[root@localhost ~]# 
```

## 6.容器相关命令

### 1.查看容器

```shell
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

- **CONTAINER** ID：容器ID
- **IMAGE**：所属镜像
- **COMMAND**：
- **CREATED**：创建时间
- **STATUS**：状态
- **PORTS**：端口
- **NAMES**：容器名称



​	查看所有容器(停止和运行)

```shell
[root@localhost ~]# docker ps -a	
CONTAINER ID   IMAGE         COMMAND    CREATED        STATUS                    PORTS     NAMES
a08d44d00165   hello-world   "/hello"   27 hours ago   Exited (0) 27 hours ago             magical_buck
```

​	查看停止运行的容器

```shell
[root@localhost ~]# docker ps -f status=exited
CONTAINER ID   IMAGE         COMMAND    CREATED        STATUS                    PORTS     NAMES
a08d44d00165   hello-world   "/hello"   27 hours ago   Exited (0) 27 hours ago             magical_buck
```

​	查看最后一次运行的容器

```shell
[root@localhost ~]# docker ps -l
CONTAINER ID   IMAGE         COMMAND    CREATED      STATUS                  PORTS     NAMES
a08d44d00165   hello-world   "/hello"   2 days ago   Exited (0) 2 days ago             magical_buck
```

​	列出最近创建的n个容器

```shell
[root@localhost ~]# docker ps -n 2
CONTAINER ID   IMAGE         COMMAND    CREATED      STATUS                  PORTS     NAMES
a08d44d00165   hello-world   "/hello"   2 days ago   Exited (0) 2 days ago             magical_buck
```

### 2.创建与启动容器

```shell
[root@localhost ~]# docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

- -i：表示运行的容器
- -t ：表示容器启动后会进入其命令行。加入这两个参数后，容器创建就能登陆进去。即分配一个伪终端。
- --name：为创建的容器命名。
- -v：表示目录映射关系（前者是宿主机目录，后者是映射到宿主机上的目录），可以使用多个-v做多个目录或文件映射。注意：最好做目录映射，在宿主机上做修改，然后共享到容器上。
- -d：在run后面加上-d参数，则会创建一个守护式容器在后台运行（这样创建容器后就不会自动登录容器，如果只加-i -t两个参数，创建容器后就会自动进容器里）。
- -p：表示端口映射，前者是宿主机端口，后者是容器内的映射端口。可以使用多个-p做多个端口映射。
- -P：随机使用宿主机的可用端口与容器暴露的端口映射。

​	创建容器并进入

```shell
[root@localhost ~]# docker run --name mynginx -P nginx	# 创建一个nginx容器，自定义名称为mynginx,将nginx的端口随机映射到宿主机端口
[root@localhost ~]# docker ps	# 查看正在运行的容器，发现nginx映射到了宿主机的49153端口
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                     NAMES
12c76efcc8f7   nginx     "/docker-entrypoint.…"   48 seconds ago   Up 47 seconds   0.0.0.0:49153->80/tcp, :::49153->80/tcp   mynginx
```

​	守护方式创建容器

```shell
[root@localhost ~]# docker run -di --name mynginx -p 80:80 nginx
a0a190090a232b9d3ed1a0882d77088c198d710b129ec764d9b66cedc960f096
[root@localhost ~]# 
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                               NAMES
a0a190090a23   nginx     "/docker-entrypoint.…"   11 seconds ago   Up 11 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp   mynginx
[root@localhost ~]# 
```

​	登录到守护方式创建的容器

```shell
[root@localhost ~]# docker exec -it mynginx /bin/bash
root@a0a190090a23:/#
```

​	启动与停止容器

```shell
[root@localhost ~]# docker start mynginx
mynginx
[root@localhost ~]# docker stop mynginx
mynginx
```

删除容器

```shell
[root@localhost ~]# docker rm 12c76efcc8f7	# 删除id为12c76efcc8f7的容器
12c76efcc8f7
```

### 3.文件拷贝

​	宿主机拷贝到容器

```shell
docker cp 需要拷贝的文件或目录 容器名称:容器目录
```

​	例：将宿主机中的test.py文件拷贝到mynginx容器中的/root目录下

```shell
[root@localhost ~]# vi test.py
[root@localhost ~]# docker cp test.py mynginx:/root
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS         PORTS                               NAMES
a0a190090a23   nginx     "/docker-entrypoint.…"   10 minutes ago   Up 3 minutes   0.0.0.0:80->80/tcp, :::80->80/tcp   mynginx
[root@localhost ~]# docker exec -it mynginx /bin/bash
root@a0a190090a23:/# ls /root/
test.py
root@a0a190090a23:/# 
```

​	容器拷贝到宿主机

```shell
docker cp 容器名称:容器目录 需要拷贝的文件或目录 
```

​	例：

```shell
root@a0a190090a23:~# touch test.txt
root@a0a190090a23:~# exit
exit
[root@localhost ~]# docker cp mynginx:/root/test.txt ./
[root@localhost ~]# ls
anaconda-ks.cfg  index.txt  test.py  test.txt
```

## 7.目录挂载

### 1.指定目录挂载

```shell
# 创建一个nginx容器，端口映射为81端口，宿主机的/root/mynginx_02映射到容器的/root/mynginx_02目录
# 此时，修改宿主机的/root/mynginx_02同时会修改容器的/root/mynginx_02
[root@localhost ~]# docker run -di --name nginx02 -p 81:80 -v /root/mynginx_02/:/root/mynginx_02 nginx
64e80e6ff89ecefea568b317690baa8c9072c270a480db3c749d0ebc07202616
```

​	查看某个容器的详细信息


```shell
[root@localhost mynginx_02]# docker inspect nginx02	# 查看nginx02的详细信息
```

### 2.匿名挂载

> 匿名挂载就是在宿主机中生成的目录名称是随机命名的

​	匿名挂载只需要写容器的目录即可，容器外对应的目录会在/var/lib/docker/volume中生成。

```shell
# 匿名挂载
docker run -di -v /usr/local/data --name centos7-02 centos:7 
# 查看volume数据卷信息
docker volume ls
```

​	例:

```shell
# 匿名挂载目录
[root@localhost ~]# docker run -di -v /usr/local/data --name centos7-02 centos:7 
59778edd9a81bc5c5dcd24799429c05fec27e8d6042c88735f23d301f78a80c1
# 查看生成的数据卷信息
[root@localhost ~]# ls /var/lib/docker/volumes/
backingFsBlockDev  e83692d4dbc68d740a75f7761cec27738f120afae98be50948527665da95bf54  metadata.db
# 进入容器的/usr/local/data目录随意创建一个文件
[root@localhost ~]# docker exec -it centos7-02 /bin/bash
[root@59778edd9a81 /]# cd /usr/local/data/
[root@59778edd9a81 data]# ls
[root@59778edd9a81 data]# touch test.txt      
# 在宿主机中查看容器对应的目录
[root@localhost ~]# cd /var/lib/docker/volumes/
backingFsBlockDev                                                 metadata.db
e83692d4dbc68d740a75f7761cec27738f120afae98be50948527665da95bf54/ 
[root@localhost ~]# cd /var/lib/docker/volumes/e83692d4dbc68d740a75f7761cec27738f120afae98be50948527665da95
[root@localhost e83692d4dbc68d740a75f7761cec27738f120afae98be50948527665da95bf54]# ls
_data
[root@localhost e83692d4dbc68d740a75f7761cec27738f120afae98be50948527665da95bf54]# cd _data/
# 发现宿主机此目录下同容器一样，有刚创建的test.txt文件
[root@localhost _data]# ls
test.txt
```

### 3.具名挂载

> 具名挂载就是在宿主机中生成的目录名称是我们指定的名称

```shell
# 创建一个nginx容器，指定宿主机目录为docker_nginx_data,容器中对应的目录为/usr/local/data,
[root@localhost volumes]# docker run -di -v docker_nginx_data:/usr/local/data --name nginx06 nginx
e832041a8a3804f68204b8740c8addb8865df7ae8bec9b477ab851d0b1671c83
# 查看宿主机生成的新目录，发现有了docker_nginx_data
[root@localhost volumes]# ls /var/lib/docker/volumes/
backingFsBlockDev  docker_nginx_data  e83692d4dbc68d740a75f7761cec27738f120afae98be50948527665da95bf54  metadata.db
```

### 4.数据卷只读

> 数据卷只读就是挂载到容器中目录，容器只有读取权限。

```shell
[root@localhost volumes]# docker run -di --name nginx07 -P -v /nginx07:/nginx07:ro nginx
8ca4534cb21f57ff7d7a4fe2d6caa4caa25f604132982072c8664db1289c43d0
# 发现在var/lib/docker/volumes/目录中不会有目录生成，新目录生成在宿主机的/nginx07
[root@localhost volumes]# ls /var/lib/docker/volumes/
backingFsBlockDev  docker_nginx_data  e83692d4dbc68d740a75f7761cec27738f120afae98be50948527665da95bf54  metadata.db
# 此时想在容器中创建文件就会报错
root@8ca4534cb21f:/nginx07# touch 123
touch: cannot touch '123': Read-only file system
```



### 5.volume-form继承

> 一个容器继承领另一个容器挂载的地址

```shell
# 创建一个新的容器nginx09，继承nginx07挂载的地址
[root@localhost _data]# docker run -di --name nginx09 --volumes-from nginx07 nginx
0bc9b443996448b613df2841d229ec769418d1365737da16ed39ab1fc15df722
# 此时进入容器中查看
[root@localhost _data]# docker exec -it nginx09 /bin/bash
# 发现有nginx07目录
root@0bc9b4439964:/# ls
bin  boot  dev	docker-entrypoint.d  docker-entrypoint.sh  etc	home  lib  lib64  media  mnt  nginx07  opt  proc  root	run  sbin  srv	sys  tmp  usr  var
# 进入nginx07目录，发现有1.txt文件
root@0bc9b4439964:/# cd nginx07/
root@0bc9b4439964:/nginx07# ls 
1.txt
```

### 6.查看目录卷挂载关系

```shell
# 查看目录卷的创建时间、名称、位置
[root@localhost _data]# docker volume inspect docker_nginx_data
[
    {
        "CreatedAt": "2021-10-31T04:41:05-04:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/docker_nginx_data/_data",
        "Name": "docker_nginx_data",
        "Options": null,
        "Scope": "local"
    }
]
# 查看某个容器的ip
[root@localhost _data]# docker inspect --format='{{.NetworkSettings.IPAddress}}' nginx07
172.17.0.2

```

## 8.docker镜像构建

- docker commit：从容器创建一个新镜像
- docker bulid：配合dockerfile创建一个镜像

### 1.通过**docker commit**来实现镜像的构建

> 我们通过基础镜像centos7，在容器中安装jdk和tomcat来创建一个新的镜像mycentos::seven:

1. **创建容器**

```shell
[root@localhost _data]# docker pull cnetos:7	# 拉取镜像
[root@localhost _data]# docker run -di --name centos7 centos:7	# 基于centos:7镜像创建一个容器centos
d38288c7a5bd5ee4edc1586d20b7e3b1900084f8267d6be977187793d898f00a
```

2. **拷贝资源**

> 先在宿主机中准备好tomcat和jdk的安装包，然后将安装包拷贝到容器中

```shell
# 将安装包拷贝到容器
[root@localhost ~]# docker cp /root/apache-tomcat-8.5.72.tar.gz centos7:/root
[root@localhost ~]# docker cp /root/jdk-8u311-linux-x64.tar.gz centos7:/root
# 进入容器中查看拷贝的东西
[root@localhost ~]# docker exec -it centos7 /bin/bash
[root@d38288c7a5bd /]# cd /root/
[root@d38288c7a5bd ~]# ls
anaconda-ks.cfg  apache-tomcat-8.5.72.tar.gz  jdk-8u311-linux-x64.tar.gz
# 解压文件
[root@d38288c7a5bd ~]# tar -zxvf apache-tomcat-8.5.72.tar.gz -C /usr/local/tomcat/
[root@d38288c7a5bd ~]# tar -zxvf jdk-8u311-linux-x64.tar.gz -C /usr/local/java/
# 配置环境变量
[root@d38288c7a5bd ~]# vi /etc/profile
# 添加以下配置，然后保存退出
export JAVA_HOME=/usr/local/java/jdk1.8.0_311
export PATH=$PATH:$JAVA_HOME/bin
# 使配置生效
[root@d38288c7a5bd ~]# source /etc/profile
# 检查java环境是否配好
[root@d38288c7a5bd ~]# java -version
java version "1.8.0_311"
Java(TM) SE Runtime Environment (build 1.8.0_311-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.311-b11, mixed mode)

```

![image-20211101180436025](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Docker/image-20211101180436025.png)

3. **构建镜像**

```shell
docker commit [options] CONTAINER [REPOSITORY[:TAG]]
```

- -a : 提交镜像的作者
- -m：提交镜像时的说明文字
- -c：使用Dockerfile指令来创建镜像
- -p：在创建镜像时将容器暂停

```shell
# 将自己的centos7容器生成一个mycentos7:7的镜像，-a代表镜像作者，-m代表这次构建镜像提交的信息
[root@localhost ~]# docker commit -a="myhelloworld" -m="java8 and tomcat9" centos7 mycentos:7
sha256:4def58ba6be8479e46dc18af7189c0ae64db802fda4af16da3d33d37d3601d8b
# 查看docker有哪些镜像，发现多了一个自己创建的mycentos
[root@localhost ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED          SIZE
mycentos      7         4def58ba6be8   11 seconds ago   741MB
nginx         latest    87a94228f133   2 weeks ago      133MB
hello-world   latest    feb5d9fea6a5   5 weeks ago      13.3kB
centos        7         eeb6ee3f44bd   6 weeks ago      204MB
```

4. **用自己的镜像创建容器**

```shell
# 尝试用自己构建的镜像创建容器
[root@localhost ~]# docker run -di --name centos7 -p 8080:8080 mycentos:7
e4137800776b4b2e6dd37ee2a8203ae7a3e37d343cd140cd4de73190948d9337
# 进入容器
[root@localhost ~]# docker exec -it centos7 bash
[root@e4137800776b /]# 
[root@e4137800776b /]# cd /usr/local/tomcat/apache-tomcat-8.5.72/
# 尝试运行tomcat，发现报错
[root@e4137800776b apache-tomcat-8.5.72]# ./bin/startup.sh 
Neither the JAVA_HOME nor the JRE_HOME environment variable is defined
At least one of these environment variable is needed to run this program
# 使环境变量生效
[root@e4137800776b apache-tomcat-8.5.72]# source /etc/profile
# 再次尝试，发现成功
[root@e4137800776b apache-tomcat-8.5.72]# ./bin/startup.sh 
Using CATALINA_BASE:   /usr/local/tomcat/apache-tomcat-8.5.72
Using CATALINA_HOME:   /usr/local/tomcat/apache-tomcat-8.5.72
Using CATALINA_TMPDIR: /usr/local/tomcat/apache-tomcat-8.5.72/temp
Using JRE_HOME:        /usr/local/java/jdk1.8.0_311
Using CLASSPATH:       /usr/local/tomcat/apache-tomcat-8.5.72/bin/bootstrap.jar:/usr/local/tomcat/apache-tomcat-8.5.72/bin/tomcat-juli.jar
Using CATALINA_OPTS:   
Tomcat started.
```

此时用一台电脑访问宿主机ip:8080即可看到如下界面：

![image-20211101182522409](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Docker/image-20211101182522409.png)

### 2.Dockerfile作用

```shell
[root@localhost ~]# mkdir -p /usr/local/dockerfile
[root@localhost dockerfile]# vi Dockerfile
ENV JAVA_HOME=/usr/loacl/java/jdk1.8.0_311
ENV PATH=$PATH:$JAVA_HOME/bin
# 启动容器时启动tomcat
CMD ["/usr/local/tomcat/apache-tomcat-8.5.72/bin/catalina.sh","run"]
[root@localhost ~]# vi /usr/local/dockerfile/Dockerfile 

# 指明构建的新镜像的基础镜像是来自centos:7的
FROM centos:7
# 通过镜像标签声明了作者信息
LABEL maintainer="mrhelloworld.com"
# 设置工作目录
WORKDIR /usr/local
# 新镜像构建成功以后创建指定目录
RUN mkdir -p /usr/local/java && /usr/local/tomcat
# 拷贝文件到镜像中并解压
ADD jdk-8u311-linux-x64.tar.gz /usr/local/java
ADD apache-tomcat-8.5.72.tar.gz /usr/local/tomcat
# 暴露容器运行时的8080监听端口给外部
EXPOSE 8080
# 设置容器内JAVA_HOME的环境变量
ENV JAVA_HOME=/usr/loacl/java/jdk1.8.0_311
ENV PATH=$PATH:$JAVA_HOME/bin
# 启动容器时启动tomcat
CMD ["/usr/local/tomcat/apache-tomcat-8.5.72/bin/catalina.sh","run"]

[root@localhost /]# cd root/
[root@localhost ~]# ls
anaconda-ks.cfg  apache-tomcat-8.5.72.tar.gz  index.txt  jdk-8u311-linux-x64.tar.gz  mynginx_02  test.py  test.txt
[root@localhost ~]# cp jdk-8u311-linux-x64.tar.gz /usr/local/dockerfile/
[root@localhost ~]# cp apache-tomcat-8.5.72.tar.gz /usr/local/dockerfile/
[root@localhost dockerfile]# ls
apache-tomcat-8.5.72.tar.gz  Dockerfile  jdk-8u311-linux-x64.tar.gz

```

![image-20211110203555946](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Docker/image-20211110203555946.png)

### 3.利用Dockerfile构建镜像

```shell
# /usr/local/dockerfile代表Dockerfile所需的安装包存放的位置
[root@localhost dockerfile]# docker build -f /usr/local/dockerfile/Dockerfile -t mycentos:7 /usr/local/dockerfile
Sending build context to Docker daemon  157.4MB
Step 1/11 : FROM centos:7
 ---> eeb6ee3f44bd
Step 2/11 : LABEL maintainer="mrhelloworld.com"
 ---> Running in acc7170cea8a
Removing intermediate container acc7170cea8a
 ---> f31f5a212077
Step 3/11 : WORKDIR /usr/local
 ---> Running in e547a711ed7a
Removing intermediate container e547a711ed7a
 ---> 5be9f42fcad7
Step 4/11 : RUN mkdir -p /usr/local/java
 ---> Running in 1a3724eaec53
Removing intermediate container 1a3724eaec53
 ---> 32f4418fdda7
Step 5/11 : RUN mkdir -p /usr/local/tomcat
 ---> Running in c418f32a0523
Removing intermediate container c418f32a0523
 ---> 8f58e412baca
Step 6/11 : ADD jdk-8u311-linux-x64.tar.gz /usr/local/java
 ---> f4ecfe50eafa
Step 7/11 : ADD apache-tomcat-8.5.72.tar.gz /usr/local/tomcat
 ---> 66b44bc9677a
Step 8/11 : EXPOSE 8080
 ---> Running in 17c52ce48b43
Removing intermediate container 17c52ce48b43
 ---> c54233396b41
Step 9/11 : ENV JAVA_HOME=/usr/local/java/jdk1.8.0_311
 ---> Running in cfb5833a22c1
Removing intermediate container cfb5833a22c1
 ---> 6252c1aba29d
Step 10/11 : ENV PATH=$PATH:$JAVA_HOME/bin
 ---> Running in 74cb21f735fd
Removing intermediate container 74cb21f735fd
 ---> 2d4b07c042a1
Step 11/11 : CMD ["/usr/local/tomcat/apache-tomcat-8.5.72/bin/catalina.sh","run"]
 ---> Running in fcee15fd66ae
Removing intermediate container fcee15fd66ae
 ---> bd1032e5d52e
Successfully built bd1032e5d52e
Successfully tagged mycentos:7
[root@localhost dockerfile]#
[root@localhost dockerfile]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED          SIZE
mycentos      7         bd1032e5d52e   24 seconds ago   584MB
hello-world   latest    feb5d9fea6a5   6 weeks ago      13.3kB
centos        7         eeb6ee3f44bd   7 weeks ago      204MB
# 用构建的镜像创建容器
[root@localhost dockerfile]# docker run -di --name mycentos7 -p 8080 mycentos:7
835d9e6796d019c46bd6b97d1b396a9c47f76df6d09982148684a5d93d7f6b52
# 查看容器是否已运行
[root@localhost dockerfile]# docker ps 
CONTAINER ID   IMAGE        COMMAND                  CREATED         STATUS         PORTS                                         NAMES
835d9e6796d0   mycentos:7   "/usr/local/tomcat/a…"   3 seconds ago   Up 2 seconds   0.0.0.0:49156->8080/tcp, :::49156->8080/tcp   mycentos7
[root@localhost dockerfile]#
# 接着直接在网页中访问ip:8080即可直接访问tomcat
```

![image-20211110204650718](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Docker/image-20211110204650718.png)

## 9.Docker的备份恢复迁移

### 1.镜像备份

​	使用 **docker save** 将指定镜像保存成tar文件

```shell
docker save [OPTIONS] IMAGE [IMAGE...]
docker save -o /root/mycentos7.tar mycentos:7
```

- -o ：镜像保存后保存的目录

例：

```shell
# 查看当前镜像有哪些
[root@localhost ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
hello-world   latest    feb5d9fea6a5   6 weeks ago   13.3kB
centos        7         eeb6ee3f44bd   8 weeks ago   204MB
# 将centos:7镜像打包成tar文件
[root@localhost ~]# docker save -o /root/mycentos.tar centos:7
# 查看是否生成文件
[root@localhost ~]# ls
anaconda-ks.cfg  apache-tomcat-8.5.72.tar.gz  index.txt  jdk-8u311-linux-x64.tar.gz  mycentos.tar  mynginx_02  test.py  test.txt
[root@localhost ~]# 

```

### 2.镜像恢复

​	使用**docker load**将**docker save**保存的tar文件导入到当前镜像

```shell
docker load [OPTIONS]
docker load -i mycentos.tar
```

- -i：指定导入的文件
- -q：精简输出信息

例：

```shell
# 删除原始镜像
[root@localhost ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
hello-world   latest    feb5d9fea6a5   6 weeks ago   13.3kB
centos        7         eeb6ee3f44bd   8 weeks ago   204MB
[root@localhost ~]# docker rmi centos:7
Untagged: centos:7
Untagged: centos@sha256:9d4bcbbb213dfd745b58be38b13b996ebb5ac315fe75711bd618426a630e0987
Deleted: sha256:eeb6ee3f44bd0b5103bb561b4c16bcb82328cfe5809ab675bb17ab3a16c517c9
Deleted: sha256:174f5685490326fc0a1c0f5570b8663732189b327007e47ff13d2ca59673db02
# 导入我们刚刚导出的镜像
[root@localhost ~]# docker load -i mycentos.tar 
174f56854903: Loading layer [==================================================>]  211.7MB/211.7MB
Loaded image: centos:7
# 查看是否导入
[root@localhost ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
hello-world   latest    feb5d9fea6a5   6 weeks ago   13.3kB
centos        7         eeb6ee3f44bd   8 weeks ago   204MB
[root@localhost ~]# 

```

## 10.DockerHub的使用

### 1.注册账号

先去https://hub.docker.com/注册一个账号

![image-20211113163804847](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Docker/image-20211113163804847.png)

### 2.登陆账号

然后登陆账号:

```shell
[root@localhost ~]# docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: 1787417712	# 输入自己的账号
Password: 				# 输入自己的密码
WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded	# 登陆成功提示
[root@localhost ~]# 
```

### 3.推送镜像至仓库

为了方便测试，我们将**hello-world**推送到仓库

先给镜像设置标签：**docker tag local-image:tagname new-repo:tagname**

再将镜像推送到仓库：**docker push new-repo:tagname**

```shell
# 查看有哪些镜像
[root@localhost ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
hello-world   latest    feb5d9fea6a5   7 weeks ago   13.3kB
centos        7         eeb6ee3f44bd   8 weeks ago   204MB
# 给一个镜像打标签
[root@localhost ~]# docker tag hello-world:latest 1787417712/test-helloworld:1.0.0
# 再次查看有哪些镜像
[root@localhost ~]# docker images
REPOSITORY                   TAG       IMAGE ID       CREATED       SIZE
1787417712/test-helloworld   1.0.0     feb5d9fea6a5   7 weeks ago   13.3kB
hello-world                  latest    feb5d9fea6a5   7 weeks ago   13.3kB
centos                       7         eeb6ee3f44bd   8 weeks ago   204MB
# 上传镜像
[root@localhost ~]# docker push 1787417712/test-helloworld:1.0.0
The push refers to repository [docker.io/1787417712/test-helloworld]
e07ee1baac5f: Pushed 
1.0.0: digest: sha256:f54a58bc1aac5ea1a25d796ae155dc228b3f0e11d046ae276b39c4bf2f13d8c4 size: 525
[root@localhost ~]# 
```

接着可以到hub.docker.com登陆自己的账号查看是否上传成功:

![image-20211113164236499](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Docker/image-20211113164236499.png)

### 4.尝试拉取自己上传的镜像

```shell
# 查看当前镜像
[root@localhost ~]# docker images
REPOSITORY                   TAG       IMAGE ID       CREATED       SIZE
1787417712/test-helloworld   1.0.0     feb5d9fea6a5   7 weeks ago   13.3kB
hello-world                  latest    feb5d9fea6a5   7 weeks ago   13.3kB
centos                       7         eeb6ee3f44bd   8 weeks ago   204MB
# 删除之前的镜像
[root@localhost ~]# docker rmi 1787417712/test-helloworld:1.0.0
Untagged: 1787417712/test-helloworld:1.0.0
Untagged: 1787417712/test-helloworld@sha256:f54a58bc1aac5ea1a25d796ae155dc228b3f0e11d046ae276b39c4bf2f13d8c4
[root@localhost ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
hello-world   latest    feb5d9fea6a5   7 weeks ago   13.3kB
centos        7         eeb6ee3f44bd   8 weeks ago   204MB
# 拉取自己上传的镜像
[root@localhost ~]# docker pull 1787417712/test-helloworld:1.0.0
1.0.0: Pulling from 1787417712/test-helloworld
Digest: sha256:f54a58bc1aac5ea1a25d796ae155dc228b3f0e11d046ae276b39c4bf2f13d8c4
Status: Downloaded newer image for 1787417712/test-helloworld:1.0.0
docker.io/1787417712/test-helloworld:1.0.0
# 查看是否拉取成功
[root@localhost ~]# docker images
REPOSITORY                   TAG       IMAGE ID       CREATED       SIZE
1787417712/test-helloworld   1.0.0     feb5d9fea6a5   7 weeks ago   13.3kB
hello-world                  latest    feb5d9fea6a5   7 weeks ago   13.3kB
centos                       7         eeb6ee3f44bd   8 weeks ago   204MB
[root@localhost ~]# 
```

### 5.退出账号

```shell
[root@localhost ~]# docker logout
Removing login credentials for https://index.docker.io/v1/
[root@localhost ~]# 
```

## 11.Docker私有仓库搭建

### 1.拉取registry镜像

```shell
[root@localhost ~]# docker pull registry
Using default tag: latest
latest: Pulling from library/registry
79e9f2f55bf5: Pull complete 
0d96da54f60b: Pull complete 
5b27040df4a2: Downloading [===============================================>   ]  6.449MB/6.824MB
e2ead8259a04: Downloading 
3790aef225b9: Downloading 
latest: Pulling from library/registry
79e9f2f55bf5: Pull complete 
0d96da54f60b: Pull complete 
5b27040df4a2: Pull complete 
e2ead8259a04: Pull complete 
3790aef225b9: Pull complete 
Digest: sha256:169211e20e2f2d5d115674681eb79d21a217b296b43374b8e39f97fcf866b375
Status: Downloaded newer image for registry:latest
docker.io/library/registry:latest
[root@localhost ~]#
```

### 2.修改配置文件

![image-20211113165513474](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Docker/image-20211113165513474.png)

```shell
[root@localhost ~]# vim /etc/docker/daemon.json
# 应用配置
[root@localhost ~]# sudo systemctl daemon-reload
# 重启docker
[root@localhost ~]# systemctl restart docker
```

### 3.创建私有仓库容器

```shell
[root@localhost ~]# docker run -di --name registry -p 5000:5000 -v /mydata/docker_registry:/var/lib/registry registry
8ce589a0bce5a7703d5c9fb018cdbdf8e147c05f878f057c4078731f4e8b5d84
[root@localhost ~]# 
[root@localhost ~]# cd /mydata/docker_registry/
[root@localhost docker_registry]# 
[root@localhost docker_registry]# ls
[root@localhost docker_registry]# docker ps
CONTAINER ID   IMAGE      COMMAND                  CREATED              STATUS              PORTS                                       NAMES
8ce589a0bce5   registry   "/entrypoint.sh /etc…"   About a minute ago   Up About a minute   0.0.0.0:5000->5000/tcp, :::5000->5000/tcp   registry
[root@localhost docker_registry]# 
```

接着打开浏览器输入ip:5000/v2/_catalog看到：

![image-20211113170311963](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Docker/image-20211113170311963.png)

即代表成功！

### 4.推送镜像到私有仓库

```shell
[root@localhost docker_registry]# docker tag hello-world:latest 192.168.1.250:5000/test-helloworld:1.0.0
#  192.168.1.250:5000是自己的ip+端口号
[root@localhost docker_registry]# docker push 192.168.1.250:5000/test-helloworld:1.0.0
The push refers to repository [192.168.1.250:5000/test-helloworld]
e07ee1baac5f: Pushed 
1.0.0: digest: sha256:f54a58bc1aac5ea1a25d796ae155dc228b3f0e11d046ae276b39c4bf2f13d8c4 size: 525
[root@localhost docker_registry]# 
```

刷新浏览器可以看到:

![image-20211113170647521](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Docker/image-20211113170647521.png)

### 5.拉取私有仓库镜像

```shell
[root@localhost docker_registry]# docker pull 192.168.1.250:5000/test-helloworld:1.0.0
1.0.0: Pulling from test-helloworld
Digest: sha256:f54a58bc1aac5ea1a25d796ae155dc228b3f0e11d046ae276b39c4bf2f13d8c4
Status: Downloaded newer image for 192.168.1.250:5000/test-helloworld:1.0.0
192.168.1.250:5000/test-helloworld:1.0.0
[root@localhost docker_registry]# docker images
REPOSITORY                           TAG       IMAGE ID       CREATED       SIZE
registry                             latest    b8604a3fe854   3 hours ago   26.2MB
192.168.1.250:5000/test-helloworld   1.0.0     feb5d9fea6a5   7 weeks ago   13.3kB
1787417712/test-helloworld           1.0.0     feb5d9fea6a5   7 weeks ago   13.3kB
hello-world                          latest    feb5d9fea6a5   7 weeks ago   13.3kB
centos                               7         eeb6ee3f44bd   8 weeks ago   204MB
[root@localhost docker_registry]# 
```

## 12.Docker网络模式

[Docker四种网络模式](https://www.jianshu.com/p/22a7032bb7bd)

| Docker网络模式 | 配置                      | 说明                                                         |
| -------------- | ------------------------- | ------------------------------------------------------------ |
| host模式       | –net=host                 | 容器和宿主机共享Network namespace。                          |
| container模式  | –net=container:NAME_or_ID | 容器和另外一个容器共享Network namespace。 kubernetes中的pod就是多个容器共享一个Network namespace。 |
| none模式       | –net=none                 | 容器有独立的Network namespace，但并没有对其进行任何网络设置，如分配veth pair 和网桥连接，配置IP等。 |
| bridge模式     | –net=bridge               | （默认为该模式）                                             |

### 1.host模式

创建容器时加上参数:**--network host**即可

```shell
# 创建一个容器，指定网络模式为host
[root@localhost /]# docker run -it --name bbox02 --network host busybox
/ # 
# 查看网卡ip
/ # ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast qlen 1000
    link/ether 00:0c:29:b5:59:76 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.250/24 brd 192.168.1.255 scope global ens33
       valid_lft forever preferred_lft forever
    inet6 fe80::e136:cd54:f97c:f725/64 scope link 
       valid_lft forever preferred_lft forever
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue 
    link/ether 02:42:23:92:ba:90 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
    inet6 fe80::42:23ff:fe92:ba90/64 scope link 
       valid_lft forever preferred_lft forever
/ # exit
[root@localhost /]# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
    link/ether 00:0c:29:b5:59:76 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.250/24 brd 192.168.1.255 scope global ens33
       valid_lft forever preferred_lft forever
    inet6 fe80::e136:cd54:f97c:f725/64 scope link 
       valid_lft forever preferred_lft forever
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN 
    link/ether 02:42:23:92:ba:90 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
    inet6 fe80::42:23ff:fe92:ba90/64 scope link 
       valid_lft forever preferred_lft forever
[root@localhost /]# 

```

 发现两者是相同的，即host模式就是容器使用的是宿主机的卡，相同的网络环境。

### bridge模式  

```shell
# 容器默认为bridge模式，所以创建的时候可以不加参数即为bridge模式
[root@localhost /]# docker run -it --name bbox02 busybox
/ # ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
10: eth0@if11: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1500 qdisc noqueue 
    link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.2/16 brd 172.17.255.255 scope global eth0
       valid_lft forever preferred_lft forever
/ # 
# 查看宿主机网卡情况，发现多了个13: veth7e697be@if12，容器和宿主机通信就是靠的这个网卡
[root@localhost ~]# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
    link/ether 00:0c:29:b5:59:76 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.250/24 brd 192.168.1.255 scope global ens33
       valid_lft forever preferred_lft forever
    inet6 fe80::e136:cd54:f97c:f725/64 scope link 
       valid_lft forever preferred_lft forever
3: docker0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP 
    link/ether 02:42:23:92:ba:90 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
    inet6 fe80::42:23ff:fe92:ba90/64 scope link 
       valid_lft forever preferred_lft forever
13: veth7e697be@if12: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master docker0 state UP 
    link/ether 96:86:47:33:2b:55 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet6 fe80::9486:47ff:fe33:2b55/64 scope link 
       valid_lft forever preferred_lft forever
[root@localhost ~]# 
```

### 3.none模式  

指定容器为None模式即容器开始没有网络，需要自己配置。

创建容器的时候加上参数**--network none**即可创建网络模式为none的容器。

### 4.container模式

创建容器时加上参数:**--network container:已运行的容器名/容器ID **即可

```shell
# 创建一个网络模式为container模式的容器，用bbox1相同的网络模式
[root@localhost /]# docker run -it --name bbox04 --network container:bbox1 busybox
/ # ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
14: eth0@if15: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1500 qdisc noqueue 
    link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.2/16 brd 172.17.255.255 scope global eth0
       valid_lft forever preferred_lft forever
/ # 
# 查看bbox1的网卡信息，发现和bbox04的一样
[root@localhost ~]# docker exec -it bbox1 sh
/ # ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
14: eth0@if15: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1500 qdisc noqueue 
    link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.2/16 brd 172.17.255.255 scope global eth0
       valid_lft forever preferred_lft forever
/ # 
```

## 12.自定义网络

### 1.创建网络

```shell
# 创建一个新的网络
[root@localhost /]# docker network create custom_network
358dcd3df93625bb7328383e89fc38cadb7046e5e31e4123bf72976d3ea874ca
# 查看是否创建成功
[root@localhost /]# docker network ls
NETWORK ID     NAME             DRIVER    SCOPE
a4417a6df8fc   bridge           bridge    local
358dcd3df936   custom_network   bridge    local
7e8bff04dc54   host             host      local
466f8d7fd78e   none             null      local
[root@localhost /]# 
# 分别创建bbox05和bbox06,网络模式选择刚创建的custom
[root@localhost /]# docker run -it --name bbox05 --network custom_network busybox
[root@localhost ~]# docker run -it --name bbox06 --network custom_network busybox
# 进入容器bbox05内,发现可以直接用容器名字ping
/ # ping bbox06
PING bbox06 (172.18.0.3): 56 data bytes
64 bytes from 172.18.0.3: seq=0 ttl=64 time=0.054 ms
64 bytes from 172.18.0.3: seq=1 ttl=64 time=0.189 ms
64 bytes from 172.18.0.3: seq=2 ttl=64 time=0.127 ms
64 bytes from 172.18.0.3: seq=3 ttl=64 time=0.131 ms
64 bytes from 172.18.0.3: seq=4 ttl=64 time=0.102 ms
^C
--- bbox06 ping statistics ---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max = 0.054/0.120/0.189 ms
/ # 
```

## 13.搭建Redis集群

### 1.环境准备

两台虚拟机:192.168.1.250,192.168.1.251

docker环境:

![image-20211114143238251](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Docker/image-20211114143238251.png)

docker镜像：redis

### 2.搭建

- 下载redis镜像

  ```shell
  [root@localhost ~]# docker pull redis
  ```

  

- 编写redis配置文件

  在两台虚拟机中分别执行:

  ```shell
  [root@localhost ~]# mkdir -p /usr/local/docker-redis/redis-cluster
  [root@localhost ~]# cd /usr/local/docker-redis/redis-cluster/
  [root@localhost redis-cluster]# vi redis-cluster.tmpl
  ```

  在192.168.1.250中编辑文件写入:

  ```shell
  port ${PORT}	# 端口
  requirepass 1234	# 密码
  masterauth 1234		# 集群节点密码
  protected-mode no	# 安全模式- 关闭
  daemonize no	    # 是否后台
  appendonly yes		# aof文件是否开启
  cluster-enabled yes	# 集群环境是否开启
  cluster-config-file nodes.conf	# 配置文件名称
  cluster-node-timeout 15000	# 超市时间
  cluster-announce-ip 192.168.1.250	# ip
  cluster-announce-port ${PORT}	# 集群端口
  cluster-announce-bus-port  1${PORT}	# 消息总线内部端口
  ```

  在192.168.1.251中编辑文件写入:

  ```shell
  port ${PORT}	# 端口
  requirepass 1234	# 密码
  masterauth 1234		# 集群节点密码
  protected-mode no	# 安全模式- 关闭
  daemonize no	    # 是否后台
  appendonly yes		# aof文件是否开启
  cluster-enabled yes	# 集群环境是否开启
  cluster-config-file nodes.conf	# 配置文件名称
  cluster-node-timeout 15000	# 超市时间
  cluster-announce-ip 192.168.1.251	# ip
  cluster-announce-port ${PORT}	# 集群端口
  cluster-announce-bus-port  1${PORT}	# 消息总线内部端口
  ```

  在192.168.1.250执行:

  ```shell
  for port in `seq 6371 6373`; do \
  mkdir -p ${port}/conf \
  && PORT=${port} envsubst < redis-cluster.tmpl > ${port}/conf/redis.conf \
  && mkdir -p ${port}/data;\
  done
  ```

  在192.168.1.251执行:

  ```shell
  for port in `seq 6374 6376`; do \
  mkdir -p ${port}/conf \
  && PORT=${port} envsubst < redis-cluster.tmpl > ${port}/conf/redis.conf \
  && mkdir -p ${port}/data;\
  done
  ```

  在192.168.1.250中执行:

  ```shell
  [root@localhost redis-cluster]# tree /usr/local/docker-redis/redis-cluster/
  /usr/local/docker-redis/redis-cluster/
  ├── 6371
  │   ├── conf
  │   │   └── redis.conf
  │   └── data
  ├── 6372
  │   ├── conf
  │   │   └── redis.conf
  │   └── data
  ├── 6373
  │   ├── conf
  │   │   └── redis.conf
  │   └── data
  └── redis-cluster.tmpl
  
  9 directories, 4 files
  [root@localhost redis-cluster]#
  ```

  在192.168.1.251中执行:

  ```shell
  [root@localhost redis-cluster]# tree /usr/local/docker-redis/redis-cluster/
  /usr/local/docker-redis/redis-cluster/
  ├── 6374
  │   ├── conf
  │   │   └── redis.conf
  │   └── data
  ├── 6375
  │   ├── conf
  │   │   └── redis.conf
  │   └── data
  ├── 6376
  │   ├── conf
  │   │   └── redis.conf
  │   └── data
  └── redis-cluster.tmpl
  
  9 directories, 4 files
  [root@localhost redis-cluster]# 
  ```

  

- 创建redis容器

在192.168.1.250中执行:

```shell
for port in $(seq 6371 6373); do \
  docker run -id --restart always --name redis-${port} --net host \
  -v /usr/local/docker-redis/redis-cluster/${port}/conf/redis.conf:/usr/local/etc/redis/redis.conf \
  -v /usr/local/docker-redis/redis-cluster/${port}/data:/data \
  redis redis-server /usr/local/etc/redis/redis.conf; \
done
```

在192.168.1.251中执行:

```shell
for port in $(seq 6374 6376); do \
  docker run -id --restart always --name redis-${port} --net host \
  -v /usr/local/docker-redis/redis-cluster/${port}/conf/redis.conf:/usr/local/etc/redis/redis.conf \
  -v /usr/local/docker-redis/redis-cluster/${port}/data:/data \
  redis redis-server /usr/local/etc/redis/redis.conf; \
done
```

就分别在两台虚拟机中各创建了3个redis容器

- 创建redis cluster集群

在192.168.1.250中执行：

```shell
[root@localhost redis-cluster]# docker exec -it redis-6371 bash
root@localhost:/data# cd /usr/local/bin/
root@localhost:/usr/local/bin# ls
docker-entrypoint.sh  gosu  redis-benchmark  redis-check-aof  redis-check-rdb  redis-cli  redis-sentinel  redis-server
root@localhost:/usr/local/bin# 
root@localhost:/data# redis-cli -a 1234 --cluster create 192.168.1.250:6371 192.168.1.250:6372 192.168.1.250:6373 192.168.1.251:6374  192.168.1.251:6375 192.168.1.251:6376 --cluster-replicas 1
Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
>>> Performing hash slots allocation on 6 nodes...
Master[0] -> Slots 0 - 5460
Master[1] -> Slots 5461 - 10922
Master[2] -> Slots 10923 - 16383
Adding replica 192.168.1.251:6376 to 192.168.1.250:6371
Adding replica 192.168.1.250:6373 to 192.168.1.251:6374
Adding replica 192.168.1.251:6375 to 192.168.1.250:6372
M: 456297129cb486b101c40e341365c10aa75ef9d6 192.168.1.250:6371
   slots:[0-5460] (5461 slots) master
M: ce097bae6e524e927a3c618cff0842b8e2ee733e 192.168.1.250:6372
   slots:[10923-16383] (5461 slots) master
S: 0dac43912efbda099854300fa6e1026247ff0808 192.168.1.250:6373
   replicates 1f11869fb991614ba37bc21944e9fe1a39a667ea
M: 1f11869fb991614ba37bc21944e9fe1a39a667ea 192.168.1.251:6374
   slots:[5461-10922] (5462 slots) master
S: 34365fc1c7931a5025364a7acd6f8c0a7b59e538 192.168.1.251:6375
   replicates ce097bae6e524e927a3c618cff0842b8e2ee733e
S: 7b13fc4d721522edd661755e058a9dda7b6dc579 192.168.1.251:6376
   replicates 456297129cb486b101c40e341365c10aa75ef9d6
Can I set the above configuration? (type 'yes' to accept): yes
>>> Nodes configuration updated
>>> Assign a different config epoch to each node
>>> Sending CLUSTER MEET messages to join the cluster
Waiting for the cluster to join
.
>>> Performing Cluster Check (using node 192.168.1.250:6371)
M: 456297129cb486b101c40e341365c10aa75ef9d6 192.168.1.250:6371
   slots:[0-5460] (5461 slots) master
   1 additional replica(s)
M: ce097bae6e524e927a3c618cff0842b8e2ee733e 192.168.1.250:6372
   slots:[10923-16383] (5461 slots) master
   1 additional replica(s)
M: 1f11869fb991614ba37bc21944e9fe1a39a667ea 192.168.1.251:6374
   slots:[5461-10922] (5462 slots) master
   1 additional replica(s)
S: 0dac43912efbda099854300fa6e1026247ff0808 192.168.1.250:6373
   slots: (0 slots) slave
   replicates 1f11869fb991614ba37bc21944e9fe1a39a667ea
S: 7b13fc4d721522edd661755e058a9dda7b6dc579 192.168.1.251:6376
   slots: (0 slots) slave
   replicates 456297129cb486b101c40e341365c10aa75ef9d6
S: 34365fc1c7931a5025364a7acd6f8c0a7b59e538 192.168.1.251:6375
   slots: (0 slots) slave
   replicates ce097bae6e524e927a3c618cff0842b8e2ee733e
[OK] All nodes agree about slots configuration.
>>> Check for open slots...
>>> Check slots coverage...
[OK] All 16384 slots covered.
root@localhost:/data# 
```



## 14.DockerCompose安装

```shell
# 安装
[root@localhost redis-cluster]#  sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--  100   633  100   633    0     0    880      0 --:--:-- --:--:-- --:--:--   881
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--    6 12.1M    6  804k    0     0   383k      0  0:00:32  0:00:02  0:00:30  100 12.1M  100 12.1M    0     0   204k      0  0:01:00  0:01:00 --:--:--  162k
[root@localhost redis-cluster]# cd /usr/local/bin/
[root@localhost bin]# ls
docker-compose
# 赋予执行权限
[root@localhost bin]# sudo chmod +x /usr/local/bin/docker-compose 
[root@localhost bin]# ll
total 12440
-rwxr-xr-x. 1 root root 12737304 Nov 14 02:27 docker-compose
[root@localhost bin]# 
```

