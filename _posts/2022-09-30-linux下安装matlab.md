---
layout:     post
title:      ubuntu下安装 matlab 超迅猛攻略
subtitle:   学习
date:       2022-09-30
author:     simplex
header-img: img/page_back.jpg
catalog: true
mathjax:  true
tags:
    - 学习	
---



# 问题描述



## 针对问题

在拥有 mathwork 许可账号的情况下，在 ubuntu 下安装matlab




## 解决方法

### I 下载镜像

从学校的[正版中心](https://nic.seu.edu.cn/fwzn/rjzbh/matlabzbh.htm)之类的网站，或者[官网](https://ww2.mathworks.cn/downloads/)下载。

```sh
wget xxxxx
```

下载完之后，将下载文件放到想要的文件夹，以 matlab 文件夹为例。如果是 .iso 文件，使用如下指令解压

```sh
7z x xxx.iso	
```



### II 下载能够使用 GUI 的远程连接软件

如 [mobaxterm](https://mobaxterm.mobatek.net/download.html)



### III 安装 matlab

进入目录，安装

```sh
cd matlab
./install
```



### IV (可选) 添加 matlab 二进制文件夹进入 PATH

执行一下指令，其中  `${Your Matlab Dir}` 表示你的 matlab 安装到的文件夹

```
echo 'export PATH="${Your_Matlab_Dir}/bin:$PATH"'>> ~/.bashrc
```



## 总结

安装的难点在于：下载能够使用 GUI 的远程连接软件，然后完成安装。只要工具用对就行了。



## 参考

Win10内置Ubuntu子系统图形化界面安装&中文方块乱码解决 https://blog.csdn.net/qq_43543789/article/details/104211359

Linux下安装Matlab https://blog.csdn.net/sunnysu99/article/details/122250219

还有一些没有用的网站



