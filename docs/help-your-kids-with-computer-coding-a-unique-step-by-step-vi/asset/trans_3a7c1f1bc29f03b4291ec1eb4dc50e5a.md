

# 输入代码

在新的代码窗口中输入这段文本。这是一条编写“Hello World!”单词的指令。

# 保存代码窗口

点击“文件”（File）菜单并选择“另存为”（Save As）。输入文件名“HelloWorld”并点击“保存”。

```python
print('Hello World!')
```

使用单引号

| IDLE | 文件 (File) | 编辑 (Edit) | 终端 (Shell) | 调试 (Debug) | 窗口 (Window) | 帮助 (Help) |
|---|---|---|---|---|---|---|
| 直 (Until) | 新窗口 (New Window) | | | | | |
| 打开 (Open) | | | | | | | | |
| 打开模块 (Open Module) | | | | | | | |
| 最近文件 (Recent Files) | | | | | | | |
| 类浏览器 (Class Browser) | | | | | | | |
| 路径浏览器 (Path Browser) | | | | | | | |
| 关闭 (Close) | | | | | | | |
| 保存 (Save) | | | | | | | |
| 另存为 (Save As) | | | | | | | |
| 另存为副本 (Save Copy As) | | | | | | | |

![](img/72d218a7a73c4d4abc7be582ebd85385_94_0.png)

点击此处保存文件

# 运行程序

在代码窗口中点击“运行”（Run）菜单并选择“运行模块”（Run Module）。这将在终端窗口中运行程序。

| IDLE | 文件 (File) | 编辑 (Edit) | 格式 (Format) | 运行 (Run) | 窗口 (Window) | 帮助 (Help) |
|---|---|---|---|---|---|---|
| HelloWorld | | | | | Python Shell | |
| print('Hello World!') | | | | | | | |
| 运行模块 (Run Module) | | | | | | | |

点击此处运行程序

# 终端窗口中的输出

查看终端窗口。当程序运行时，应该出现“Hello!”消息。你创建了你的第一段 Python 代码！

> 记住

# IDLE 的工作原理

在 IDLE 中始终遵循这三个步骤：编写代码、保存代码、然后运行。记住，未保存的代码将无法运行。如果你尝试这样做，会出现警告。

```python
>>>
Hello World!
>>>
```

消息出现时不会带引号

| 输入代码 (Enter code) | 保存 (Save) | 运行 (Run) |

## 错误

程序第一次运行可能无法工作，但它们总是可以修复的。当程序代码输入错误时，Python 将显示错误消息，告诉哪里出了问题。

## 代码窗口中的错误

当尝试在代码窗口中运行程序时，可能会看到弹出的窗口，其中包含错误消息（例如“SyntaxError”）。这些错误会阻止程序运行并需要修复。

另请查看
Bugs and 148-149 > 调试 (debugging)
接下来做什么？176-177 >

- 1. 语法错误 (Syntax error)
如果弹出带有“SyntaxError”消息的窗口，通常意味着代码中存在拼写错误或输入错误。

- 2. 错误高亮
点击弹出窗口中的“确定”，你将返回程序。错误处或附近会有红色高亮。仔细检查该行内容。

![](img/72d218a7a73c4d4abc7be582ebd85385_95_0.png)

```python
print('Hello World'!)
```

> 此处缺少一个引号
错误已高亮显示

### 专家提示：经典错误

某些错误特别容易发生。注意这些常见问题：

- **大写与小写：** 大小必须完全匹配。如果你写 "Print" 而不是 "print"，Python 将无法理解该指令。
- **单引号和双引号：** 不要混用单引号和双引号。所有的引号都需要匹配的结束引号。
- **减号和下划线：** 下划线可能会让减号 (-) 与下划线 (_) 混淆。
- **不同的括号：** 不同形状的括号，如 () 和 [] 用于不同的用途。使用正确的括号，并确保它们成对出现。

# 终端窗口中的错误

有时，终端窗口中会出现红色文本的错误消息。这将阻止程序运行。

# 名称错误 (Name error)

如果出现错误消息“NameError”，意味着 Python 无法理解使用的某个单词。如果错误在代码窗口的代码中，右键点击终端窗口中的错误消息并选择“跳转到文件/行”（Go to file/line）。

![](img/72d218a7a73c4d4abc7be582ebd85385_96_0.png)

代码中（代码窗口中）发现错误的行

回溯 (Traceback most recent call last):

```
File "C:\PythonCode\errors.py", line 1, in <module>
pront('Hello World!')
```
NameError: name 'pront' is not defined

| 剪切 (Cut) |
| 复制 (Copy) |
| 粘贴 (Paste) |
| 跳转到文件/行 (Go to file/line) |

Python 不理解的单词

点击高亮代码窗口中出现错误的行

# 修复错误

代码窗口中的错误行已高亮。输入了 "pront" 而不是 "print"。你可以编辑代码来修复错误。

```python
pront('Hello World!')
```

将其更改为 "print"

# 发现错误

使用这两页中的提示找到代码中出现错误的行，仔细检查该行。仔细检查该行。

