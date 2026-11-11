
## 第 1 章：Python 基础

一旦你在系统上安装好软件，就可以开始用 Python 进行编程之旅了。我将从变量、字符串和关键字等基础知识开始。现在，你将学习并编写你的第一个 Python 程序，了解可以处理的不同数据、如何使用变量以及关键字。让我们从基础开始，立刻开始编写代码。

### 关键字

|  |  |  |  |
|---|---|---|---|
| async | assert | as | and |
| def | from | nonlocal | while |
| continue | for | lambda | try |
| elif | if | or | yield |
| else | import | pass |  |
| global | not | with | del |
| in | raise | False | await |
| return | None | break | except |
| True | class | finally | is |

让我们从基础“Hello”程序开始，这是任何程序员的第一步。

```python
print("Hello, Welcome to Python Programming!")
```

当运行这段程序代码时，你的输出将是：

```text
Hello, Welcome to Python Programming!
```

Python 程序总是以 .py 扩展名结尾。让我们把这个程序保存为 Hello.py。请始终记得用示例的名称保存每个示例，以便在需要时能回想起它们。当你使用编辑器或 IDE 时，文件会由解释器运行，解释器会判断程序中使用的词。例如，在下面的程序中，解释器会看到括号中的内容，并打印括号内的内容。在编写 Python 代码的过程中，编辑器可能会高亮显示程序的某些部分。例如，它能识别出 print() 是一个函数名，并用特定颜色来区分它。但是，当它遇到“Hello, Welcome to Python Programming!”时，它会识别出这是 Python 程序代码，因此使用另一种颜色将其与其他代码区分开来。这个独特的功能称为语法高亮，对初学者很有用。

### 缩进与代码行

在 Python 中，没有像花括号那样的符号来表示函数和类的代码块。通常，代码块由行缩进表示，并且这种缩进会被严格执行。重要的是，缩进的空格数可以不同；但是，块中的每个语句必须使用相同的缩进量。例如，

```python
if False:
    print "False"
else:
    print "True"
```

然而，下面的语句块将产生错误：

```python
if False:
print "Result"
```

```python
file.write(file_text)
file.write("\n")
file.close()
fileName = raw_input("Enter filename: ")
if len(fileName) == 0:
    print "Next time input something"
    sys.exit()
try:
    file = open(fileName, "r")
except IOError:
    print "Error reading file requested"
    sys.exit()
fileText = file.read()
file.close()
print fileText
```

### 多行语句

这些语句通常以换行符终止。不过，Python 允许你使用特殊字符（\）来继续一条语句。请看下面的代码：

```python
Total_Number = number1 + \
    number2 + \
    number3
```

尽管如此，如果此类语句包含括号，如 ()、{} 或 []，则存在例外情况。例如：

```python
months = ['December', 'November', 'October', 'September', 'August',
          'July', 'June', 'May', 'April', 'March', 'February', 'January']
```

### 变量

变量是一个存储位置，并且有一个分配给它的名称。在 Python 中，我们可以为变量赋值并在之后引用这些变量。我相信一个例子会让事情更清楚。还记得我们的第一个程序（hello.py）吗？让我们再添加两行。请看下面的程序：

```python
outcome = "Hello, Welcome to Python Programming!"

print(outcome)
```

当你运行该程序时，输出将与之前相同，即：

```text
Hello, Welcome to Python Programming!
```

唯一的区别是我们添加了一个名为“outcome”的变量。每个变量总是有一个分配给它的值。在这种情况下，“outcome”的值是“Hello, Welcome to Python Programming!”

让我们在前面的代码中再添加两行。不过，在添加新代码之前，请确保在第一个代码中插入一个空行。

```python
outcome = "Hello, Welcome to Python Programming!"
print(outcome)

outcome = "Hello, Welcome to Learning Python!"
print(outcome)
```

添加这两行后，保存文件并再次运行程序。你的输出将如下所示：

```text
Hello, Welcome to Python Programming!

Hello, Welcome to Learning Python!
```

### 变量命名规则

在 Python 中命名变量时，有一些重要的规则需要遵守。如果你违反了其中任何一条规则，都会收到错误消息。因此，在编写程序时请务必牢记这些规则。

- 变量名只能包含数字、下划线和字母。你可以用下划线或字母开头；但不能以数字开头。例如，变量名可以是 outcome_1，但使用 1_outcome 是完全错误的。
- 变量名中不能包含空格。不过，你可以使用下划线来分隔两个单词。例如，outcome_program 可以正常工作；但 outcome program 会导致程序出错。
- 避免使用函数名和关键字作为变量名。
- 变量名在使用时应简短且具有描述性。例如，score 比 s 更可取，serial_name 比 sn 更好。

### 避免变量名错误

作为初学者，你会犯错误。专业人士也无法避免这种情况，但他们知道如何高效地处理这些错误。让我们来看一个你在开始 Python 编程课程时很可能会犯的错误。我会故意拼错“outcome”这个词来编写一段错误代码。

```python
outcome = "Hello, Welcome to Learning Python!"
#program will generate an error
print(outcom)
```

当出现此类错误时，Python 解释器会找出解决问题的最佳方法。一旦程序无法成功运行，它就会提供一个 traceback（回溯）。没有多少编程语言具备这种错误回溯功能。让我们看看解释器会如何响应我们上面的程序：

```text
Traceback (most recent call last):

    1. File "hello.py", line 3, in <module>
    2. print(outcom)
    3. NameError: name 'outcom' is not defined
```

第 1 行报告第 3 行存在错误，文件名为“hello.py”；解释器会快速识别该错误，并告诉我们第 3 行中错误的具体类型。在这种情况下，它会表示这是一个名称错误。此外，它会报告我们的变量没有被正确定义。每当你看到名称错误时，都意味着存在拼写错误，或者我们没有为变量设置值。不过，在本例中，这是一个拼写错误：我们的变量名中没有包含字母“e”。

```python
outcome = "Hello, Welcome to Python Programming!"

print(outcome)
outcome = "Hello, Welcome to Learning Python!"
print(outcome)
```

程序输出将是：

```text
Hello, Welcome to Python Programming!

Hello, Welcome to Learning Python!
```

你必须明白，编程语言是严格的；然而，它们不关心拼写的好坏。因此，在创建变量名时，你无需考虑语法和拼写规则。

### 尝试练习

编写一个程序来完成以下事情。确保保存文件并遵循变量命名规则。

- 编写一个程序，将一个消息赋值给你选择的变量名，然后打印该消息。
- 在第二个程序中，更改值并使用一条新消息，然后打印该消息。
- 从下面的列表中勾选错误的变量名。
  - 1_school
  - Fred Love
  - Fred_love
  - _exercises
  - Firsttwoletters

### Python 中的数据类型

在编写代码时，我们需要将数据存储到内存中。这些数据不能存储在同一个内存中，因为数字与字母不同。例如，人的姓名是字母；地址可以是字母数字字符；年龄可以存储为数值。Python 提供了数据类型来定义存储这些数据的不同操作和方法。Python 中有五种数据类型，分别是：

- 字符串
- 数字
- 元组
- 列表
- 字典

### 字符串

字符串是一系列用引号括起来的字符。在 Python 中，引号中的任何内容都被视为一个独特的字符串。在 Python 中，单引号和双引号都可以用来构成字符串。

```python
'Hello World'
"Hello World"
```

如果运行这两条语句，它们会产生相同的输出。

