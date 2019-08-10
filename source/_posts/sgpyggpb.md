---
title: 屏蔽搜狗输入法广告方法
date: 2019-08-02 13:16:56
tags: 
  - Tools
  - SouGouPinYin
  - Rubbish
---

切输入法第一下卡顿、切下搜狗后明显感觉鼠标状态是繁忙、弹出搜狐新闻提示、后台会有一个pinyinup.exe 可能会引起全屏游戏后弹到桌面解决方案

<!-- more -->

将下面内容复制进reg文件中导入重启电脑即可。

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\ImeUtil.exe]
"Debugger"="c:\\windows\\temp\\P2P类.exe"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\PinyinUp.exe]
"Debugger"="c:\\windows\\temp\\P2P类.exe"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\SogouCloud.exe]
"Debugger"="c:\\windows\\temp\\P2P类.exe"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\showie.exe]
"Debugger"="c:\\windows\\temp\\P2P类.exe"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\SohuNews.exe]
"Debugger"="c:\\windows\\temp\\P2P类.exe"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\SGTool.exe]
"Debugger"="c:\\windows\\temp\\P2P类.exe"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\SGDownload.exe]
"Debugger"="c:\\windows\\temp\\P2P类.exe"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\SogouComMgr.exe]
"Debugger"="c:\\windows\\temp\\P2P类.exe"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\SogouExe.exe]
"Debugger"="c:\\windows\\temp\\P2P类.exe"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\SGSetc.exe]
"Debugger"="c:\\windows\\temp\\P2P类.exe"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\userNetSchedule.exe]
"Debugger"="c:\\windows\\temp\\P2P类.exe"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\crashrpt.exe]
"Debugger"="c:\\windows\\temp\\P2P类.exe"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\SogouFlash.exe]
"Debugger"="c:\\windows\\temp\\P2P类.exe"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\SeFastInstall.exe]
"Debugger"="c:\\windows\\temp\\P2P类.exe"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\SkinReg.exe]
"Debugger"="c:\\windows\\temp\\P2P类.exe"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\sgimeguard.exe]
"Debugger"="c:\\windows\\temp\\P2P类.exe"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\skinbox.exe]
"Debugger"="c:\\windows\\temp\\P2P类.exe"
```