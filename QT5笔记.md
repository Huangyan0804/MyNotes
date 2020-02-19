# PyQt5



## 安装

```bash
sudo apt install qt5-default  # 安装QT5
sudo apt install qttolls5-dev-tools  # 安装QT5 designer
```

python安装pyqt5，**需要先安装 sip库**

```
pip3 install sip
pip3 install pyqt5
```



## 使用Designer设计UI

[qt5 designer教程](https://levonfly.github.io/p/a0594c46.html)

使用 `pyuic5 xxx.ui -o xxx.py`生成py文件

在主程序下使用下面的代码：

```python
import sys
from PyQt5 import QtWidgets
from PyQT_Form import Ui_Form

class MyPyQT_Form(QtWidgets.QWidget,Ui_Form):
    def __init__(self):
        super(MyPyQT_Form,self).__init__()
        self.setupUi(self)

    #实现slot函数
    def slot(self):
        pass


if __name__ == '__main__':
    app = QtWidgets.QApplication(sys.argv)
    my_pyqt_form = MyPyQT_Form()
    my_pyqt_form.show()
    sys.exit(app.exec_())
```

