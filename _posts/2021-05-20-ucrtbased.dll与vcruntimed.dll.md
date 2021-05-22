---
layout:     post
title:      ucrtbased.dll与vcruntimed.dll
subtitle:   学习
date:       2021-05-20
author:     simplex
header-img: img/page_back.jpg
catalog: true
mathjax:  true
tags:
    - 学习	
    - debug
---

# ucrtbased.dll与vcruntimed.dll

在做数字图像处理作业的时候，在X86下debug发现的问题，这两的dll没有

## 解决方案

使用everything 找到已有的ucrtbased.dll和vcruntimed.dll，一定是在x86下的，然后放到C:\Windows\SysWOW64上

成功编译运行

我的路径：

C:\Program Files (x86)\Windows Kits\10\bin\10.0.17763.0\x86\ucrt

H:\vs2017\VC\Redist\MSVC\14.16.27012\debug_nonredist\x86\Microsoft.VC141.DebugCRT

