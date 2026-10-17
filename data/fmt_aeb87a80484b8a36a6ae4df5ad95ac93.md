
| :--- | :--- |
| * 纯文本: .txt,.csv | * 可执行文件: .exe,.dmg,.bin |
| * 源代码: .py,.html,.css,.js | * 图像: .jpg,.png,.gif,.tiff,.ico |
| * 数据: .json,.xml | * 视频: .mp4,.m4v,.mp4,.mov |
| | * 音频: .aif,.mp3,.mpa,.wav |
| | * 压缩: .zip,.deb,.tar.gz |
| | * 字体: .woff,.otf,.ttf |
| | * 文档: .pdf,.docx,.xlsx |

**图 10-1:** 常见的文本和二进制文件。

你可以使用 `VS Code` 或几乎任何代码编辑器来编写 Python 代码。我们在本章中使用 `VS Code` 仅仅是因为它的资源管理器面板（打开时在左侧）显示了你当前正在工作的文件夹内容。

## 打开和关闭文件

要从 Python 应用程序打开文件，使用以下语法：

```python
open(filename, mode)
```

将 `filename` 替换为你想要打开的文件名。如果文件与 Python 代码不在同一个目录中，你需要指定文件的路径。例如，如果你正在使用 Windows 并且想要打开桌面上的 `foo.txt`，且你的用户名是 Alan，你将使用路径 `C:\Users\Desktop\foo.txt`。

模式（`mode`）是可选的（用方括号表示）。使用它来指定你想要的访问类型，使用以下缩写：

- `r` (读取)：打开文件但不允许 Python 进行任何更改。这是默认模式，如果你没有指定模式，将使用它。如果文件不存在，Python 将抛出 `FileNotFoundError`。
- `r+` (读/写)：打开文件并允许 Python 对其进行读写。
- `a` (追加)：打开文件并允许 Python 在文件末尾添加内容，但不更改现有内容。如果文件不存在，此模式将创建文件。
- `w` (写入)：打开文件并覆盖其内容，如果文件不存在则创建文件。
- `x` (创建)：如果文件不存在则创建文件。你也可以指定：
- `t` (文本)：以文本模式打开文件。
- `b` (二进制)：以二进制模式打开文件。

你可以使用 `VS Code` 或几乎任何代码编辑器来编写 Python 代码。我们在本章中使用 `VS Code` 仅仅是因为它的资源管理器面板（打开时在左侧）显示了你当前正在工作的文件夹内容。

## 打开和关闭文件

要从 Python 应用程序打开文件，使用以下语法：

```python
open(filename, mode)
```

将 `filename` 替换为你想要打开的文件名。如果文件与 Python 代码不在同一个目录中，你需要指定文件的路径。例如，如果你正在使用 Windows 并且想要打开桌面上的 `foo.txt`，且你的用户名是 Alan，你将使用路径 `C:\Users\Desktop\foo.txt`。

模式（`mode`）是可选的（用方括号表示）。使用它来指定你想要的访问类型，使用以下缩写：

- `r` (读取)：打开文件但不允许 Python 进行任何更改。这是默认模式，如果你没有指定模式，将使用它。如果文件不存在，Python 将抛出 `FileNotFoundError`。
- `r+` (读/写)：打开文件并允许 Python 对其进行读写。
- `a` (追加)：打开文件并允许 Python 在文件末尾添加内容，但不更改现有内容。如果文件不存在，此模式将创建文件。
- `w` (写入)：打开文件并覆盖其内容，如果文件不存在则创建文件。
- `x` (创建)：如果文件不存在则创建文件。你也可以指定：
- `t` (文本)：以文本模式打开文件。
- `b` (二进制)：以二进制模式打开文件。

你可以使用 `VS Code` 或几乎任何代码编辑器来编写 Python 代码。我们在本章中使用 `VS Code` 仅仅是因为它的资源管理器面板（打开时在左侧）显示了你当前正在工作的文件夹内容。

## 读取文件内容

在本章之前，你已经看到了如何使用 `.read()` 读取打开文件的内容。但那并不是读取文件的唯一方法。你有三个选择：

- `read([size])`：如果括号为空，则读取整个文件。如果你在括号内指定了大小，它将读取许多字符（文本文件）或相应字节（二进制文件）。
- `readline()`：从文本文件中读取一行——行在遇到换行符处结束。
- `readlines()`：将文本文件的所有行读取到列表中。

示例代码如下：

```python
with open('quotes.txt') as f:
    # 读取整个文件
    content = f.read()
    print(content)
```

`content` 变量存储了文本文件的所有副本。文件每行末尾的换行符在打印时会开启新行。

这是使用 `readlines()` 而不是 `read()` 的相同代码：

```python
with open('quotes.txt') as f:
    content = f.readlines()
    print(content)
```

'我度过了一个非常奇妙的夜晚，但并不是这一个。

'格鲁奇·马克克斯', 《极限》。愚蠢与天才的区别在于，天才也有它的局限性。

'阿尔伯特·爱因斯坦', '我们来到地球都是为了帮助别人的；而其他人来到这里是为了什么，我无所知。'

'W. H. 奥登', '以介词结尾句子是件我无法接受（not put out）的事情。'

'温斯顿·丘尔威尔']

输出周围的方括号告诉你是这是一个列表。列表中的每个项目都用引号括起来并用逗号分隔。每个项目末尾的 `\n` 是在文件中结束该行的换行符。

与 `readlines()`（复数形式）不同，`readline()` 仅从文件中读取一行。该行从文件的当前位置延伸到下一个换行符。再次执行另一个 `readline()` 会读取文件的下一行，依此类推。例如，假设你运行了以下代码：

```python
with open('quotes.txt') as f:
    content = f.readline()
    print(content)
```

输出结果

> 我度过了一个非常奇妙的夜晚，但并不是这一个。

在此之后执行另一个 `readline()` 将读取下一行。正如你可能猜到的，当涉及到 `readline()` 和 `readlines()` 时，你可能想使用循环来访问所有数据，从而获得更多的控制权。

## 遍历文件

你可以使用 `readlines()` 或 `readline()` 来遍历文件。`readlines()` 方法总是一次性读取整个文件。因此，如果文件很大，在读取完文件之前，你的计算机可能会耗尽内存（RAM）。但如果你知道文件的大小且它相对较小（可能是几千行数据或更少），`readlines()` 是获取所有数据的快速方法。这些数据将存储在列表中，因此你将遍历的是列表而不是文件。

## 使用 readlines() 循环

当你使用 `readlines()` 读取文件时，你是一次性将整个文件作为一个列表读取的。因此，你并不是在逐行循环遍历文件。相反，你遍历的是 `readlines()` 存储在内存中的项目列表。实现代码如下：

```python
with open('quotes.txt') as f:
    # 先读取所有行，然后进行循环。
    for one_line in f.readlines():
        print(one_line)
```

如果你运行这段代码，输出将是双倍间距，因为每个列表项目都以换行符结束，而 `print` 在每次循环时都会正常添加它自己的换行符。如果你想保留单倍间距，可以在 `print` 语句中添加 `end=''`（确保使用单引号或双引号，且周围没有空格）。

## 使用 readline() 循环

如果你不确定正在读取的文件的大小，或者运行应用程序的计算机内存有多大，那么使用 `readlines()` 读取整个文件可能是有风险的。如果没有足够的内存来容纳整个文件，程序在内存耗尽时将会崩溃。为了安全起见，你可以一次遍历一行遍历文件，这样在任何给定时间内内存中都只有文件的某部分内容。

要使用这种方法，你打开文件，读取一行并将其放入变量中。然后只要变量不为空（`while`），就继续循环文件。因为文件中的每一行都包含某些文本，在读取完最后一行之前，该变量都不会为空。以下是这种循环方法的代码：

```python
with open('quotes.txt') as f:
    one_line = f.readline()
    while one_line:
        print(one_line, end='')
        one_line = f.readline()
```

对于较大的文件，这种方法是可行的，因为在任何点都没有读取整个文件。由于你不是一次性读取整个文件，所以不需要担心内存问题。

## 使用 seek()移动指针

`seek()` 方法允许你将指针移动到特定位置。`whence` 参数决定了相对于何的位置：

- `0`：文件开头。
- `1`：当前指针位置。
- `2`：文件末尾。

如果你省略 `whence` 值，它默认认为 `0`。最常见的 `seek` 用法是将指针重置到文件顶部。

## 读取并复制二进制文件

假设你有一个二进制文件，你想为它创建一个副本。与其一次性打开它并导致内存耗尽，你可以分块读取并分块写入。二进制文件没有“行”。所以 `readline()` 不是遍历的良好选择，但你可以使用指定大小的 `read()`。

```python
## 指定要复制的文件
file_to_copy = 'happy_pickle.jpg'
## 在扩展名之前添加 _copy 创建新文件名。
name_parts = file_to_copy.split('.')
new_file = name_parts[0] + '_copy.' + name_parts[1]
## 以只读二进制模式打开原始文件。
with open(file_to_copy, 'rb') as original_file:
  # 创建或打开文件写入
  with open(new_file,'wb') as copy_to:
    # 获取原始文件的块数据（4KB）。
    chunk=original_file.read(4096)
    # 循环直到没有更多块。
    while len(chunk) > 0:
      copy_to.write(chunk)
      # 确保在循环中读取下一个块。
      chunk = original_file.read(4096)

## 循环结束后自动关闭，显示完成消息。
print('Done!')
```

**图 10-2：** `binarycopy.py` 文件可以复制任何二进制文件。

**图 10-3** 显示了运行代码的结果。终端仅显示 Done!。但正如你所见，文件夹中有一个名为 `happy_pickle_copy.jpg` 的文件。

## 图 10-3：运行 binarycopy.py 将 happy_pickle_copy.jpg 添加到文件夹。

![](img/be36b4e9a8416f1ae2a353bd745f71cb_141_0.png)

# 第 11 章

## 玩转 JSON 数据

**本章内容包括**

- 发现如何组织 JSON 数据
- 学习序列化
- 从 JSON 文件导入数据
- 将 Python 数据导出到 JSON

JavaScript Object Notation (`JSON`) 是一种面向对象的常用序列化格式。序列化格式通常是指用于将数据从一台计算机发送到另一台计算机的格式。然而，某些数据库（例如 Google Firebase 的免费实时数据库）也以 JavaScript Object Notation 格式存储数据。开头的 JavaScript 这个词有时会让人困惑，尤其是当你使用 Python 而不是 JavaScript 来编写代码时。别担心，这种格式起源于 JavaScript 世界，现在已成为广为人知的、适用于各种计算机和编程语言的通用格式。

在本章中，你将确切地了解什么是 JSON，以及如何从 JSON 导出和导入数据。如果你发现围绕 JSON 的所有术语让你感到不适，再次别担心。我们会先过所有的专业术语。正如你所看到的，JSON 数据的格式与 Python 数据字典几乎相同，因此没有多少新内容需要学习。此外，你已经拥有了免费的 Python JSON 模块，这使得处理 JSON 数据变得更加容易。

## 组织 JSON 数据

JSON 数据大致等同于 Python 中的数据字典，这使得 JSON 文件非常容易处理。将 JSON 数据与表格数据进行比较时可能是最容易理解的。例如，图 11-1 显示了 Excel 工作表中的一些表格数据。图 11-2 显示了相同数据转换为 JSON 格式后的样子。Excel 表格中的每行数据都已转换为 JSON 文件中的一个键值对字典。当然，还有许多大括号来表示该数据是一个对象。

| | | 出生年份 | 加入日期 | 是否激活 | 余额 |
|---|---|---|---|---|---|
| 全名 | | | | | |
| Angst, Annie | 1982 | 1/11/2011 | TRUE | $300.00 |
| Bonañas, Barry | 1973 | 2/11/2012 | FALSE | -$123.45 |
| Schadenfreude, Sandy | 2004 | 3/3/2003 | TRUE | $0.00 |
| Weltschmerz, Wanda | 1995 | 4/24/1994 | FALSE | $999,999.99 |
| Malaise, Mindy | 2006 | 5/5/2005 | TRUE | $454.01 |
| O'Postum, Ollie | 1987 | 7/27/1997 | TRUE | -$1,000.00 |
| Pusillanimity, Pamela | 1979 | 8/8/2008 | TRUE | $12,345.67 |

**图 11-1：** Excel 表格中的某些数据。

资源生成器

打开编辑器

people_from_exceljson

JSON_FILES

- firebase_hitcounts.json
- json_get_nokey.py
- json_get.py
- people_excel.csv
- people_excel.xlsx
- people_from_exceljson

```json
{
  "Full Name": "Angst, Annie",
  "Birth Year": 1982,
  "Date Joined": 40554,
  "Is Active": true,
  "Balance": 300
},
{
  "Full Name": "Bonañas, Barry",
  "Birth Year": 1973,
  "Date Joined": 40950,
  "Is Active": false,
  "Balance": -123.45
},
{
  "Full Name": "Schadenfreude, Sandy",
  "Birth Year": 2004,
  "Date Joined": 37683,
  "Is Active": true,
  "Balance": 0
}
```

**图 11-2：** 转换为 JSON 格式的 Excel 表格数据。

![](img/be36b4e9a8416f1ae2a353bd745f71cb_144_0.png)

> 提示 要将现有的 Excel 数据转换为 JSON，请从 Excel 菜单中选择文件 ⇒ 导出文件 ⇒ 另存为，并导出为 CSV（逗号分隔）。你可以使用类似的技术从 Google Sheets 和 Apple 的 Numbers 应用导出 CSV。获得 CSV 文件后，你可以使用 convertcsv.com 网站将其转换为 JSON。在网站上寻找“Convert CSV to JSON”选项，并按照屏幕上的说明进行操作。

从 Excel 导出数据只是创建 JSON 文件的方法之一。你还可以创建一个键值 JSON 文件，其中每块数据都有一个唯一标识其自身的键。（同一文件中的其他字典不能具有相同的键。）

```python
print(type(people))
```

Python 显示如下内容：

```
<class 'list'>
```

这一行告诉你该对象是 `list` 类的实例。换句话说，它是一个列表对象，尽管大多数人只会简单地称它为列表。

由于该对象是一个列表，你可以对它进行循环。在循环内部，你可以显示每个项的类型，如下：

```python
for p in people:
    print(type(p))
```

输出如下：

```
<class 'dict'>
<class 'dict'>
<class 'dict'>
<class 'dict'>
<class 'dict'>
<class 'dict'>
<class 'dict'>
```

这是一个非常有用的信息，因为它告诉你列表中的每个“人”（我们在代码中将其缩写为 `p`）都是一个 Python 字典。因此，在循环内部，你可以通过键（key）来分离每个值。例如，看这段代码：

```python
for p in people:
    print(p['Full Name'], p['Birth Year'], p['Date Joined'],
           p['Is Active'], p['Balance'])
```

运行这段代码将显示 JSON 文件中的所有数据，如下所示。这些数据来自之前图 11-1 中的 Excel 表格。
