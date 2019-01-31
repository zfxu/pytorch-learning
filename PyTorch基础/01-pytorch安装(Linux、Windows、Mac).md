## (1)PyTorch在Windows下的安装

官网：https://pytorch.org/get-started/locally/

安装自己的平台和版本选择相应的选项，这里我选择了：

``` xml
PyTorch Build：Stable(1.0)
Your OS：Windows
Package：Conda
Language：Python36
CUDA：None
```

然后给出的 Run this Command 为：`conda install pytorch-cpu torchvision-cpu -c pytorch`

安装过程中可能会出现如下报错：

``` xml
CondaHTTPError: HTTP 000 CONNECTION FAILED for url <https://conda.anaconda.org/pytorch/win-64/pytorch-cpu-1.0.0-py3.6_cpu_1.tar.bz2>
Elapsed: -

An HTTP error occurred when trying to retrieve this URL.
HTTP errors are often intermittent, and a simple retry will get you on your way.
```

添加下 Conda 国内源，依次敲打如下命令：

``` xml
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
conda config --set show_channel_urls yes
```

执行完毕，可以使用 everything 软件搜索文件`.condarc `，可以看到：

``` xml
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
  - defaults
ssl_verify: true
show_channel_urls: true
```

（但问题还没解决，待之后再探究下~）

换回默认源 ：

``` xml
conda config --remove-key channels
```

注：在执行 conda config 命令的时候，会在当前用户目录下创建 `.condarc` 文件，可以查看更换源前后该文件内容的变化。



## (2)PyTorch在Linux(发行版Ubuntu)下的安装







## (3)PyTorch在Mac下的安装