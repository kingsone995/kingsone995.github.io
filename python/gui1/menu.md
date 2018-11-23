### 用PYQT写一个空窗口


代码如下：
```
import sys
from PyQt5.QtWidgets import QMainWindow, QTextEdit, QAction, QApplication
from PyQt5.QtGui import QIcon
 
 
class Example(QMainWindow):
     
    def __init__(self):
        super().__init__()
         
        self.initUI()
         
         
    def initUI(self):              
         
        textEdit = QTextEdit()
        self.setCentralWidget(textEdit)
 
        exitAction = QAction(QIcon(sys.path[0]+'/exit24.png'), 'Exit', self)
        exitAction.setShortcut('Ctrl+Q')
        exitAction.setStatusTip('Exit application')
        exitAction.triggered.connect(self.close)
 
        self.statusBar()
 
        menubar = self.menuBar()
        menubar.setNativeMenuBar(False) #MAC OS 需要特别增加这个语句
        fileMenu = menubar.addMenu('&File')
        fileMenu.addAction(exitAction)
 
        toolbar = self.addToolBar('Exit')
        toolbar.addAction(exitAction)
         
        self.setGeometry(300, 300, 350, 250)
        self.setWindowTitle('Main window')   
        self.show()
         
         
if __name__ == '__main__':
     
    app = QApplication(sys.argv)
    ex = Example()
    sys.exit(app.exec_())
```


应该弹出如下窗口,其中，图标图像各位可以自己设置，放在py同一个文件夹下面即可。
<center>
  <img src="https://raw.githubusercontent.com/kingsone995/python/master/step2/menu.png"> 
</center>
