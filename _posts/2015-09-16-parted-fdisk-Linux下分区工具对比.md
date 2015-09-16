---
layout: post
title:  
date:   2015-09-16 14:40:58
categories: devops
---

Linux下，分区工具最常用的大约就是`fdisk`了。但是由于MBR分区表最大只支持到2T，而在存储系统中，单个磁盘动辄4T的情况下，fdisk就显得无能为力了。也正是这种情况下，接触到了parted分区工具。便借此机会在此记录下parted，并将parted与fdisk作下对比。

首先，fdisk是`MBR`分区,而parted则是`GPT`分区。由于MBR分区表的最大可寻址的存储空间只有2TB，所以fdisk进行的分区，单盘最大只支持2T，这也便是我刚刚提到的问题。而MBR分区的另一个缺点在于，由于MBR中分区表只设计了四个表项的空间，所以只能有四个主分区。GPT分区则解决了这两个问题，GPT对分区的数目没有限制，而且，单个分区的磁盘大小达到了惊人的18EB(1EP=1024PB=1024*1024TB).

两者还有一个差异，即parted是一种实时分区工具，fdisk是一种非实时的分区工具。这句话的意思是parted的分区是在你执行分区命令的同时便已经开始执行了，而fdisk的分区执行是在你w保存时才开始的。使用parted的时候，操作需更谨慎一些。

大概介绍了两者之间的一些差异之后，下面再大概讲fdisk和parted两个命令的操作：


##fdisk的操作
```
locakhost# fdisk /dev/sdb    #查看盘
Command (m for help): m
Command action
   a   toggle a bootable flag
   b   edit bsd disklabel
   c   toggle the dos compatibility flag
   d   delete a partition
   l   list known partition types
   m   print this menu
   n   add a new partition
   o   create a new empty DOS partition table
   p   print the partition table
   q   quit without saving changes
   s   create a new empty Sun disklabel
   t   change a partition's system id
   u   change display/entry units
   v   verify the partition table
   w   write table to disk and exit
   x   extra functionality (experts only)
```


