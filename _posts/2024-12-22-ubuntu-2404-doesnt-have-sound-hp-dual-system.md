---
layout: post
title: "ubuntu 24.04 doesn't have sound hp dual boot system"
subtitle: "consist"
date: 2024-12-22
author: "Dl"
header-img: "img/post-bg-2015.jpg"
tags: [ubuntu, sound]
---

# Solve solution
If your laptop is a dual boot system, my solve solution will be some valuable for you.
First, you should reboot your laptop and select the windows boot. 
Then you should shutdown the laptop and make the power off. (It's a feature named Hybrid Shutdown" or "Fast Boot since windows 8.)
Finally, power on your laptop and select the ubuntu system.Now you would find your sound is back. Enjoy.

# Principal 
1. Hybrid Shutdown : In my opinion, it will store some data that will accelerate the speed of windows. 
2. Linux users are advised to turn off hybrid shutdown , otherwise they will be unable to mount NTFS filesystems(because the current state of the NTFS filesystem is not stored on the NTFS partition, but held in the hibernated kernel memory)[1](https://askubuntu.com/questions/464388/no-sound-from-laptop-speakers-in-ubuntu-14-04-after-booting-into-windows-8-1)


# Other knowledge
1. ubuntu 24.04 now use pipewire, which will contradict pulseaudio. 
2. dmesg will output all messages that kernel needs.
3. /proc/asound/cards show device sound 
4. aplay -l 


# SomeThings
The right solution which I found was used wrong output. which means the output is right, but I don't know the meaning so I search it. Fortunately, I found the right answer.
This is life. AH.