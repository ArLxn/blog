---
title: 【超详细！】vmWare搭建黑群晖
date: 2019-11-24 00:18:39
---

使用vmWare 15搭建一台黑群晖（第一期），本期主要讲述如何从零搭建一台基于vmware并属于自己的黑群晖。

<!-- more -->

## 配置

CPU: AMD A4-5300B
RAM: 4GB DDR3
操作系统：Windows 10 1809(LTSC 2019) x64
vmware：15（需要提前安装这里不再赘述）
网卡：板载千兆
（然而这些都不重要）
重要的是路由器，要求必须得开着DHCP并可以自动分配IP地址，如果不能的话Disk Station将会无法被找到。
当然全部配置完成之后可以再切换到没有DHCP的设备上。

## 一、准备阶段

### 1. 下载vmware安装黑群晖所用的启动盘和pat固件，并解压
这个固件的下载地址有空我会给出来。
<fancybox>![这里直接解压到D盘](https://mobicoin.ltd/syn-pic/1.png)</fancybox>

### 2. 启动vmware
这个没什么好解释的吧
<fancybox>![这个没什么好解释的吧](https://mobicoin.ltd/syn-pic/2.png)</fancybox>

### 3. 新建虚拟机
我是不是有点啰嗦
<fancybox>![我是不是有点啰嗦](https://mobicoin.ltd/syn-pic/3.png)</fancybox>

### 4. 选择自定义不然后面很多选项会被直接跳过
<fancybox>![嗯](https://mobicoin.ltd/syn-pic/4.png)</fancybox>

### 5. 点击稍后安装操作系统
事实上你只能选这个
<fancybox>![事实上你只能选这个](https://mobicoin.ltd/syn-pic/5.png)</fancybox>

### 6. 选择Linux 3.x x64
<fancybox>![嗯。](https://mobicoin.ltd/syn-pic/6.png)</fancybox>

### 7. 内存1GB就足够了
如果有其他需要比如需要运行大型的网络服务再说往上加内存的事
<fancybox>![如果有其他需要再说其他的](https://mobicoin.ltd/syn-pic/7.png)</fancybox>

### 8. 网络类型这步很重要，必须选桥接模式
如果不选桥接模式接下来会非常麻烦
<fancybox>![如果不选桥接模式接下来会非常麻烦](https://mobicoin.ltd/syn-pic/8.png)</fancybox>

### 9. 磁盘类型选SATA
磁盘类型只能选SATA，其他的IDE太古老，剩下的都不支持
<fancybox>![理论上nvme也支持但没试过](https://mobicoin.ltd/syn-pic/9.png)</fancybox>

### 10.添加磁盘这步选择已有磁盘，并选择刚才下载的启动盘
vmdk那个就是，注意别点错了就成
<fancybox>![使用现有磁盘](https://mobicoin.ltd/syn-pic/10.png)</fancybox>
<fancybox>![vmdk那个就是](https://mobicoin.ltd/syn-pic/11.png)</fancybox>

### 11.转换格式这步选择不转换格式
转换格式之后启动盘会直接废掉
<fancybox>![转换格式之后启动盘会直接废掉](https://mobicoin.ltd/syn-pic/12.png)</fancybox>

### 12.全部完成之后点击编辑虚拟机设置
这一步不是必须的但是可以节省系统性能。
<fancybox>![编辑配置](https://mobicoin.ltd/syn-pic/13.png)</fancybox>
没有特殊需要直接删除光驱声卡打印机。
当然DSM支持共享打印机，如果需要此功能可以保留打印机。
<fancybox>![移除就对了](https://mobicoin.ltd/syn-pic/14.png)</fancybox>
这是我的基础配置
<fancybox>![这是我的基础配置](https://mobicoin.ltd/syn-pic/15.png)</fancybox>

## 二、安装阶段

### 1. 启动虚拟机
等待出现Booting the Kernel之后等待大约一分钟
当然如果主机性能高的话可以适当缩短等待时间
<fancybox>![当然如果主机性能高的话可以适当缩短等待时间](https://mobicoin.ltd/syn-pic/16.png)</fancybox>

### 2. 找到Disk Station
这一步分成两个部分。
如果可以直接访问到路由器的后台管理页面，可以登录路由器后台，找到Disk Station，点开就可以看到DS的IP。
<fancybox>![17](https://mobicoin.ltd/syn-pic/17.png)</fancybox>
<fancybox>![这是我的DS的IP](https://mobicoin.ltd/syn-pic/18.png)</fancybox>

如果无法登录后台（例如学校或者企业的交换机）可以直接在浏览器里输入https://find.synology.com
这是个万能的方案，如果你懒得登录路由器的后台也可以使用此方案找到DS。

### 3. 安装DiskStation的操作系统
点击设置，开始安装系统
<fancybox>![他就这一个按钮...](https://mobicoin.ltd/syn-pic/19.png)</fancybox>
选择手动安装
<fancybox>![必须要手动安装不然的话在线安装会被发现是黑群晖，然后就会无限黑屏23333](https://mobicoin.ltd/syn-pic/20.png)</fancybox>
选择刚才下载的pat文件，点击立即安装
<fancybox>![burst!](https://mobicoin.ltd/syn-pic/21.png)</fancybox>
稍后DiskStation会将pat固件文件上传到vmware并且会在20分钟内全自动安装完成。
还是那句话，电脑性能高的话其实也很快。

## 三、配置阶段

### 1. 配置账户
用户名密码记住，毕竟黑群晖可没有Reset按钮
<fancybox>![按照屏幕提示填就行，这没什么好说的](https://mobicoin.ltd/syn-pic/22.png)</fancybox>

### 2. 更新这个选择手动安装，下面的两个勾也都点掉
<fancybox>![如果你不想让它炸的话就要这么做](https://mobicoin.ltd/syn-pic/23.png)</fancybox>

### 3. Quick Connect
黑群晖qc基本都炸了，可以碰碰运气，如果出现错误就直接跳过吧，反正qc也坑得很
<fancybox>![Quick Connect](https://mobicoin.ltd/syn-pic/24.png)</fancybox>

### 4. 完成
到这基本上就算是配置完了，后期还需要创建RAID用来存储文件。
<fancybox>![清爽吗？](https://mobicoin.ltd/syn-pic/25.png)</fancybox>

