---
title: 使用管理员权限运行批处理
date: 2019-07-24 21:57:07
tags: sys
---

在写批处理的时候发现一些人的电脑装的是正版的系统，默认会弹出来uac的那个框框。默认cmd执行的时候是不带任何权限的。如果执行的批处理命令需要管理员权限，那么命令执行将会失败。本文将讲述如何避免这种情况的出现。

<!-- more -->

写批处理的时候在**所有批处理命令**的最上方加入下列代码即可解决问题。

```bat
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
```