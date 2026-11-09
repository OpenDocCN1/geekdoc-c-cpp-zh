
### 8. 选择一个数字

现在使用 random 模块中的 randrange() 函数，从 0 到 100 中选择一个随机数。将这一行放到代码底部。

```python
noun = random.choice(nouns)
number = random.randrange(0, 100)
```

### 专家提示

### 常量

常量是一种特殊类型的变量，其内容不能更改。常量 string.punctuation 保存着用于标点符号的一串字符。要查看它包含什么，请在 shell 中输入 import string，然后输入 print(string.punctuation)。

```python
>>> import string
>>> print(string.punctuation)
!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
```

此常量中的字符

### 9. 选择一个特殊字符

再次使用 random.choice() 函数，添加这一行来随机选取一个标点字符。这会让你的密码更难被破解！

```python
number = random.randrange(0, 100)
special_char = random.choice(string.punctuation)
```

这是一个常量。

### 10. 创建新的安全密码

现在是时候将所有不同部分组合起来，创建新的安全密码了。在你的程序末尾输入这两行代码。

你的安全密码将存储在此变量中。

这会把随机数转换为字符串。

```python
password = adjective + noun + str(number) + special_char
print('Your new password is: %s' % password)
```

这会在 shell 中显示新密码。

### 专家提示

### 字符串和整数

str() 函数会将整数（integer）转换为字符串。如果不使用此函数，当你尝试将整数与字符串相加时，Python 会显示错误。测试一下：在 shell 窗口中输入 print('route ' +66)。

```python
>>> print('route ' +66)
Traceback (most recent call last):
  File "<pyshell#0>", line 1, in <module>
    print('route ' +66)
TypeError: Can't convert 'int' object to str implicitly
```

错误消息

为避免此错误，请先使用 str() 函数将数字转换为字符串。

```python
>>> print('route ' +str(66))
route 66
```

数字放在 str() 函数的括号内。

### 11. 测试程序

现在是测试代码的好时机。运行它，并在 shell 中查看结果。如果出现错误，别担心。仔细回看你的代码，找出任何错误。

```text
Welcome to Password Picker!
Your new password is: bluegoat92=
```

你的随机密码可能会有所不同。

![](img/6b18a113f7aa9338e32f3ac1fa217987_57_0.png)

### 12. 再来一个？

你可以使用 while 循环，在用户表示想要一个不同的密码时生成另一个密码。将这段代码添加到你的程序中。它会询问用户是否需要新密码，然后将回复存储在名为 response 的变量中。

```python
print('Welcome to Password Picker!')

while True:
    adjective = random.choice(adjectives)
    noun = random.choice(nouns)
    number = random.randrange(0, 100)
    special_char = random.choice(string.punctuation)

    password = adjective + noun + str(number) + special_char
    print('Your new password is: %s' % password)

    response = input('Would you like another password? Type y or n: ')
    if response == 'n':
        break
```

**while** 循环从这里开始。

你需要缩进这些已有代码行，确保它们位于 **while** 循环中。

**while** 循环在这里结束。

input() 函数要求用户在 shell 中输入回复。

如果回答是“yes”（y），循环会返回开头。如果回答是“no”（n），程序会退出循环。

### 13. 挑选一个完美的密码

就是这样——你完成了。现在你可以创建难以破解且便于记忆的密码了！

```text
Welcome to Password Picker!
Your new password is: yellowapple42?
Would you like another password? Type y or n: y
Your new password is: greenpanda13*
Would you like another password? Type y or n: n
```

在此提示符处输入“y”以获取新密码。

在此提示符处输入“n”以退出程序。

## 技巧与调整

试着改造你的程序以添加这些额外功能。你能想到其他让它更难被破解的方法吗？

![](img/6b18a113f7aa9338e32f3ac1fa217987_58_0.png)

### 添加更多单词

要增加可能密码的数量，请向名词和形容词列表中添加更多单词。想一些不寻常或滑稽的单词，如果它们出现在密码中，会让你印象深刻。

```python
nouns = ['apple', 'dinosaur', 'ball',
         'toaster', 'goat', 'dragon',
         'hammer', 'duck', 'panda',
         'telephone', 'banana', 'teacher']
```

### 获取多个密码

修改代码，使程序一次创建并显示三个密码。你需要使用 for 循环。把它放在 while 循环内。

```python
while True:
    for num in range(3):
        adjective = random.choice(adjectives)
        noun = random.choice(nouns)
        number = random.randrange(0, 100)
        special_char = random.choice(string.punctuation)

        password = adjective + noun + str(number) + special_char
        print('Your new password is: %s' % password)

    response = input('Would you like more passwords? Type y or n: ')
```

for 循环运行 3 次，并选择 3 个不同的密码。

保持这些行缩进。

![](img/6b18a113f7aa9338e32f3ac1fa217987_58_1.png)

### 让它更长

通过向每个密码中添加另一个单词，使密码更长、更安全。你可以创建一个颜色列表，然后随机选择一种颜色添加到每个密码中。

```text
Add a random colour ...

Your new password is: hairybluepotato33%
```

## 模块

模块是代码包，帮助你处理常见的编程挑战。模块提供不太有趣的代码部分，让你专注于有趣的内容。此外，由于模块被很多人使用，它们往往运行良好且没有错误。

### 内置模块

Python 包含许多有用的模块。这些模块的集合称为标准库。以下是库中一些你可能想尝试的有趣模块。

![](img/6b18a113f7aa9338e32f3ac1fa217987_59_0.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_59_1.png)

- **statistics**：使用 `statistics` 计算平均值，或在数字列表中查找最常见的值。如果你需要计算游戏中的平均分，它会很方便。
- **datetime**：此模块让你处理日期。你可以获取今天的日期，或计算距离某个特殊日子还有多长时间。

![](img/6b18a113f7aa9338e32f3ac1fa217987_59_2.png)

- **random**：你在密码选择器中使用了此模块进行随机选择。它非常适合为游戏或程序添加随机因素。

![](img/6b18a113f7aa9338e32f3ac1fa217987_59_3.png)

- **webbrowser**：你可以使用此模块控制计算机的 Web 浏览器，从而直接从代码中打开网页。

![](img/6b18a113f7aa9338e32f3ac1fa217987_59_4.png)

- **socket**：socket 模块允许程序跨网络和互联网通信。它可用于创建在线游戏。

![](img/6b18a113f7aa9338e32f3ac1fa217987_59_5.png)

### 使用模块

要在代码中使用模块，你必须告诉 Python 你想包含它。你使用 import 语句指示 Python 要包含哪些模块。根据你从模块中需要什么，有几种不同的方法可以做到这一点。

![](img/6b18a113f7aa9338e32f3ac1fa217987_60_0.png)

### import...

输入关键字 import 可以让你使用模块的所有内容。但是，你需要在使用的任何函数前加上模块名。这段代码导入整个 webbrowser 模块，并使用其 open() 函数在计算机的浏览器中打开 Python 网站。

```python
>>> import webbrowser
>>> webbrowser.open('https://docs.python.org/3/library/')
```

这一行导入整个 webbrowser 模块。

模块名位于函数之前。

### from... import...

如果你只想使用模块的特定部分，可以通过添加 from 关键字只导入该部分。现在你可以单独使用该函数。这段代码导入 random 模块的 choice() 函数。该函数会从你提供的任何列表中随机挑选一项。

```python
>>> from random import choice
>>> direction = choice(['N', 'S', 'E', 'W'])
>>> print(direction)
W
```

只从 random 模块导入 choice 函数。

不需要模块名。

代码会打印一个随机方向。

### from... import... as...

有时你可能想更改导入模块或函数的名称，也许是因为你已经使用过该名称，或者它不够清晰。要做到这一点，请使用关键字 as，后面跟新名称。在此处显示的示例中，time() 函数（我们已将其重命名为 time_now()）给出当前时间。所给时间是自 1970 年 1 月 1 日 00:00 起的精确秒数——大多数计算机将此日期用作时钟的起点。

```python
>>> from time import time as time_now
>>> now = time_now()
>>> print(now)
1478092571.003539
```

这一行导入并重命名 time() 函数。

此变量使用该函数的新名称。

自 1970 年 1 月 1 日 00:00 起的秒数

![](img/6b18a113f7aa9338e32f3ac1fa217987_60_1.png)

