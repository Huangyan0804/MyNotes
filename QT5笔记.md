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





## 控件命令

### lineEdit

| 方法                 | 描述                                                         |
| -------------------- | ------------------------------------------------------------ |
| setAlignment()       | 按固定值方式对齐文本                                         |
|                      | Qt.AlignLeft：水平方向靠左对齐                               |
|                      | Qt.AlignRight:水平方向靠右对齐                               |
|                      | Qt.AlignCenter：水平方向居中对齐                             |
|                      | Qt.AlignJustify：水平方向调整间距两端对齐                    |
|                      | Qt.AlignTop：垂直方向靠上对齐                                |
|                      | Qt.AlignBottom：垂直方向靠下对齐                             |
|                      | Qt.AlignVCenter：垂直方向居中对齐                            |
| setEchoMode()        | 设置文本框的显示格式，允许输入的文本显示格式的值可以是：     |
|                      | QLineEdit.Normal：正常显示所输入的字符，此为默认选项         |
|                      | QLineEdit.NoEcho：不显示任何输入的字符，常用于密码类型的输入，且长度保密 |
|                      | QLineEdit.Password：显示与平台相关的密码掩饰字符，而不是实际输入的字符 |
|                      | QLineEdit.PasswordEchoOnEdit：在编辑时显示字符，负责显示密码类型的输入 |
| setPlaceholderText() | 设置文本框显示文字                                           |
| setMaxLength()       | 设置文本框所允许输入的最大字符数                             |
| setReadOnly()        | 设置文本为只读                                               |
| setText()            | 设置文本框的内容                                             |
| text()               | 返回文本框的内容                                             |
| setDragEnable()      | 设置文本框是否接受拖动                                       |
| selectAll()          | 全选                                                         |
| setFocus()           | 得到焦点                                                     |
| setInputMask()       | 设置掩码                                                     |
| setValidator()       | 设置文本框的验证器（验证规则），将限制任意可能输入的文本，可用的校验器为 |
|                      | QIntValidator:限制输入整数                                   |
|                      | QDoubleValidator:限制输入浮点数                              |
|                      | QRegexpValidator:检查输入是否符合正则表达式                  |

**QLineEdit类中常用信号如下**

| 信号             | 描述                               |
| ---------------- | ---------------------------------- |
| selectionChanged | 只要选择改变了，这个信号就会发射   |
| textChanged      | 当修改文本内容时，这个信号就会发射 |
| editingFinished  | 当编辑文本结束时，这个信号就会发射 |

**定义输入掩码的字符**
下表列出了输入掩码的占位符和字面字符，并说明其如何控制数据输入

| 字符 | 含义                                              |
| ---- | ------------------------------------------------- |
| A    | ASCII字母字符是必须输入的（A-Z，a-z）             |
| a    | ASCII字母字符是允许输入的，但不是必须输入的       |
| N    | ASCII字母字符是必须输入的（A-Z，a-z，0-9）        |
| n    | ASCII字母字符是允许输入的，但不是必须输入的       |
| X    | 任何字符都是必须输入                              |
| x    | 任何字符都是允许输入的，但不是必须输入的          |
| 9    | ASCII数字字符是必须输入的（0-9）                  |
| 0    | ASCII数字字符是允许输入的，但不是必须输入的       |
| D    | ASCII数字字符是必须输入的（1-9）                  |
| d    | ASCII数字字符是允许输入的，但不是必须的（1-9）    |
| #    | ASCII数字字符与加减字符是允许输入的，但不是必须的 |
| H    | 十六进制格式字符是必须输入的（A-F，a-f，0-9）     |
| h    | 十六进制格式字符允许输入，但不是必须的            |
| B    | 二进制格式字符是必须输入的（0,1）                 |
| b    | 二进制格式字符是允许输入的，但不是必须的          |
| >    | 所有字母字符都大写                                |
| <    | 所有字母字符都小写                                |
| ！   | 关闭大小写转换                                    |
| \    | 使用‘\’转义上面列出的字符                         |

***掩码由掩码字符与分隔符字符串组成，后面可以跟一个分号和空白字符，空白字符在编辑后会从文本删除的\***
掩码示例如下：

| 掩码                             | 注意事项                                      |
| -------------------------------- | --------------------------------------------- |
| 000.000.000.000;_                | ip地址，空白字符是‘_’                         |
| HH:HH:HH:HH:HH:HH;               | MAC地址                                       |
| 0000-00-00                       | 日期，空白字符是空格                          |
| >AAAAA-AAAAA-AAAAA-AAAAA-AAAAA;# | 许可证号，空白字符是‘_’，所有字母都转换为大写 |



### TextEdit

| 方法           | 描述                 |
| -------------- | -------------------- |
| setPlainText() | 设置多行文本框的内容 |
|toPlainText() |	返回多行文本框的文本内容|
|setHtml()|	设置多行文本框的文本内容为HTML文档，HTML文档是描述网页的|
|toHtml()	|返回多行文本框的HTML内容|
|clear()	|清除多行文本框的内容|
|append()	|追加文本|
|moveCursor()	|移动光标|

