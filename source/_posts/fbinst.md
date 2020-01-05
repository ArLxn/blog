---
title: 使用Fbinst工具创建UEFI+BIOS启动盘
date: 2019-10-25 12:59:04
---

使用Fbinst tool 1.7工具创建属于自己的EFI+BIOS启动盘。

<!-- more -->

## 个人环境介绍

操作系统：Windows 8.1 Enterprise；
处理器架构：x64；
使用的移动存储设备：WDC400（外部转接硬盘盒）；
工具：Fbinst Tool 1.7。

## 备注

本例中作者由于手头没有U盘所以使用移动硬盘代替；

本文中提到“移动存储设备”、“存储设备”、“U盘”则代指的都是一个东西。

## 第一步：备份文件

这一步要求备份存储设备内的所有文件，因为FbinstTool会对存储设备进行全盘重新格式化。

格式化后数据无法恢复！！！

## 第二步：启动Fbinst Tool

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/1.webp)

Fbinst Tool的启动界面
<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/2.webp)

## 第三步：格式化存储设备

点击“启动设置”->“格式化”

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/3.webp)

在弹出来的对话框中，点选“强行格式”，UD扩展区一项填存储设备的所有剩余空间。

至于强行格式化是否有必要的问题，目前作者是一直点选了的。

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/4.webp)

稍候片刻，出现信息提示格式化成功后点击确定返回

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/5.webp)

返回之后发现文件列表多了一个文件，这个是对格式化前的mbr的备份，如果出错想还原可以将此文件复制出来还原，不需要则可以直接删除。

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/6.webp)

## 第四步：准备Grub和启动初步部署

首先先下载Grub4DOS的完整包，官网可下。

不过请注意，目前作者发现诸多问题，请务必下载图中版本0.4.6a确保与接下来操作相兼容。

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/7.webp)

下载好了直接解压就可以。

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/8.webp)

回到Fbinst，右键空白区域导入文件

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/9.webp)

找到刚才下载的Grub解压出来的文件夹，文件夹里有一个无扩展名的文件Grldr，导入这个文件。

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/10.webp)

点击顶栏Grub菜单，删除所有文字之后输入

```
timeout 60
gfxmenu (ud)/message
```

输入完成之后切记右键空白区域，点击保存！！！

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/11.webp)

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/12.webp)

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/13.webp)

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/14.webp)

## 第五步：导入启动必备的文件

导入一些镜像或者iso，具体取决于你的Grub语法水平而不是它支持什么文件

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/15.webp)

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/16.webp)

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/17.webp)

## 第六步：建立启动项

根据实际情况写入代码，这只是一个示例。

```
title Windows 8 PE (x64) by Lxn
map (ud)/8x64.iso (0xff)
map --hook
chainloader (0xff)

title Windows 7 PE (x86) by Lxn
map (ud)/7x86.iso (0xff)
map --hook
chainloader (0xff)

title CDLinux
map (ud)/cdl.iso (0xff)
map --hook
chainloader (0xff)
```

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/18.webp)

## 第七步：建立Storage存储区

怎么说呢，Storage这个名是我自己取的。

其实就是分出来一块区域给日常使用。

右键空白区域新建文件

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/19.webp)

大小那一栏想填多少填多少，不能超出剩余空间；文件名想改就改不想改就不改。

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/20.webp)

右键刚才创建的文件，加入分区表

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/21.webp)

然后你就会发现有一个新的分区已经上线了

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/22.webp)

----

## BIOS启动模式制作结束

截止至此，BIOS启动用的启动盘就已经全部完成了，

如果你不需要UEFI启动的话，接下来的教程可以全部跳过。

----

## UEFI 1：建立UEFI分区

采用上文第七步的方法创建一个EFI分区，名字就叫EFI.img就可以。

分区大小不必太大，能装下所有启动用的文件就可以了。

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/24.webp)

创建完成将他加入分区表使其可见。

注意：Windows 10 1809在Storage.img和EFI.img甚至更多映像加入分区表后全都可见（即在“此电脑”中可见），这种情况就不必先卸载Storage.img。

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/25.webp)

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/26.webp)

找到你做的PE的ISO文件，把所有东西都扔到EFI的分区里。

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/27.webp)

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/28.webp)

## UEFI2：配置分区表

按照下图中的序号指示操作即可

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/35.webp)

----

## UEFI制作完成

至此UEFI的制作也全部完成，接下来介绍一些常见的问题

----

## FAQ1：no enough space

描述：创建文件时按照下方显示的剩余空间建立镜像可是提示：无足够空间

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/29.webp)

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/30.webp)

解决：碎片整理即可

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/31.webp)

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/32.webp)

<fancybox>![](https://mobicoin.ltd/CDN/blog/fbinstPic/33.webp)

## FAQ2：QEMU无法测试UEFI启动

这个是QEMU的问题与我无瓜...