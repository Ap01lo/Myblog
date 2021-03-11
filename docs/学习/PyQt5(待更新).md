

> 记于：2021/3/10
>
> 完成于：未完成

#### 工具

1. Sublime text 3
2. QT Designer



### PyQt5

## 设置主窗口

主窗口类型有三种

+ QMainWindow：包含菜单栏、工具栏、状态栏、标题栏
+ QWidget：什么都可以加(不知道用什么的时候就用这个)
+ QDialog：对话窗口的基类，没有菜单栏、工具栏、状态栏

```python
from PyQt5.QtWidgets import QApplication, QMainWindow, QWidget, QDialog
import sys
class MyWindow(QWidget):
	def __init__(self):
		super(MyWindow,self).__init__()
		# 添加窗口标题
        self.setWindowTitle('MainWindow')
		# 定义窗口大小
        self.resize(500,600)
        # 添加状态栏
        self.status = self.statusBar()
		self.status.showMessage('2 secends',2000)

if __name__ == '__main__':
	app = QApplication(sys.argv)
	w = MyWindow()
	w.show()
	sys.exit(app.exec_())

```

> 一般都使用面向对象的方式来实现一个窗口，给窗口里面添加原件就相当于给对象添加成员函数与属性，让他们一起运行。

窗口居中显示代码：

```python
def center(self):
    # 获取屏幕坐标系
	screen  = QDesktopWidget.screengeometry()
	# 获取屏幕尺寸
    size = self.geometry()
	# 计算左右间隔
    newLeft = (screen.width()-size.width())/2
	newRight = (screen.height()-size.height())/2
	# 移动位置
    self.move(newLeft,newRight)
```

退出程序：

```python
class MyWindow(QMainWindow):
	def __init__(self):
		super(MyWindow,self).__init__()
		# 添加按钮
		self.btn1 = QPushButton('Quit App')
		# 将按钮与命令链接
        self.btn1.clicked.connect(self.onClick_btn1)
		# 应用添加按钮的布局
        self.LayOut()

	def onClick_btn1(self):
		app = QApplication.instance()
		app.quit()

	def LayOut(self):
		layout = QHBoxLayout()
		layout.addWidget(self.btn1)
		mainFrame = QWidget()
		mainFrame.setLayout(layout)
		self.setCentralWidget(mainFrame)
```

窗口坐标获取：（三个区别没搞清楚）

```python
def onClick_btn1():
    # --
	print(f'w.x = {w.x()}') # 窗口横坐标
	print(f'w.y = {w.y()}') # 窗口纵坐标
	print(f'w.width = {w.width()}') # 工作区宽度
	print(f'w.height = {w.height()}') # 工作区高度
    # --
 	print(f'w.x = {w.geometry.().x()}') # 工作区横坐标
	print(f'w.y = {w.geometry.().y()}') # 工作区纵坐标
	print(f'w.width = {w.geometry.().width()}') # 工作区宽度
	print(f'w.height = {w.geometry.().height()}') # 工作区高度   
    # --
 	print(f'w.x = {w.frameGeometry.().x()}') # 窗口横坐标
	print(f'w.y = {w.frameGeometry.().y()}') # 窗口纵坐标
	print(f'w.width = {w.frameGeometry.().width()}') # 窗口宽度
	print(f'w.height = {w.frameGeometry.().height()}') # 窗口高度 
```

窗口与程序图标：

```python
from PyQt5.QtWidgets import QIcon

self.setWindowIcon(QIcon('path'))
```

添加空间提示信息：

```python
from PyQt5.QWidgets import QToolTip
from PyQt5.QtGui import QFont
# 设置字体
QToolTip.setFont(QFont('SansSerif',12))
# 给整个窗口设置提示信息
self.setToolTip('This is the App')
# 给元件设置提示信息
self.btn1.setToolTip('This is botton1')
```

## QLabel控件

常用属性：

`setAlignment()` 设置文本对齐方式

`setIndent()` 设置文本缩进

`text()` 获取文本内容

`setText()` 设置文本内容

`setBuddy()` 设置伙伴关系

`selectedText()` 返回所选择的字符

`setWordWrap()` 设置是否允许换行

```python
class MyWindow(QWidget):
	def __init__(self):
		super(MyWindow,self).__init__()
		self.initUI()

	def initUI(self):
		self.resize(1000,800)
		self.setWindowTitle('LabelTest')

		lab1 = QLabel(self)
		lab2 = QLabel(self)
		lab3 = QLabel(self)
		lab4 = QLabel(self)

		lab1.setText('<font color = green size = 12>Welcome Here</font>')
		lab1.setAutoFillBackground(True)
		palette = QPalette()
		palette.setColor(QPalette.Window, Qt.blue)
		lab1.setPalette(palette)
		lab1.setAlignment(Qt.AlignCenter)

		lab2.setText('<font color = blue size = 5>Following is a picture.')
		
		lab3.setAlignment(Qt.AlignCenter)
		lab3.setPixmap(QPixmap('./image/desktop.jpg'))

		lab4.setText('<font color = blue size = 6>Redemption')
		lab4.setAlignment(Qt.AlignRight)
		

		vbox = QVBoxLayout()
		vbox.addWidget(lab1)
		vbox.addWidget(lab2)
		vbox.addWidget(lab3)
		vbox.addWidget(lab4)

		lab2.linkHovered.connect(self.linkHovered_lab2)
		lab4.linkActivated.connect(self.linkActivate_lab4)
		self.setLayout(vbox)

	def linkHovered_lab2(self):
		print('Covering lab2')

	def linkActivate_lab4(self):
		print('Activating lab4')
```

#### 设置伙伴关系：

```python
def initUI(self):

	self.resize(500,200)
	nameLab = QLabel('&Name',self)
	passwardLab = QLabel('&Passward',self)
	
	nameLine = QLineEdit()
	passwardLine = QLineEdit()

	nameLab.setBuddy(nameLine)
	passwardLab.setBuddy(passwardLine)

	btnOK = QPushButton()
	btnOK.setText('OK')
	btnCancel = QPushButton()
	btnCancel.setText('Cancel')

	layout = QGridLayout()
	layout.addWidget(nameLab,0,0)
	layout.addWidget(nameLine,0,1,1,2)
	layout.addWidget(passwardLab,1,0)
	layout.addWidget(passwardLine,1,1,1,2)
	layout.addWidget(btnOK,2,1)
	layout.addWidget(btnCancel,2,2)
	self.setLayout(layout)
```

## QLineEdit控件

基本功能：输入单行文本

EchoMode：回显模式

+ Normal 模式
+ NoEcho 模式
+ Passward 模式
+ PasswardEchoOnEdit 模式

```python
def initUI(self):

	self.resize(500,200)
	Normal = QLineEdit()
	NoEcho = QLineEdit()
	Passward = QLineEdit()
	PasswardOnEcho = QLineEdit()

	Normal.setPlaceholderText('NormalMode')
	NoEcho.setPlaceholderText('NoEchoMode')
	Passward.setPlaceholderText('PasswardMode')
	PasswardOnEcho.setPlaceholderText('PasswardOnEcho')

	Normal.setEchoMode(QLineEdit.Normal)
	NoEcho.setEchoMode(QLineEdit.NoEcho)
	Passward.setEchoMode(QLineEdit.Password)
			PasswardOnEcho.setEchoMode(QLineEdit.PasswordEchoOnEdit)

	layout = QFormLayout()
	layout.addRow('Normal',Normal)
	layout.addRow('NoEcho',NoEcho)
	layout.addRow('Passward',Passward)
	layout.addRow('PasswardOnEcho',PasswardOnEcho)

	self.setLayout(layout)
```

#### 限制输入格式（小数，浮点，满足条件的字符串）

```python
def initUI(self):

	self.resize(500,200)
	IntLim = QLineEdit()
	DoubleLim = QLineEdit()
	StrLim = QLineEdit()

	IntLim.setPlaceholderText('IntLim')
	DoubleLim.setPlaceholderText('DoubleLim')
	StrLim.setPlaceholderText('StrLim')

	IntValidator = QIntValidator(self)
	IntValidator.setRange(1,99)
	IntLim.setValidator(IntValidator)

	DoubleValidator = QDoubleValidator(self)
	DoubleValidator.setRange(-1000,1000)
	DoubleValidator.setDecimals(3)
	DoubleLim.setValidator(DoubleValidator)

	reg = QRegExp('[a-zA-z0-9]+$')
	validator = QRegExpValidator(self)
	validator.setRegExp(reg)
	StrLim.setValidator(validator)

	layout = QFormLayout()
	layout.addRow('Int',IntLim)
	layout.addRow('Double',DoubleLim)
	layout.addRow('Str',StrLim)

	self.setLayout(layout)
```

#### 掩码

| A    | ASCII 字母字符是必须输入的（A-Z、a-z）                    |
| ---- | --------------------------------------------------------- |
| a    | ASCII 字母字符是允许输入的，但不是必需的（A-Z、a-z）      |
| N    | ASCII 字母字符是必须输入的（A-Z、a-z、0-9）               |
| n    | ASCII 字母字符是允许输入的，但不是必需的（A-Z、a-z、0-9） |
| X    | 任何字符都是必须输入的                                    |
| x    | 任何字符都是必须输入的，但不是必需的                      |
| 9    | ASCII 数字字符是必须输入的（0-9）                         |
| 0    | ASCII 数字字符是必须输入的，但不是必需的                  |
| D    | ASCII 数字字符是必须输入的（1-9）                         |
| d    | ASCII 数字字符是允许输入的，但不是必需的（1-9）           |
| #    | ASCII 数字字符或加减符号是允许输入的，但不是必需的        |
| H    | 十六进制格式字符是必须输入的，但不是必需的（A-Fa-f0-9）   |
| B    | 二进制格式字符是允许输入的，但不是必需的（0，1）          |
| b    | 二进制格式字符是允许输入的，但不是必需的（0，1）          |
| >    | 所有字母字符都大写                                        |
| <    | 所有字母字符都小写                                        |
| ！   | 关闭大小写字母转换                                        |
| \    | 使用'\\'转义上面列出的字符                                |

```python
def initUI(self):

	self.resize(500,200)
	Line1 = QLineEdit()
	Line2 = QLineEdit()
	Line3 = QLineEdit()

	Line1.setInputMask('000.000.000.000;#')
	Line2.setInputMask('HH-HH-HH-HH-HH-HH;#')

	layout = QFormLayout()
	layout.addRow('IP',Line1)
	layout.addRow('MAC',Line2)
	self.setLayout(layout)
```

