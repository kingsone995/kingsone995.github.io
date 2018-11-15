### 用PYQT写一个空窗口


代码如下：
```
from PyQt5.QtWidgets import QApplication, QWidget
from PyQt5.QtCore import QT_VERSION_STR
from PyQt5.Qt import PYQT_VERSION_STR
from sip import SIP_VERSION_STR

if __name__=='__main__':
    import sys
    app=QApplication(sys.argv)
    w=QWidget();
    w.resize(640, 320);
    w.move(400, 200);
    w.setWindowTitle("Empty Window")
    w.show()
    print("Qt5 Version Number is: {0}".format(QT_VERSION_STR))
    print("PyQt5 Version is: {}".format(PYQT_VERSION_STR))
    print("Sip Version is: {}".format(SIP_VERSION_STR))

    sys.exit(app.exec_())
```


应该弹出如下窗口：
<center>
  <img src="https://raw.githubusercontent.com/kingsone995/kingsone995.github.io/master/python/gui1/empty windows.png"> 
</center>


同时，在命令行打印三行版本信息：
```
Qt5 Version Number is: 5.8.0
PyQt5 Version is: 5.8
Sip Version is: 4.19.1
```