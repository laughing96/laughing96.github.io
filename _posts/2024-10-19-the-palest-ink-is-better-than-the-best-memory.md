---
layout: post
title: "The palest ink is better than the best memory"
subtitle: "docker 使用方法记录 - arm调试"
date: 2024-10-19
author: "Dl"
header-img: "img/post-bg-2015.jpg"
tags: [“arm环境搭建”]
---

# arm 系统环境配置
## images 获取
安装 docker engine


## container 创建

还是用命令行。冲。
```
services:
  app:
    image: ubuntu:16.04
    command: "/bin/bash"
    volumes:
      - ./:/swap
    environment:
      - PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    cap_add:
      - ALL
    container_name: embeed 
    tty: true
    privileged: true
volumes:
  arm-data:
```

此时 直接使用 docker 命令行
```
docker compose up -d #-d 表示后台运行
```

进入container 后, 寻找替代vi 的方式修改 etc/apt/source.list
```
apt-get install vim
apt-get install kmod
apt-get install minicom
apt-get install iputils-ping
apt-get install net-tools
apt-get install make
# NFS 服务
apt-get install nfs-kernel-server rpcbind（每装好）
##ssh
apt-get install openssh-server
#xz 文件解压
apt-get install xz-utils

```

当前目录与容器内的 /swap 目录是可以进行文件传输的。至此，进行开发的系统环境配置完毕。

- [] docker中使用 nfs 提示 加密 [nfs配置问题](https://forum.ubuntu.org.cn/viewtopic.php?p=840692)

# 开发环境

## 交叉编译器
仅仅列举部分有意思的指令
```
echo "export PATH=\$PATH:$(pwd)" >> /etc/profile #这样就是标准的
echo "export PATH=$PATH:$(pwd)" >> /etc/profile #这样会把PATH变量解析出来
echo "export PATH=$PATH:$pwd" >> /etc/profile #pwd 是命令，不是变量，所以为空

#相关库
apt-get install lsb-core lib32stdc++6

# verify
arm-linux-gnueabihf-gcc -v

```

## 开发板的内核移植
### U-BOOT 移植
### linux 内核移植
### 根文件系统移植