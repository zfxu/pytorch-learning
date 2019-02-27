# 1. PyTorch 简介

## 1.1 认识 PyTorch

关于 Torch：

- 2002 年发布 Torch
- 2011 年发布 Torch7

关于 PyTorch：

在 2017年 1 月 18 日，Facebook 下的 Torch7 团队宣布 PyTorch 开源后就引来了剧烈的反响。PyTorch 是 Torch 在 Python 上的衍生版本。Torch 是一个使用 Lua 语言的神经网络库，Torch 很好用，但是 Lua 流行度不够, 所以 Facebook 开发团队将 Lua 的 Torch 移植到了更流行的语言 Python 上，推出了 PyTorch 。

PyTorch 是一个 Python 优先的深度学习框架，是一个和 TensorFlow，Caffe，MXnet 一样，非常底层的框架。

PyTorch 相比于 TensorFlow 的三大优势：

**(1) Python优先支持**

PyTorch 主推的特性之一，就是支持 Python（官方的提法：puts Python first）。因为直接构建自 Python C API，PyTorch 从细粒度上直接支持 Python 的访问。相比于原生 Python 实现，引入的新概念很少，这不仅降低了 Python 用户理解的门槛，也能保证代码基本跟原生的 Python 实现一致。事实上，开发者可以直接用原生 Python 代码扩展 PyTorch 的 operation。

而 TensorFlow 总有一种用 Python 调用 C++ 写的第三方动态链接库的感觉；写模型需要更多代码，无法贯彻 Python 的简约风格；而且写新的 operation 必须用 C++ 开发。

**(2) 动态图的良好支持**

TensorFlow 运行必须提前建好静态计算图，然后通过 feed 和 run 重复执行建好的图。但是 PyTorch 却不需要这么麻烦：PyTorch 的程序可以在执行时动态构建/调整计算图。相对来说，PyTorch 具有更好的灵活性。这得益于 PyTorch 直接基于 Python C API 构建的 Python 接口。

TensorFlow 饱受诟病的痛点就是只支持静态图模型。也就是说，在处理数据前必须预先定义好一个完整的模型。如果数据非常规整，那还好。但实际工程和研究项目中的数据，难免有一些边角的情况。很多项目，其实需要大量实验才能选择正确的图模型。这就很痛苦了。因此，很多项目转而采用了 PyTorch 等支持动态图模型的框架，以便在运行程序的时候动态修正模型。

**(3) 易于Debug**

PyTorch 在运行时可以生成动态图，开发者就可以在堆栈跟踪中看到哪一行代码导致了错误。你甚至可以在调试器中停掉解释器并看看某个层会产生什么。

## 1.2 PyTorch 的更新

2018 年 4 月 25 号，PyTorch 官方发布 0.4.0 版本，该版本的 PyTorch 有多项重大更新，其中最重要的改进是官方支持 Windows（详细改动见 Pytorch 官方 [GitHub](https://github.com/pytorch/pytorch/releases/tag/v0.4.0)）：

- Tensor/Variable 合并
- 零维张量
- 数据类型
- [迁移指南](https://blog.csdn.net/sunqiande88/article/details/80172391)
- Windows 支持
- C++ 扩展
- ONNX 改进 支持 RNN
- Bug修复与性能优化

2018 年 12 月 8 日，Pytorch1.0 正式发布，源码地址：https://github.com/pytorch/pytorch/releases。这次最新的 PyTorch1.0 有很多重大的更新，分布式更好用了，其实最重要的应该是 C++ 的前端支持，部署更方便，效率更高，使得 PyTorch 往产品化方面又迈进了坚实的一步。





# 2. PyTorch 安装

## 2.1 Windows下安装PyTorch

官网：https://pytorch.org/get-started/locally/

如果已经装了 Ananconda，不管是 `Python3.5`，`Python3.6` 还是 `Python3.7`，都可以选择对应的 cuda 版本，然后直接执行下面命令安装：

```xml
conda install pytorch torchvision cuda80 -c pytorch            #for cuda8
conda install pytorch torchvision -c pytorch                   #for cuda9
conda install pytorch torchvision cuda100 -c pytorch           #for cuda10
conda install pytorch-cpu torchvision-cpu -c pytorch           #for cpu version
```

注意：`Conda` 安装只支持 `Python3`，如果你的 Ananconda 是 `Python2` 版本，请用 `pip` 方式安装。

安装自己的平台和版本选择相应的选项，我这里选择了：

```xml
PyTorch Build：Stable(1.0)
Your OS：Windows
Package：Conda
Language：Python36
CUDA：None
```

然后给出的 Run this Command 为：`conda install pytorch-cpu torchvision-cpu -c pytorch`

安装过程中可能会出现如下报错：

```xml
CondaHTTPError: HTTP 000 CONNECTION FAILED for url <https://conda.anaconda.org/pytorch/win-64/pytorch-cpu-1.0.0-py3.6_cpu_1.tar.bz2>
Elapsed: -

An HTTP error occurred when trying to retrieve this URL.
HTTP errors are often intermittent, and a simple retry will get you on your way.
```

添加下 Conda 国内源，依次敲打如下命令：

```xml
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
conda config --set show_channel_urls yes
```

执行完毕，可以使用 everything 软件搜索文件`.condarc `，可以看到：

```xml
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
  - defaults
ssl_verify: true
show_channel_urls: true
```

换回默认源 ：

```xml
conda config --remove-key channels
```

注：在执行 `conda config` 命令的时候，会在当前用户目录下创建 `.condarc` 文件，可以观察 Anconada 源更换前后该文件内容的变化。

参考：[Windows下安装PyTorch1.0](https://blog.csdn.net/xiangxianghehe/article/details/86300773)

## 2.2 Linux(发行版Ubuntu)下安装PyTorch





## 2.3 Mac下的安装PyTorch