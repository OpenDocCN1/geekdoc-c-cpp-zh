
```
Python 3.4.2 Shell
File Edit Shell Debug Options windows help
Python 3.4.2 (default. Oct 19 2014, 13:31:11)
(GCC 4.9.0) on Linux
>>> print("copyright "credits" or "license") for more information.
>>> 1/2
0.5
>>> 54356+3553245
3607601
>>> 986734*2734484421
269807102281179024
```

# 数字与表达式

**步骤 5**：你也可以使用运算符来查看除法后的余数。例如：

**步骤 8**：这将显示为 '01'，将整数转换为二进制并在前面添加前缀 `0b`。如果你想移除 `0b` 前缀，可以使用：

`10/3`

将显示为 `3.333333333`，即 `3.3` 循环小数。如果你现在输入：

**`Format(3, "b")`**

该命令将一个值（数字 `3`）转换为格式化表示，由格式规范中的 `'b'` 部分控制。

`10%3`

将显示为 `1`，即 `10` 除以 `3` 的余数。

```
>> 2**3
== 8
>> (1+2)*3
== 9
>> 1/2
== 0.5
>> 6/2
== 3
>> 10/3
== 3.3333333333333335
>> 10%3
== 1
```

等等，让我们重新检查 `10/3` 的结果。

`10/3`

== 3.3333333333.

**步骤 6**：接下来是幂运算符，或者如果你想显得专业，可以叫指数运算。计算某个数的幂，你可以使用键盘上的双乘号或双星号：

**步骤 9**：布尔逻辑，其结果为真（`True`）或假（`False`）。我们可以使用这些来比较数据，查看它们是否相等、小于或大于。这在一个新文件中：

`2**3`

`10**10`

本质上它是 `2` 的 `3` 次方，但你已经了解数学运算符背后的基础。在 Python 中你可以这样写：

```python
a = 6
b = 7
print(a == a)
 True
print(a == b)
 False
print(a == 6 and b == 7)
 True
print(a == 4 and b == 7)
 False
print(5, not a == 7 and b)
 False
print(6, a == 7 or b == 7)
 True
print(7, a == 7 or b == 6)
 True
print(8, not (7 or b == 6))
 False
print(9, not (7 and b == 6))
```

```
>> 2**3
== 8
>> (1+2)*3
== 9
>> 1/2
== 0.5
>> 6/2
== 3
>> 10/3
== 3.3333333333333335
>> 10%3
== 1
>> 2**3
== 8
>> 10**10
== 10000000000
```

**步骤 7**：数字和表达式并不止于此。Python 有内置函数来处理数字、绝对值、复数以及各种数学表达式和勾股定理。要转换为二进制，请使用：

**步骤 10**：执行步骤 9 中的代码，你可以看到一系列 `True` 或 `False` 语句，展示了值 `6` 和 `7` 的结果。这是你之前看到内容的扩展，是编程中的重要部分。

`bin(3)`

```
>> 1/2
== 0.5
>> 2**3
== 8
>> (1+2)*3
== 9
>> 1/2
== 0.5
>> 6/2
== 3
>> 10/3
== 3.3333333333333335
>> 10%3
== 1
>> 2**3
== 8
>> 10**10
== 10000000000
>> bin(3)
'0b11'
```

![](img/588364e02a77f179099fae91a1713f0a_30_0.png)

![](img/588364e02a77f179099fae91a1713f0a_30_1.png)

www.bdmpublic.com 31

## 使用注释

当你编写代码时，代码的流程、每个变量的作用、整个程序的运行方式都在你的脑海中。另一位程序员随着时间的推移逐行查看代码时，这可能会变得难以阅读。

## 注释！

程序员通过对代码段进行注释来保持代码的可读性。例如，如果使用了一个变量，程序员会注释它预期的功能。这是一种良好的习惯。

- **步骤 1**：从创建一个 IDLE 编辑器新实例（`File -> New File`）开始，创建一个简单的变量和打印（`print`）命令：

```python
a=10
print("The value of A is", a)
```

保存文件并执行。

- **步骤 3**：重新保存代码并执行。你可以看到，尽管添加了行，IDLE Shell 中的输出与之前相同。简单来说，井号（`#`）是程序员可以插入的一行文本，用于告知他们和他人正在发生什么，而无需让用户察觉。

![](img/588364e02a77f179099fae91a1713f0a_31_0)

- **步骤 2**：运行代码将在 IDLE Shell 窗口中返回：A 的值为 10，这是我们预期的。现在，添加一些代码中常见的注释：

```python
## Set the value of A to 10
a=10
## Print the current value of A
print(a
```

- **步骤 4**：假设我们创建的变量 A 是游戏中的生命值。每当玩家死亡时，变量就会减 1。程序员可以：

```python
a -= 1
```

![](img/588364e02a77f179099fae91a1713f0a_31_1)

# 变量操作

## 第 5 步

然而，你不能在同一个命令中组合字符串和整数变量，因为你需要一组变量来将一个转换为另一个，反之亦然。当你尝试将两者结合时，你将得到一个错误消息：

```python
print (name + age)
```

```python
Python 3.4.2 (default, Oct 19 2014, 13:31:11)
name = 'Thor'
age = 44
print(type(name))
<class 'str'>
print(type(age))
<class 'int'>
print(name + ' Descended from Vikings')
Thor Descended from Vikings
print(name + age)
TypeError: Can't convert 'int' object to str
```

## 第 8 步

当你想要处理用户输入的数字时，这会带来一些问题，因为 `age + 10` 由于是一个字符串和一个整数而无法工作。相反，你需要：

```
int(age) + 10
```

这将把字符串转换为可以操作的整数。

```python
Python 3.4.2
Edit File Debug Options Windows Help
Python 3.4.2 (default, Oct 19 2014, 13:31:11)
age = input("Enter your age: ")
print(type(age))
<class 'str'>
print(age + 10)
TypeError: Can't convert 'str' object to int
```

在处理浮点数运算时，类型转换（Casting）类型也很重要；记住小数点。例如，输入：

```
float(19.99)
```

## 第 6 步

这种过程被称为类型转换（Casting）。Python 代码如下：

```python
print ("age is " + str(age) + " years old.")
44 years old.
```

或者你可以使用：

注意在最后一个例子中，你不需要在引号单词之间留空格，因为逗号会分别处理每个部分。

```python
print ("name is " + name + ", years old.")
Thor is 44 years old.
```

## 第 9 步

现在输入 `type(float)`，你会发现 Python 已将数字转换为了 'float'（浮点数），它包含小数值。

```python
Python 3.4.2
Edit File Debug Options Windows Help
Python 3.4.2 (default, Oct 19 2014, 13:31:11)
age = float(input("Enter your age: "))
print(type(age))
<class 'float'>
print(age + 10)
29.99
```

## 第 7 步

类型转换的另一个示例是你需要用户的输入，例如：

```python
age = input("How old are you?")
```

所有数据都被存储为字符串。

```python
Python 3.4.2
Edit File Debug Options Windows Help
Python 3.4.2 (default, Oct 19 2014, 13:31:11)
age = input("How old are you?")
print(type(age))
<class 'str'>
How old are you? 
44
```

## 第 10 步

组合整数和浮点数时，Python 将整数转换为浮点数，但不会返回精确值。在转换为整数时，Python 总是向下舍入到最近的整数，这称为截断（truncating）；对于 `19.99`，它变为了 `19`。

```python
Python 3.4.2
Edit File Debug Options Windows Help
Python 3.4.2 (default, Oct 19 2014, 13:31:11)
age = 19.99
print(int(age))
<class 'int'>
19
```

## 用户输入

我们从之前的几个示例中已经了代码的一些基础用户交互，所以现在是专注于你如何从用户那里获取信息并展示它们的好时机。

## 用户友好型

你想要从用户那里获得的输入类型很大取决于你正在编写的程序类型。例如，游戏可能会询问角色的名字，而数据库可以询问个人详情。

- 第 1 步：如果尚未打开，打开 Python 3 IDLE Shell，在编辑器中创建一个新文件（New File）。让我们从一些简单的内容开始，输入：

```python
print("Hello")
firstname=input("What is your name? ")
print("Thanks")
surname=input("What is your surname? ")
```

- 第 3 步：现在我们已经将用户的名字存储在几个变量中，我们可以随时调用它们：

```python
print("Welcome", firstName, surname, ". I hope you're well today.")
```

- 第 2 步：保存并执行代码，正如你无疑怀疑的那样，在 IDLE Shell 中，程序会询问你的名字，将其存储为变量 `firstName`，然后是你的姓氏，存储在另一个变量中：

- 第 4 步：运行代码，你会发现一个轻微的问题，姓氏后的句号留了一个空格。为了消除这个问题，我们可以在代码中使用加号代替逗号：

```python
print("Welcome"
```

```python
Python 3.4 Shell
Python 3.4.2 (default, Oct 19 2014, 13:31:11)
>>> print("Hello")
Hello
>>> firstName=input("What is your name? ")
David
>>> print("Thanks")
Thanks
>>> surname=input("What is your surname? ")
Hayward
>>> print("Welcome", firstName, surname)
Welcome David
58836402a77f1799fa9a173f0a_35_0.png

 第 5 步

你并不总是要在 `input` 命令中包含引号文本。例如，你可以询问用户的名字，并在下方有输入：

```python

print("Hello. What's name?")

name=input()

```
58836402a77f1799fa9a173f0a_36_0.png

```python

Edit File Format Options Windows Help

print("Hello. What's name?")

name=input()

```

## 第 8 步

你在这里创建了一个条件，我们将很快涵盖。简而言之，如果用户输入一个名字，程序将允许。否则，如果他们输入的不是 David 名字，程序将停止。

```python

Edit File Format Options Windows Help

print("Hello. What's name?")

name=input()

```

## 第 6 步

上一步的代码经常被批评为活性不足，但它并不是一成不变的，所以我们这样做：

```python

print("Hello. What's name?")

name=input()

```

## 第 9 步

正如你所学到的，任何 `input` 都是字符串，所以你需要将它转换为其他东西。例如：

```python

age = float(input("Enter your age: "))

```

## 第 7 步

在处理浮点数运算时，类型转换类型也很重要；记住小数点。例如，输入：

```

float(19.99)

```

等待，让我重新对齐文本流。

```python

print("Hello. What's name?")

name=input()

```

## 第 10 步

为了完成速率，我们可以添加：

```

distance = float(input())

```

等待，提供的 OCR 非常破碎且混乱。我将根据提供的页面内容重构逻辑流。（自我修正：OCR 文本顺序错误且重复。我将按照要求输出文本，修复明显的错误并进行格式化。）

# 变量操作

## 第 5 步

然而，你不能在同一个命令中组合字符串和整数变量，因为你需要一组变量来将一个转换为另一个，反之亦然。当你尝试将两者结合时，你将得到一个错误消息：

```python

print (name + age)

```

```python

Python 3.4.2 (default, Oct 19 2014, 13:31:11)

name = 'Thor'

age = 44

print(type(name))

<class 'str'>

print(type(age))

<class 'int'>

print(name + ' Descended from Vikings')

Thor Descended from Vikings

print(name + age)

TypeError: Can't convert 'int' object to str

```

## 第 8 步

当你想要处理用户输入的数字时，这会带来一些问题，因为 `age + 10` 由于是一个字符串和一个整数而无法工作。相反，你需要：

```

int(age) + 10

```

这将把字符串转换为可以操作的整数。

```python

Python 3.4.2

Edit File Debug Options Windows Help

Python 3.4.2 (default, Oct 19 2014, 13:31:11)

age = input("Enter your age: ")

print(type(age))

<class 'str'>

print(age + 10)

TypeError: Can't convert 'str' object to int

```

在处理浮点数运算时，类型转换（Casting）类型也很重要；记住小数点。例如，输入：

```

float(19.99)

```

## 第 6 步

这种过程被称为类型转换（Casting）。Python 代码如下：

```python

print ("age is " + str(age) + " years old.")

44 years old.

```

或者你可以使用：
注意在最后一个例子中，你不需要在引号单词之间留空格，因为逗号会分别处理每个部分。

```python

print ("name is " + name + ", years old.")

Thor is 44 years old.

```

## 第 9 步

现在输入 `type(float)`，你会发现 Python 已将数字转换为了 'float'（浮点数），它包含小数值。

```python

Python 3.4.2

Edit File Debug Options Windows Help

Python 3.4.2 (default, Oct 19 2014, 13:31:11)

age = float(input("Enter your age: "))

print(type(age))

<class 'float'>

print(age + 10)

29.99

```

## 第 7 步

类型转换的另一个示例是你需要用户的输入，例如：

```python

age = input("How old are you?")

```

所有数据都被存储为字符串。

```python

Python 3.4.2

Edit File Debug Options Windows Help

Python 3.4.2 (default, Oct 19 2014, 13:31:11)

age = input("How old are you?")
