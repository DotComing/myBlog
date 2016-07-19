title: Ubuntu14.04下Nvidia GTX显卡驱动安装
tag: 
- Ubuntu
- Linux
- Nvidia
- GPU
categories: Linux
date: 2015-12-19 15:00:00
---

前言
---
实验室有一块TITAN卡，昨天**显卡驱动**跪了。重新安装更新了一下显卡驱动，过程还是有点艰难，稍微记录一下。之前有过几次类似的问题了，Ubuntu下安装显卡(包括卸载)感觉还是有些麻烦。
<!-- more -->

环境
---
### 系统
- **Ubuntu 14.04 LTS server 64bits**

### 硬件
- **Nvidia GeForce GTX TITAN X**

### 软件版本
- **Driver Version:352.68**

安装
---
### Before
可能是之前的显卡驱动比较老，在更新某些安装包的导致显卡驱动无法支持而奔溃。我们这块主要是用来跑`Deeplearning`程序，结合`Caffe`, `Theano`和`Keras`使用。起因是运行`Theano`程序报错无法识别显卡,提示驱动是否安装并启动。`nvidia-smi`命令无法运行,因此基本上确定显卡驱动出问题了。马上还是着手重新安装。首先想到的是`google`和`stackoverflow`,确实也找到了靠谱的解决方案，想到的是显卡驱动应该有将近半年没有更换了，也正好升级一下，在引用的链接中找到了匹配的最新的驱动版本之后，也是根据链接里面的提示进行安装，非常顺利，这里对过程重新整理一遍。 

### STEP1 卸载显卡驱动
- 删除nvidia原来的驱动
```
sudo apt-get remove nvidia*
```

- 添加ppa的源，能下载到更多更新的安装包
```
sudo add-apt-repository -r ppa:xorg-edgers/ppa
sudo apt-get update
```

- 删除xorg的配置
```
sudo rm /etc/X11/xorg.conf.timestamp
```

- 重新安装GL
```
sudo apt-get --reinstall install libgl1-mesa-glx
```

- 卸载完毕，重启!!!
```
sudo reboot
```

### STEP2 安装显卡驱动
- 安装显卡驱动，注意版本的匹配。需要考虑GPU型号和ubuntu版本，如果没有添加ppa源请添加，方法见**STEP1**.
```
sudo add-apt-repository -r ppa:xorg-edgers/ppa
sudo apt-get update
```

- 安装显卡驱动和相关设置
```
sudo apt-get install nvidia-352 nvidia-settings
```

- 等待安装完毕，重启
```
sudo reboot
```

- 查看显卡状况命令如下
```
nvidia-smi
nvidia-smi -a
```
结果如下：
```
$ nvidia-smi
Sat Dec 19 17:12:15 2015
+------------------------------------------------------+
| NVIDIA-SMI 352.68     Driver Version: 352.68         |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX TIT...  Off  | 0000:04:00.0     Off |                  N/A |
| 25%   66C    P2    96W / 250W |    272MiB / 12287MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID  Type  Process name                               Usage      |
|=============================================================================|
|    0     12471    C   python                                         247MiB |
+-----------------------------------------------------------------------------+
```

参考链接
---
[Use Nvidia Graphics Drivers In Ubuntu/linux Mint For Best Performance](http://www.noobslab.com/2014/12/use-nvidia-graphics-drivers-in.html)
