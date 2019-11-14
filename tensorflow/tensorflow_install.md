## 概述
本文详细说明在Win10下如何安装TensorFlow开发环境

### 1.安装PYTHON3.7
如果没有安装PYTHON的同学，先从[https://www.python.org](https://www.python.org)网站下载相关安装包。我这次下载的是3.7.5.

### 2.安装Anaconda
此次下载的文件名为：Anaconda3-2019.10-Windows-x86_64.exe，网站要是上不去，可从其他地方搜索下载。
安装时候，建议安装到C:\programdata目录下，也就是自动提示的那个目录。

安装完成后需要为环境变量PATH增加两个路径。
一个是C:\ProgramData\Anaconda3\Scripts
另一个是C:\ProgramData\Anaconda3\Library\bin
修改环境变量方法：开始菜单-->windows系统-->控制面板-->系统和安全-->系统-->高级系统设置-->环境变量-->PATH-->编辑-->新建，把上面这两个依次加进去即可。

### 3.安装CUDA相关

运行tensorflow一般都要有GPU支持，如果没有GPU支持的同学，直接装CPU版本，有GPU的同学先安装CUDA相关。

* 首先是安装CUDA toolkit，这个可以到英伟达网站下载。本次下载的文件名为：cuda_10.1.243_426.00_win10.exe

* 接着安装cuDNN，本次下载的版本为cudnn-10.1-windows10-x64-v7.6.5.32.zip.
解压缩之后，把CUDA文件夹放到C:\Tools目录，把C:\Tools\CUDA\bin也加到环境变量PATH中

### 4.升级Anaconda3
这一步可以做一下，不过时间很漫长。

如果时间过长，可以把channel换到国内，这样会快些。


### 5.开始安装tensorflow

1. 在命令行中使用以下命令创建 conda 环境（如果使用 Windows，最好在命令行中以管理员身份执行）：
```
conda create -n tensorflow python=3.7
```
2. 激活 conda 环境
```
active tensorflow
（tensorflow）C:>
```
成功后就提示成下面这一行

3. 执行安装命令
```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple tensorflow-gpu
```
接下来又是漫长等待，

4. 