---
layout: post
title: "Docker engine& desktop | about security"
subtitle: "This is a subtitle"
date: 2024-10-19
author: "Dl"
header-img: "img/post-bg-2015.jpg"
tags: ["security","Docker"]
---

# 背景
利用 ubuntu 24 建立一个 ubuntu16 的系统环境，用16 来进行开发板的开发。

# 问题
在 docker 中搭建 NFS服务，在编辑 /etc/exports 文件后，重启 nfs 服务时不通过，原因是 docker 中的文件路径都进行了 encryption。 即使我的 yaml 文件中使用了 privileged = true. 为此，需要在 docker compose up -d 时，使用 sudo 权限运行。

在使用 sudo 运行 docker 命令时，遇到
```
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
```
/var/run/docker.sock 是docker context 的默认配置。但是我的电脑上没有这个文件。

在进一步搜索中发现，好像涉及到了 docker 的security 权限部分，
[security讨论网站](https://unix.stackexchange.com/questions/771525/is-it-possible-to-run-docker-engine-without-frequent-sudo-in-a-manner-as-secure)

根据[docker官方介绍](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user)，当前我的电脑只有在lucky 用户权限下通过docker-desktop 有权限获取 /var/run/docker.sock (不清楚是不是因为安装的时候使用的lucky用户)

### 排查过程
![groups查看当前用户组](/img/in-post/groups.png)
可以看出， docker 用户组下只有 x:997, 本身的lucky 用户不属于其中

[dockerForLinux](https://stackoverflow.com/questions/75134896/docker-context-ls-and-sudo-docker-context-ls-dont-have-same-setting-options) linux不需要GUI,only need docker(now named docker engine)
根据这篇记录，查看自己的 context ，可以看出 lucky 才具备通信资格，root 没有。
![context-error](/img/in-post/docker-context-error.png)
- [x] 已经将lucky加入到 docker 组中了，需要重启运行 docker run hello-world 验证

# 结论
1. docker 有很多product，如果是linux 系统，只需要关注一个叫做 docker-engine 的即可。参考[安装教程](https://docs.docker.com/engine/install/ubuntu/)安装
2. docker compose 限制了很多权限，是只安装到当前用户的，用systemctl --user start docker-desktop 才能启动，且用户间隔离。（猜测)
3. linux 下CLI 才是王道。
4. 补充[增加用户的方法](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user)
   
*good question*
NFS mounts as the docker "data-root" is not supported. This limitation is not specific to rootless mode.


# linux
```
netstat -tulpn 