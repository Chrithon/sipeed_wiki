# Docker开发环境

## docker安装

### 什么是docker？

Docker 是一个开源的应用容器引擎，基于 Go 语言 并遵从Apache2.0协议开源。Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app）,更重要的是容器性能开销极低。本节只简单介绍docker开发环境的搭建，想要详细了解docker，可以查看“[Docker 命令速查](./../../Zero-Doc/Start/docker_command.md)”。简而言之，我帮你搞好了docker镜像，你就不用自己再费力搭建啦。

### docker下载安装

```
sudo apt-get install docker.io
docker version
```

安装成功后可见版本信息

``` 
Client version: 1.6.2
Client API version: 1.18
Go version (client): go1.2.1
Git commit (client): 7c8fca2
OS/Arch (client): linux/amd64
FATA[0000] Get http:///var/run/docker.sock/v1.18/version: dial unix /var/run/docker.sock: permission denied. Are you trying to connect to a TLS-enabled daemon without TLS? 
```

默认情况下会报后面的错误，如果使用sudo就不会报错。不想每次都sudo的话，可以把用户加入到docker组。


如果还没有 docker group 就添加一个(默认安装后已经有了)

    sudo groupadd docker

将用户加入该 group 内。然后退出并重新登录就生效啦。

    sudo gpasswd -a ${your_user_name} docker

重启 docker 服务

    sudo service docker restart

切换当前会话到新 group, 或者关掉终端重新连接也会生效

    newgrp - docker


## 安装荔枝派开发镜像

可通过两种方式导入lichee-nano编译环境镜像

### 通过百度网盘下载并导入lichee-nano编译环境镜像

首先通过百度网盘下载[docker镜像](https://pan.baidu.com/s/1aYcGfzyz-g4CbxGSsVREGQ) ；
再将镜像加载到 docker：

``` 
gunzip nano.tar.gz
docker import nano.tar
```

### 通过docker官方仓库拉取lichee-nano编译环境镜像

``` 
docker pull zepan/licheepi-nano
```

### 镜像使用

- 载入镜像后查看镜像ID docker images
- 通过 id 运行某个命令 docker run xxxx-IMAGE-ID-xxx ls
- 后台运行 docker 并使用 ssh 去连接到镜像(6666端口) docker run -d -p 6666:22 xxxx-IMAGE-ID-xxx /usr/sbin/sshd -D

这样就安装并开启的容器ssh服务，只需连接主机的6666端口，以root用户，licheepi密码登录即可进行开发操作。

    ssh -p 6666 root@127.0.0.1

要停止该docker镜像时：

```
# 查看正在运行的容器
docker ps

# 根据 容器ID 进行停止
docker stop xxx-CONTAINER-ID-xxx
```

> **交流与答疑**
> 对于本节内容，如有疑问，欢迎到 [Docker使用与配置交流帖](http://bbs.lichee.pro/d/23-docker) 提问或分享经验。
