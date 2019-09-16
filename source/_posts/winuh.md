---
title: Windows 7 及以上版本常用优化脚本
date: 2019-08-24 00:18:39
---

介绍几个常用的优化脚本和问题处理脚本
不定期更新

<!-- more -->

## 请注意：
## 本页面中绝大多数脚本只在官方原版系统中测试过
## 对于Ghost方式安装的系统本人不保证一定都有效和不出现任何问题
## 如果你有什么好的脚本也可以在下方留言区留下

## 1.Win8+安装.net 3.0

将以下命令中x换成你的挂载盘符
```cmd
dism /online /enable-feature /featurename:netfx3 /All /source:x:\sources\sxs /Limitaccess
```

## 2.卸载OneDrive

然鹅实测的时候局限性很大...
```cmd
@ECHO OFF
%SystemRoot%\SysWOW64\OneDriveSetup.exe /uninstall
RD "%UserProfile%\OneDrive" /Q /S
RD "%LocalAppData%\Microsoft\OneDrive" /Q /S
RD "%ProgramData%\Microsoft OneDrive" /Q /S
RD "C:\OneDriveTemp" /Q /S
REG Delete "HKEY_CLASSES_ROOT\CLSID\{018D5C66-4533-4307-9B53-224DE2ED1FE6}" /f
REG Delete "HKEY_CLASSES_ROOT\Wow6432Node\CLSID\{018D5C66-4533-4307-9B53-224DE2ED1FE6}" /f
END
```

## 3.Win7+右键没有新建选项

这个需要复制到txt并改成reg导入
```regedit
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\Background\shellex\ContextMenuHandlers\New]
@="{D969A300-E7FF-11d0-A93B-00A0C90F2719}"
```

## 4.Win7+桌面右下角显示版本号

讲真，只有未注册版本在会在桌面右下角显示版本号
```regedit
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Control Panel\Desktop]
"PaintDesktopVersion"=dword:00000001
```

## 5.Windows 8.1 安装完成之后删除安装缓存文件

Ghost系统无效
```cmd
dism.exe /online /cleanup-image /startcomponentcleanup
```

## 6.Windows 10 LTSC 图片查看器修复

实测部分版本导入后出现查看器异常无法看图的情况（常见于LTSC 2015）
```cmd
@echo off
>nul 2>&1 "%SYSTEMROOT%\system32\cacls.exe" "%SYSTEMROOT%\system32\config\system"
if '%errorlevel%' NEQ '0' (
goto UACPrompt
) else ( goto gotAdmin )
:UACPrompt
echo Set UAC = CreateObject^("Shell.Application"^) > "%temp%\getadmin.vbs"
echo UAC.ShellExecute "%~s0", "", "", "runas", 1 >> "%temp%\getadmin.vbs"
"%temp%\getadmin.vbs"
exit /B
:gotAdmin
if exist "%temp%\getadmin.vbs" ( del "%temp%\getadmin.vbs" )

FTYPE Paint.Picture=%SystemRoot%\System32\rundll32.exe "%ProgramFiles%\Windows Photo Viewer\PhotoViewer.dll", ImageView_Fullscreen %1

FTYPE jpegfile=%SystemRoot%\System32\rundll32.exe "%ProgramFiles%\Windows Photo Viewer\PhotoViewer.dll", ImageView_Fullscreen %1

FTYPE pngfile=%SystemRoot%\System32\rundll32.exe "%ProgramFiles%\Windows Photo Viewer\PhotoViewer.dll", ImageView_Fullscreen %1
```

## 7.防假死优化

```cmd
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Control Panel\Desktop]
"WaitToKillAppTimeout"=dword:00000000
```

## 8.管理员取得所有权

```regedit
Windows Registry Editor Version 5.00　　 

[HKEY_CLASSES_ROOT\*\shell\runas] 
@="管理员取得所有权" 
"NoWorkingDirectory"=""　　 
[HKEY_CLASSES_ROOT\*\shell\runas\command] 
@="cmd.exe /c takeown /f \"%1\" && icacls \"%1\" /grant administrators:F" 
"IsolatedCommand"="cmd.exe /c takeown /f \"%1\" && icacls \"%1\" /grant administrators:F"　　 
[HKEY_CLASSES_ROOT\exefile\shell\runas2] 
@="管理员取得所有权" 
"NoWorkingDirectory"=""　　 
[HKEY_CLASSES_ROOT\exefile\shell\runas2\command] 
@="cmd.exe /c takeown /f \"%1\" && icacls \"%1\" /grant administrators:F" 
"IsolatedCommand"="cmd.exe /c takeown /f \"%1\" && icacls \"%1\" /grant administrators:F"　　 
[HKEY_CLASSES_ROOT\Directory\shell\runas] 
@="管理员取得所有权" 
"NoWorkingDirectory"=""　　 
[HKEY_CLASSES_ROOT\Directory\shell\runas\command] 
@="cmd.exe /c takeown /f \"%1\" /r /d y && icacls \"%1\" /grant administrators:F /t" 
"IsolatedCommand"="cmd.exe /c takeown /f \"%1\" /r /d y && icacls \"%1\" /grant administrators:F /t"
```

## 9.强制更新组策略

```cmd
>nul 2>&1 "%SYSTEMROOT%\system32\cacls.exe" "%SYSTEMROOT%\system32\config\system"
if '%errorlevel%' NEQ '0' (
goto UACPrompt
) else ( goto gotAdmin )
:UACPrompt
echo Set UAC = CreateObject^("Shell.Application"^) > "%temp%\getadmin.vbs"
echo UAC.ShellExecute "%~s0", "", "", "runas", 1 >> "%temp%\getadmin.vbs"
"%temp%\getadmin.vbs"
exit /B
:gotAdmin
if exist "%temp%\getadmin.vbs" ( del "%temp%\getadmin.vbs" )
cls
gpupdate /force
echo 操作完成，按任意键退出
Pause >NUL
```

## 10.清楚图标缓存

``` cmd
@echo off
taskkill /f /im explorer.exe
CD /d %userprofile%\AppData\Local
DEL IconCache.db /a
start explorer.exe
```