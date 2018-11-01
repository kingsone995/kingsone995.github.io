### 1.基本准备工作
* 安装好PYTHON
* 安装好VS CODE
* 安装好QT5.8

### 2.下载基本源文件

从[这里](https://sourceforge.net/projects/pyqt/files/)下载到以下源文件（Windows应该下载.zip，macOS/Linux应该下载.tar.gz）

* sip-4.19.1.zip
* PyQt5_gpl-5.8.zip
* PyQt3D_gpl-5.8.zip
* QScintilla_gpl-2.10.zip

创建一个工作目录，把这些zip/tar包直接解压缩到这个工作目录里。这样会形成4个子目录。

最后，检查一下命令行环境，看看编译器（运行cl或者g++）和Qt是否能够找到（运行qmake）

* 现象：如果找不到qmake，后面的操作会提示如下错误：
  
```
Error: Use the --qmake argument to explicitly specify a working Qt qmake.
```

* 原因：qmake所在目录没有包含到环境变量PATH中，导致找不到qmake。

* 解决思路：用export指令临时把qmake对应路径加入到PATH中。

* 具体方法（以MAC下为例）：
```
export PATH=/Users/aaa/Qt5.8.0/5.8/clang_64/bin:$PATH
```
>注：上面aaa根据各自的用户名不同而不同
### 3.编译sip
用以下命令编译sip（在Windows/Visual Studio平台下，以下命令的make应用nmake代替）
```
$ cd sip-4.19.1
$ python configure.py
$ make
```

### 4.编译PyQt5
在Windows/Visual Studio平台下,用以下命令编译PyQt5
```
$ cd PyQt5_gpl-5.8
$ python configure.py --sip=..\sip-4.19.1\sipgen\sip.exe --sip-incdir=..\sip-4.19.1\siplib --disable=QtNfc
$ nmake
$ nmake install
```
在macOS/Linux下的命令
```
$ cd PyQt5_gpl-5.8
$ python configure.py --sip=../sip-4.19.1/sipgen/sip --sip-incdir=../sip-4.19.1/siplib --disable=QtNfc
$ make
$ sudo make install
```
（QtNfc因为固有bug，忽略不使用）
PyQt5安装位置为(每人均不同)：
```
/usr/local/Homebrew/Cellar/python@2/2.7.15_1/Frameworks/Python.framework/Versions/2.7/share/sip/PyQt5/
```

把刚才编译sip进行安装，否则不能进行下一步。
```
$ cd sip-4.19.1
$ sudo make install
```

### 5.编译PyQt3D
Windows/Visual Studio平台下,用以下命令编译PyQt3D：
```
$ cd PyQt3D_gpl-5.8
$ python configure.py --sip=..\sip-4.19.1\sipgen\sip.exe --sip-incdir=..\sip-4.19.1\siplib
$ nmake
$ nmake install
```
在macOS/Linux下的命令
```
$ cd PyQt3D_gpl-5.8
$ python configure.py --sip=../sip-4.19.1/sipgen/sip --sip-incdir=../sip-4.19.1/siplib
$ make
$ sudo make install
```

### 6.编译QScintilla2
* 首先编译QScintilla2：

在Windows下的命令
```
$ cd QScintilla_gpl-2.10\Qt4Qt5
$ qmake
$ nmake release
$ nmake install
```
在macOS/Linux下的命令：
```
$ cd QScintilla_gpl-2.10/Qt4Qt5
$ qmake
$ make
$ sudo make install
```
* 然后编译PyQt的QScintilla2

在Windows下的命令
```
$ cd QScintilla_gpl-2.10\Python
$ python configure.py --sip=..\..\sip-4.19.1\sipgen\sip.exe --sip-incdir=..\..\sip-4.19.1\siplib --pyqt-sipdir=..\..\PyQt5_gpl-5.8\sip --pyqt=PyQt5
$ nmake release
$ nmake install
```

在macOS/Linux下的命令：
```
$ cd QScintilla_gpl-2.10/Python
$ python configure.py --sip=../../sip-4.19.1/sipgen/sip --sip-incdir=../../sip-4.19.1/siplib --pyqt-sipdir=../../PyQt5_gpl-5.8/sip --pyqt=PyQt5
$ make
$ sudo make install
```

### 7.最后测试
写一个代码
```
import sys
from PyQt5.QtCore import *
from PyQt5.QtGui import *
from PyQt5.QtWidgets import *
from PyQt5.Qsci import QsciScintilla, QsciLexerPython


if __name__ == "__main__":
    app = QApplication(sys.argv)
    font = QFont()
    font.setFamily('Courier')
    font.setFixedPitch(True)
    editor = QsciScintilla()
    editor.setFont(font)
    lexer = QsciLexerPython()
    lexer.setFont(font)
    editor.setLexer(lexer)
    editor.show()
    editor.setText(open(sys.argv[0]).read())
    app.exec_()
```
保存为testgui.py

运行指令
```
python testgui.py
```
如果弹出如下窗口，那就大功告成了。
<center>
  <img src="https://raw.githubusercontent.com/kingsone995/kingsone995.github.io/master/python/pythongui.png"> 
</center>


>其他例子，在PyQt5_gpl-5.8/examples中也有，可自行测试

关于tar，具体请见笔记：[tar命令详解](https://app.yinxiang.com/shard/s3/nl/1318585/2f8da7e1-6db6-4516-a2b9-03ae3a0b79ca/)

tar -xzvf file.tar.gz //解压tar.gz

#### 其他信息，请参见帖子：
[1.知乎帖子:构建PyQt5.8/Python2.7](https://zhuanlan.zhihu.com/p/25561911)

[2.个人博客：Pyqt5 MacOS 环境搭建](http://blog.justbilt.com/2015/10/17/setup-pyqt5-on-mac/)
