---
title: 使用Git提交更改的日志
author: ArLxn
categories: Git
tags: 
- Git
- Log
export_md: false
---

泫凝云前期准备工作


<!-- more -->

```bash

Lxn@Lxn-Desktop MINGW64 /d/aLxn/cloud
$ git init
Initialized empty Git repository in D:/aLxn/cloud/.git/

Lxn@Lxn-Desktop MINGW64 /d/aLxn/cloud (master)
$ git commit -m "first commit"
On branch master

Initial commit

nothing to commit

Lxn@Lxn-Desktop MINGW64 /d/aLxn/cloud (master)
$ git add .

Lxn@Lxn-Desktop MINGW64 /d/aLxn/cloud (master)
$ git add .

Lxn@Lxn-Desktop MINGW64 /d/aLxn/cloud (master)
$ git commit -m "test 4 pdf"
[master (root-commit) b5b09f6] test 4 pdf
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 "\346\224\277\346\262\273\345\260\217\350\200\2030403.pdf"

Lxn@Lxn-Desktop MINGW64 /d/aLxn/cloud (master)
$ git remote add origin git@github.com:ArLxn/NingCloud.git

Lxn@Lxn-Desktop MINGW64 /d/aLxn/cloud (master)
$ git push -u origin master
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 118.60 KiB | 339.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:ArLxn/NingCloud.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.

Lxn@Lxn-Desktop MINGW64 /d/aLxn/cloud (master)
$
```