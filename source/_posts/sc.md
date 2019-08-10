---
title: 使用sc在命令行中创建服务
date: 2019-08-02 12:59:04
tags: 
  - sys
  - Services
categories: 
  - sys
---

本文讲述如何使用sc在命令行中创建服务(Services)。

<!-- more -->

如下:在命令行模式下执行：        
```
sc create TestService binpath= "c:\in estapp.exe" displayname= "TestService" depend= Tcpip start= auto 
```
注意这里的格式，“=”后面是必须空一格的，否则会出现错误。在提示建立成功后，可以直接输入如下命令来启动服务，或者可以直接在“管理工具”的“服务”中直接启动。 
```net start TestService```

---

C:\Documents and Settings\Administrator>sc create 
描述: 
在注册表和服务数据库中创建服务项。 
用法: 
sc <server> create [service name] [binPath= ] <option1> <option2>... 
选项: 
注意: 选项名称包括等号。 
type= <own|share|interact|kernel|filesys|rec> 

       (默认 = own) 

start= <boot|system|auto|demand|disabled> 

       (默认 = demand) 

error= <normal|severe|critical|ignore> 

       (默认 = normal) 

binPath= <BinaryPathName> 

group= <LoadOrderGroup> 

tag= <yes|no> 

depend= <依存关系(以 / (斜杠) 分隔)> 

obj= <AccountName|ObjectName> 

       (默认 = LocalSystem) 

DisplayName= <显示名称> 

password= <密码> 