### linux下tun/tap虚拟设备的使用

---

[TOC]

#### 概述

- `A gateway to userspace`



#### 工作原理

- tun/tap 虚拟设备连接了 **网络协议栈** 与 **用户态进程**(区别于 物理网卡, 连接 网络与协议栈)
- 用户态进程 再通过 socket连接到 内核协议栈



#### 内核空间与用户空间交互方式

- socket | proc文件系统 | 设备文件
- tun/tap 就是利用设备文件实现 内核空间与用户空间的数据交互



#### 一张图说明问题

![](/home/wangpeng/Documents/LearningNote/pictures/tun-tap.png)



#### 如果不行那就两张

![](/home/wangpeng/Documents/LearningNote/pictures/tuntapveth.png)

#### 典型应用场景 - VPN

![](/home/wangpeng/Documents/LearningNote/pictures/vpn.png)



#### 参考资料

[tun/tap原理](blog.csdn.net/sld880311/article/details/77854651)