---
layout: post
title: "Arch install guide"
subtitle: "安装记录"
date: 2025-01-01
author: "Dl"
header-img: "img/post-bg-2015.jpg"
tags: []
---
# 背景

# 问题
1. 安装系统引导失败，导致启动后进入grub界面，而不是arch界面。
   
   pacman -K grub efibootmgr intel-ucode os-prober
   mkdir /boot/grub
   grub-mkconfig > /boot/grub/grub.cfg
   grub-install --target=x86_64-efi --efi-directory=/boot
   

'''
intel-ucode 更新驱动程序
os-prober 探测其它系统 
'''
2. 密码失败
   U盘在来一遍，挂载 root 区，之后 passwd 重置。


shadow is a dependency of base

# user management
1. usermod 修改 
2. useradd add user
3. userdel delete
4. passwd set password
5. crontab frequently periodically
   
# group management
1. user groups : ftp http games log 
2. system groups : dbus, root proc, kmem tty lp
3. pre system groups: audio video input disk storage  optical
4. unused groups : nobody user uuidd daemon bin power 