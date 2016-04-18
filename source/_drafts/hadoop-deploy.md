title: Ubuntu下Hadoop,Hbase和Hive分布式部署
tag: 
- ubuntu
- hadoop
- hbase
- hive
categories: bigdata
date: 2015-12-11 22:15:00
---

前言
---
技术是不断积累的过程，实践也一样，之前在实验室的系统上部署过很多次`hadoop`集群，在实验室自己的`wiki`上也有记录过，自己也把安装的过程写成了脚本，这次正好又要部署一遍，总结整理在此，`hadoop`等版本上没有更新到最新，如果有需要参考的请注意版本问题，这个问题不是很大，虽然版本等有差异，但是部署过程大体类同。同时，我是在实验室自己部署的`openstack`上搭建`hadoop`集群，省去了物理网络设置的问题，直接在`openstack`上创建虚拟机，并通过虚拟网络的连接，使其处在同一个网段即可。那么下面开始整个的`hadooop`的部署过程。

<!-- more -->

环境
---
###系统
- **Ubuntu 14.04.1 LTS**

###软件版本
- **Hadoop**
- **Hbase**
- **Hive**

安装
---
###STEP1 安装MacTeX


###STEP2 安装Sublime Text


###STEP3 安装SKIM


###STEP 4 中文配置
**查看`log`文件,`log`文件会自动在`.tex`同目录**下，我们可以看到如下结果：
```
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!
! Fatal fontspec error: "cannot-use-pdftex"
! 
! The fontspec package requires either XeTeX or LuaTeX to function.
! 
! You must change your typesetting engine to, e.g., "xelatex" or "lualatex"
! instead of plain "latex" or "pdflatex".
! 
! See the fontspec documentation for further information.
! 
! For immediate help type H <return>.
!...............................................  
```

###总结


参考链接
---

###下载链接
- [MacTeX.pkg](http://www.tug.org/mactex/)

###参考链接
- [中文字体的英文名称](http://blog.sina.com.cn/s/blog_4b45a4ae0101e58w.html)
