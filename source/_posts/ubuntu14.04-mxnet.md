title: Ubuntu14.04下mxnet编译安装
tag: 
- Ubuntu
- CUDA
- mxnet
- DeepLearning
categories: DeepLearning
date: 2015-12-24 11:00:00
---

前言
---
之前在`Ubuntu14.04`下安装了显卡驱动，该步骤已经记录，`CUDA7.0`的安装以后有需要的话再更新记录安装步骤，包括现在比较火的`Theano`的安装等。这里主要记录开源的`mxnet`的编译过程。现在`deeplearning`这么火，`python`那边一大推开源的库，`caffe`也用过一段时间，`torch`没有接触过，但是也积累了一定的用户量。这里`mxnet`也做的挺不错的，用的人比较多，我比较喜欢他们底层计算框架`mshadow C++`的写法。话不多说，直接开始编译，其实具体步骤官方文档上有，这里会更直白一些。
<!-- more -->

环境
---
### 系统
- **Ubuntu 14.04 LTS server 64bits**

### 硬件
- **Nvidia GeForce GTX TITAN X**

### 软件版本
- **Driver Version:352.68**
- **CUDA7.0 & cuDNN**
- **[mxnet](https://github.com/dmlc/mxnet)**

安装
---
### Before
`mxnet`核心是`C++`写的，所以需要在`Ubuntu`下先编译动态链接库，也就是`.so`文件。之后，如果想在`python`下面运行，那么需要编译`python egg`文件，这也是这里主要涉及的两个部分，`mxnet`支持`python`，`C++`，`matlab`和`R`等，我想这也是受欢迎的原因之一。

### STEP1 Prerequisites
- Nvidia驱动 CUDA7.0 cuDNN 自不必说。

- libatlas等安装。
```
sudo apt-get update
sudo apt-get install -y build-essential git libatlas-base-dev libopencv-dev
```

### STEP2 编译.so文件
- git clone mxnet
```
git clone --recursive https://github.com/dmlc/mxnet
cd mxnet
```

- 修改config文件，config文件可以修改的项目很多，按需取用，很好理解
```
cp make/config.mk .
vim config.mk
在文件末尾添加如下内容：
USE_CUDA=1  注释请去掉,需要cuda，不添加之后运行代码无法使用cpu
USE_CUDA_PATH=/usr/local/cuda 注释请去掉,cuda路径，不对的话需要修改
USE_CUDNN=1  注释请去掉,道理同cuda，如果已经装了那么就勾上
USE_BLAS=atlas  注释请去掉,atlas，也可以使用openblas等等
```

- 保存配置之后多线程编译
```
make -j16 
```

- 编译结束后，/mxnet/lib/出现libmxnet.so文件

### STEP3 编译python版本, 默认在mxnet目录下
- 在step2成功之后，打包python egg。
```
sudo apt-get install python-numpy
cd python/
sudo python setup.py install
```

- 设置pythonpath
```
echo 'export PYTHONPATH=~/mxnet/python' >>  ~/.bashrc
source ~/.bashrc
```

### STEP4 测试demo mnist, 默认在mxnet目录下
- without gpu
```
python example/image-classification/train_mnist.py
```

- with gpu
```
python example/image-classification/train_mnist.py --gpus 0
```

### 注意点
**在具体运行的时候可能出现`OpenCV is not available.`的提醒，一般情况下不用理会，因为用不到，如果需要使用的话，安装参考[教程](https://github.com/bearpaw/Install-OpenCV)**

参考链接
---
[MXNet官方Documentation](http://mxnet.readthedocs.org/en/latest/)
[OpenCV安装教程](https://github.com/bearpaw/Install-OpenCV)
