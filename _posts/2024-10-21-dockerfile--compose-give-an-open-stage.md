---
layout: post
title: "Dockerfile & compose give an open stage"
subtitle: "利用dockerfile 与 compose 文件缩短跨平台开发的配置"
date: 2024-10-21
author: "Dl"
header-img: "img/post-bg-2015.jpg"
tags: []
---

# Background
前两天是在ubuntu默认镜像下打容器，操作。镜像的修改在关闭后就不存在了。了解到了 dockerfile（有了使用场景，才有技术需要）。本文是记录 dockerfile 与 compose 合作搭建 arm 交叉编译的方法。

# Prepare
1. 将 需要安装的文件，不能联网的都放到一个文件下，统一安装。
2. - [] dockerfile中RUN执行 source 命令就会失败
3. - [] 交叉编译器 的路径，放到env中不识别，需要后续补充
   
## 时区修改 
- [] 时区修改，使用如下命令 但没有作用
docker cp /etc/localtime 0f2d0ffb7a41:/etc/localtime
docker exec -it 0f2d0ffb7a41 bash -c "echo 'Asia/Shanghai' > /etc/timezone"



# 执行命令
docker build -t  embed-test1 
vscode 配置docker 插件后可以直接attach 使用

# minicom 验证 U-boot 启动
## minicom 配置
```
minicom -s 设置 /dev/ttyUSB0 115200 
```

## usb
eject /dev/sda1 
eject /dev/sda
## minicom show nothing
