title: Sublime Text,Latex和Skim on Mac（支持中文）
tag: 
- Sublime
- LateX
- Skim
- Mac
categories: Mac
date: 2015-03-04 23:00:00
---

前言
---
最近开始找实习，要修改一下简历，`Latex`之前也用过，但是没有做过简历，而且之前用`Latex`是在`Windows`上的`Ctex`，在`Mac`上没有用过，于是今天下午就开始准备在`Mac`上好好整理一下`Tex`，俗称环境配置。
显然这是一个碰壁的过程，博客上的信息比较冗余，而且受到版本更新的冲击，会发现很多地方不一样。最终还是查看官方文档，各种`google`，终于在`Mac`完成了自己的**中文简历**。
我主要还是**大自然的搬运工**，有问题的**欢迎交流讨论**。**同时请注意软件版本以及本blog的发布时间，如果时间太久请勿参考，如带来什么不便，敬请谅解。**

<!-- more -->

环境
---
### 系统
- **Macbook Pro with OS X Yosemite Version 10.10.2**

### 软件版本
- **MacTEX-2014 Distribution(MacTeX.pkg 25 May 2014)**
- **Sublime Text (Sublime Text Build 3065)**
- **Skim pdf reader(Version 1.4.10)**

安装
---
### STEP1 安装MacTeX
官网下载[MacTeX.pkg](http://www.tug.org/mactex/)安装即可，没有什么注意点，耐心就行。
### STEP2 安装Sublime Text
在[Sublime Text](http://www.sublimetext.com/)，至于是`ST2`或者`ST3`应该都是可以的，同时需要在`Sublime`上安装`Package Control`，接着再安装`Sublime`中的`LaTex`插件`LaTeXTools`。具体方法这里不在赘述，按照参考链接[Making your first PDF with LaTeX and Sublime Text 2 for Mac](http://economistry.com/2013/01/installing-and-using-latex-for-mac/)中的**Step1~Step4**操作即可。
### STEP3 安装SKIM
下载并安装[Skim](http://skim-app.sourceforge.net/)，正常安装，安装完之后，打开`Skim`，打开`Preferences`设置`Sync`中的`Preset`为对应的`Sublime Text`版本（我使用的`Sublime 3065`选择的是图中选项），这是新版的`Skim`支持的功能，而不需要去修改图中的命令脚本。
截图如下：
![Skim Preferences](http://img.blog.csdn.net/20150304221524250)

![Skim->Sync->Preset](http://img.blog.csdn.net/20150304221618931)
如此一来就连通了`Sublime`和`Skim`之间的同步，以及代码之间的相互指向。
到这一步为止已经可以使用`Sublime`和`Skim`编辑`LeTex`了，编译自动会调用`MacTex`。可以简单的测试一下，代码如下：
```
\documentclass{article}
\title{Title} 
\author{Your Name}
\begin{document}
\maketitle{}
\section{Introduction}
This is where you will write your content.\newline
$$\sum_{i=1}^n a_i=0$$
\end{document}
```
运行结果（`Sublime`编译快捷键`Command + b`）如下：
![test.tex运行结果](http://img.blog.csdn.net/20150304222459610)

### STEP 4 中文配置
我们现在在`Sulime Text`运行如下代码（注意这里加入了中文）：
```
\documentclass{article}
\usepackage{fontspec, xunicode, xltxtra}  
\setmainfont{Hiragino Sans GB}  
\title{Title}
\author{}
\begin{document}
\maketitle{}
\section{Introduction}
This is where you will write your content. 在这里写上内容。
\end{document}
```
得到如下错误：
```
[Compiling /Volumes/Mymac/tex/test2.tex]
TraditionalBuilder: Invoking latexmk... done.
Errors:
/usr/local/texlive/2014/texmf-dist/tex/latex/fontspec/fontspec.sty:41: !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! [ }]
```
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
这个时候原因已经很明显了，因为我们在安装配置完之后没有多编译引擎做任何更改，默认的是`latex`或者`pdflatex`，`log`文件中提供改成`xelatex`就可以了。这个就是问题的重点，网上很多博客上写的方法比较复杂，而且跟软件版本关系很大，我找到一个只需要在`tex`源文件的首行加入`%!TEX program = xelatex`即可。结果如下图：
![修正后结果](http://img.blog.csdn.net/20150304223825117)
这个时候在解析`tex`代码的时候会自动使用`xelatex`进行编译，使用过`tex`的应该知道`xelatex`的功能更强大一些。
### STEP 5 中文简历模板
这里提供一个- [Moderncv简历模板下载](http://www.ctan.org/tex-archive/macros/latex/contrib/moderncv)，也是比较知名的一个简历模板了，有中文和英文模板，该模板在下载下来之后直接打开`example`目录下的`template-zh.tex`是直接可以运行并出现中文的，因为它没有加上`fontspec.sty`，因此不需要在顶部加入代码`%!TEX program = xelatex`，然而，很多其他的中文简历模板都有引用`fontspec.sty`，因此需要加上改行。并且在`tex`文件中的字体说明**如果是中文需要修改成对应的英文单词**，参考博客中还有对应关系。例如：
```
\setsansfont{微软雅黑} 
需要改成
\setsansfont{Microsoft YaHei}
```
### 总结
博客确实不好写，先为`CSDN BLOG`支持`markdown`编辑点赞。那么我这里采用`Sublime Text`作为`Latex`的文本编辑器，首先编辑方便，这比`Texshop`好用多了，同时这支持不同编译引擎之间的切换，通过加入那行代码的加入，最重要的是你不用担心打开一个`tex`文件，首先源文件里面的中文有乱码，编译报错，或者编译结果中中文不显示等，甚至无法愉快的使用各种中文模板了。如果你碰到以上问题，那么不妨照着我说的步骤配置一下。
对了，这些快捷键要记住：
- **Command + b 编译**
- **Command + shift + click（鼠标左键） 在pdf上操作跳转到对应的源码位置**

参考链接
---

### 下载链接
- [MacTeX.pkg](http://www.tug.org/mactex/)
- [Sublime Text](http://www.sublimetext.com/)
- [Skim](http://skim-app.sourceforge.net/)

### 参考博客
- [Making your first PDF with LaTeX and Sublime Text 2 for Mac](http://economistry.com/2013/01/installing-and-using-latex-for-mac/)
- [Sublime Text 2 with LaTeX & Skim on Mac (XeTeX支援中文)](http://tech.marsw.tw/blog/2014/04/18/sublime-text-2-with-latex-skim-on-mac-xelatex-chinese-support/)
- [Using different engine doesn't work](https://github.com/SublimeText/LaTeXTools/issues/303)
- [LaTeXTools README FILE](https://github.com/SublimeText/LaTeXTools)
- [Moderncv简历模板下载](http://www.ctan.org/tex-archive/macros/latex/contrib/moderncv)
- [中文字体的英文名称](http://blog.sina.com.cn/s/blog_4b45a4ae0101e58w.html)
