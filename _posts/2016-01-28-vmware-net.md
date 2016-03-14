---
layout: post
title:  "VMware网络模式"
date:   2016-01-28 23:03:54
categories: Linux	
---
* content
{:toc}


VMware提供了三种网络模式，分别是：

- bridged 桥接模式
- host-only 主机模式
- NAT 网络地址转换模式

### bridge 桥接模式

根据我的理解，VMware虚拟机创建的系统就相当于在局域网内多了一台机器，只要是处于同一网段的就可以做到与主机通信。

但是在这个模式下，需要我们自己给系统配置IP和子网掩码。

看到资料里说，如果要用虚拟机在局域网内新建一个虚拟服务器，为局域网内的用户提供网络服务，就应该用这个模式。

### host-only 主机模式

这个模式好像就是说虚拟系统和主机系统可以相互通信，但是并不是通过真实网络来通信。

虚拟系统的TCP/IP配置信息(如IP地址、网关地址、DNS服务器等)，都是由**VMnet1**(host-only)虚拟网络的DHCP服务器来动态分配的。（还看的不是太懂）

### NAT 网络地址转换模式

在这个模式下，虚拟机不用复杂的手工配置就可以直接通过主机访问公网。

AT模式下的虚拟系统的TCP/IP配置信息是由**VMnet8**(NAT)虚拟网络的DHCP服务器提供的，无法进行手工修改。（一样不是太懂）

又看到一点，说是只能虚拟机和互联网只能实现单通，也就是只能虚拟机访问互联网。

但是，好像都推荐用这个模式。。

----------

嗯，了解了虚拟网卡这个概念。

VMnet1~VMnet9呢，被称作虚拟交换机。VMnet1就是Host网卡，VMnet8就是NAT网卡。

关于这些虚拟网卡的网络地址规划表，看到一个合理的安排，可以每次都按照这个来设置。

就是从VMnet1：192.168.10.0（使用网段）24（子网掩码）开始，其中的10变成20、30……90。（额，有空把他变成表格的形式）。 
