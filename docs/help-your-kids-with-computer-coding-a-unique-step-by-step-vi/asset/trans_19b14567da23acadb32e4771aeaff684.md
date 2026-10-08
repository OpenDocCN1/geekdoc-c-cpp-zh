
# Scratch 与 Python

Scratch 中使用的许多元素在 Python 中也会用到——只是看起来不同。以下是这两种语言的一些相似之处。

```python
print('Hello World!')
```

此积块会在气泡中显示消息

在此处输入你想发送的消息

![](img/72d218a7a73c4d4abc7be582ebd85385_88_0.png)

Hello World!

消息像这样显示在屏幕上

Hello World!

在 Scratch 中，“说”积块用于在屏幕上显示内容。

在 Python 中，一个名为 "print" 的命令用于在屏幕上显示文本。

- Scratch 中的打印
- Python 中的打印

开启画笔

重复内部的积块 24 次以画出一个圆

![](img/72d218a7a73c4d4abc7be582ebd85385_88_1.png)

让角色向前移动

```python
from turtle import *
pendown()
for n in range(24):
    forward(10)
    right(15)
```

让乌龟顺时针旋转 15 度

关闭画笔

![](img/72d218a7a73c4d4abc7be582ebd85385_88_2.png)

- Scratch 中的乌龟图
脚本使用“画笔落下”积块来移动猫角色并画一个圆。

- Python 中的乌龟图
Python 中也有乌龟。这段代码可以用来画圆。

![](img/72d218a7a73c4d4abc7be582ebd85385_88_3.png)

# 安装 Python

在使用 Python 编程语言之前，你需要在电脑上下载并安装它。Python 3 是免费的、易于安装的并且适用于 Windows PC、Mac 以及 Ubuntu 等 Linux 操作系统。

# 什么是 IDLE？

当你安装 Python 3 时，还会获得一个名为 IDLE（集成开发环境）的免费程序。IDLE 为初设计，包含一个基础文本编辑器，允许你编写和编辑 Python 代码。

> 专家提示

# 保存代码

在 Python 中保存工作时，你需要使用“文件 > 另存为...”菜单命令，这样就可以为文件命名。首先创建一个文件夹来存放所有文件。给文件夹起一个清晰的名字，例如“PythonCode”，并与电脑所有者协商存放位置。

# WINDOWS

- Windows

在下载 Python 之前，请检查你的电脑是什么种操作系统。如果你使用的是 Windows，请确认是 32 位还是 64 位版本。点击“开始”按钮，右键点击“电脑”，然后左键点击“属性”。然后选择出现的选项。

![](img/72d218a7a73c4d4abc7be582ebd85385_89_0.png)

# MAC

- Mac

如果你使用 Apple Mac，在安装 Python 之前请确认它拥有什么操作系统。点击左上角的苹果图标并选择“关于本机”。

# UBUNTU

- Ubuntu

Ubuntu 是一个免费的操作系统，工作方式与 Windows 和 Mac 类似。要了解如何在 Ubuntu 上安装 Python，请参阅第 91 页。

![](img/72d218a7a73c4d4abc7be582ebd85385_89_1.png)

![](img/72d218a7a73c4d4abc7be582ebd85385_89_2.png)

# Windows 版 Python 3

在 Windows PC 上安装 Python 3 之前，确保获得电脑所有者的许可。你可能还需要所有者在安装期间提供管理员密码。

- **访问 Python 官网**
在浏览器中输入以下地址打开 Python 网站。点击“Download”（下载）打开下载页面。

- **下载 Python**
点击适用于 Windows 的最新版本（以数字 3 开头），它通常位于列表顶部。

```
http://www.python.org
```
这是 Python 的 URL（网页地址）

如果你是 32 位 Windows，请选择此项：
- Python 3.3.3 Windows x86 MSI 安装程序
- Python 3.3.3 Windows x86-64 MSI 安装程序

不用担心具体的数字，只要开头是 3 即可

如果你是 64 位 Windows，请选择此项：

- **安装**
安装程序文件将自动下载。完成后，双击安装 Python。选择“install for all users”（为所有用户安装），并在提示处点击“next”（下一步），不要更改默认设置。

- **运行 Idle**
现在检查程序是否安装正确。打开“开始”菜单，点击“所有程序”，“Python”，然后选择“IDLE”。

![](img/72d218a7a73c4d4abc7be582ebd85385_90_0.png)

确保你选择了 Python 3

当 Python 安装时会出现 Windows 安装程序图标

![](img/72d218a7a73c4d4abc7be582ebd85385_90_1.png)

| Python 3.3 |
| :--- |
| IDLE (Python 图形界面) |
| Module Docs (模块文档) |
| Python (命令行) |
| Python Manuals (帮助手册) |
| Uninstall Python (卸载 Python) |

- **打开 Python 窗口**
打开一个类似下面的窗口。你现在可以编写代码了——只需在括号 `>>>` 之后输入。

| IDLE | File | Shell | Debug | Window | Help |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Untitled (无标题) | | | | | |
