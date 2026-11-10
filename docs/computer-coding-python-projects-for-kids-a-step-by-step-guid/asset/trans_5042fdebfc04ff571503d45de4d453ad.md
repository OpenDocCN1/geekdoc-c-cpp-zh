
## 密码生成器流程图

程序会随机选择密码的四个部分，将它们组合在一起，并在 shell 窗口中显示密码。如果你想要另一个密码，它会再次重复这些步骤。如果你不想，程序就会结束。

- 开始
- 随机选择一个形容词
- 随机选择一个名词
- 随机选择 0 到 100 之间的一个数字
- 随机选择一个标点符号
- 创建安全密码
- 显示安全密码
- 想要另一个密码吗？
  - Y：重复密码生成步骤
  - N：结束

## 工作原理

本项目将向你展示如何使用 Python 的 random 模块。程序从形容词、名词、数字和标点符号组中随机选择，来组合每个密码。你很快就能生成疯狂又难忘的密码，例如 "fluffyapple14(" 或 "smellygoat&"！

![](img/1bd24ab186f69fb18194b4174ca15178_52_0.png)

## 巧妙却简单！

这个程序在密码方面做了些巧妙的事，但代码量不大，所以很快就能完成。

![](img/1bd24ab186f69fb18194b4174ca15178_52_1.png)

- **1. 创建新文件**
  打开 IDLE。在“文件”菜单下，选择“新建文件”。将文件保存为“password_picker.py”。

- **2. 添加模块**
  从 Python 库中导入 string 和 random 模块。在文件顶部输入这两行，以便稍后使用这些模块。

  ```python
  import random
  import string
  ```

  string 模块让你能对字符串做一些有用的事，比如拆分字符串或改变它们的显示方式。

- **3. 欢迎用户**
  首先创建一条消息，欢迎用户使用该程序。

  这一行显示一条欢迎用户的消息。

  ```python
  import random
  import string

  print('Welcome to Password Picker!')
  ```

- **4. 试运行代码**
  运行代码。欢迎消息应出现在 shell 窗口中。

  ```
  Welcome to Password Picker!
  ```

- **5. 创建形容词列表**
  你需要形容词和名词来生成新密码。在 Python 中，你可以将一组相关的内容保存为列表。首先创建变量 `adjectives` 来存储列表，方法是在 `print()` 命令和 `import` 语句之间输入这段新代码。将整个列表放在方括号中，并用逗号分隔每一项。

  ```python
  import string

  adjectives = ['sleepy', 'slow', 'smelly',
                'wet', 'fat', 'red',
                'orange', 'yellow', 'green',
                'blue', 'purple', 'fluffy',
                'white', 'proud', 'brave']

  print('Welcome to Password Picker!')
  ```

  - 列表存储在变量 `adjectives` 中。
  - 每一项都是字符串。
  - 在每一项后加逗号。
  - 列表放在方括号中。

- **6. 创建名词列表**
  接下来创建一个保存名词列表的变量。把它放在形容词列表下方、`print()` 命令上方。记得像第 5 步那样使用逗号和方括号。

  ```python
  'white', 'proud', 'brave']

  nouns = ['apple', 'dinosaur', 'ball',
           'toaster', 'goat', 'dragon',
           'hammer', 'duck', 'panda']

  print('Welcome to Password Picker!')
  ```

  将每一项放在引号内。

## 专家提示

### 随机数

掷骰子、从一副牌中抽一张牌或抛硬币，都可以通过生成随机数来模拟。你可以在“帮助”菜单的“文档”部分阅读更多关于如何使用 Python 的 random 模块的内容。

![](img/1bd24ab186f69fb18194b4174ca15178_53_0.png)

- **7. 挑选单词**
  要创建密码，你需要随机挑选一个形容词和一个名词。你可以使用 random 模块中的 `choice()` 函数来完成。在 `print()` 命令下方输入这段代码。（每当你想从列表中随机选择一项时，都可以使用这个函数。只需把包含各项的变量传给它。）

  ```python
  print('Welcome to Password Picker!')

  adjective = random.choice(adjectives)
  noun = random.choice(nouns)
  ```

  - 这个变量保存从形容词列表中随机选择的一个单词。
  - 从列表中选择一个名词并存入这个变量。

## 模块

模块是现成代码的集合，可帮助你应对常见的编程挑战。模块提供了那些不那么有趣的代码部分，让你能专注于有趣的内容。此外，由于模块被很多人使用，它们往往运行良好且没有错误。

### 内置模块

Python 自带许多有用的模块。这些模块的集合称为标准库。以下是标准库中一些你可能会想尝试的有趣模块。

![](img/1bd24ab186f69fb18194b4174ca15178_57_0.png)

### datetime

这个模块让你可以处理日期。你可以获取今天的日期，或计算距离某个特殊日子还有多久。

![](img/1bd24ab186f69fb18194b4174ca15178_57_1.png)

### statistics

使用 statistics 计算平均值，或找出数字列表中最常见的值。如果你需要计算游戏中的平均分，它会很方便。

![](img/1bd24ab186f69fb18194b4174ca15178_57_2.png)

### random

你在“密码生成器”中使用这个模块进行随机选择。它非常适合为游戏或程序加入随机性。

![](img/1bd24ab186f69fb18194b4174ca15178_57_3.png)

### webbrowser

你可以用这个模块控制计算机的网页浏览器，从而直接从代码中打开网页。

![](img/1bd24ab186f69fb18194b4174ca15178_57_4.png)

### socket

socket 模块允许程序跨网络和互联网通信。它可以用来创建在线游戏。

![](img/1bd24ab186f69fb18194b4174ca15178_57_5.png)

## 使用模块

要在代码中使用模块，必须告诉 Python 你想包含它。你可以使用 import 语句指示 Python 包含哪些模块。根据你从模块中需要什么，有几种不同的做法。

![](img/1bd24ab186f69fb18194b4174ca15178_58_0.png)

### ▷ import ...

输入关键字 import 可以使用模块的全部内容。但是，你需要在使用的任何函数前加上模块名。这段代码导入整个 webbrowser 模块，并使用其 open() 函数在计算机浏览器中打开 Python 网站。

```python
>>> import webbrowser
>>> webbrowser.open('https://docs.python.org/3/library/')
```

- 这一行导入整个 webbrowser 模块。
- 模块名位于函数之前。

### ▷ from ... import ...

如果你只想使用模块的特定部分，可以通过添加 from 关键字只导入该部分。现在你可以单独使用函数名。这段代码导入 random 模块的 choice() 函数。该函数会从你提供的任何列表中随机挑选一项。

这里只从 random 模块导入了 choice 函数。

```python
>>> from random import choice
>>> direction = choice(['N', 'S', 'E', 'W'])
>>> print(direction)
W
```

- 不需要模块名。
- 代码会打印一个随机方向。

### ▷ from ... import ... as ...

有时你可能想更改导入的模块或函数的名称，也许是因为你已经使用了那个名称，或者它不够清晰。要做到这一点，请使用 as 关键字，后跟新名称。在下面展示的示例中，time() 函数被重命名为 time_now()，它为我们提供当前时间。给出的时间是从 1970 年 1 月 1 日 00:00 起经过的精确秒数——大多数计算机把这个日期作为其时钟的起点。

这一行导入并重命名了 time() 函数。

```python
>>> from time import time as time_now
>>> now = time_now()
>>> print(now)
1478092571.003539
```

- 这个变量使用了函数的新名称。
- 自 1970 年 1 月 1 日 00:00 起经过的秒数

> 你正好迟到了
> 1478092571.003539
> 秒！

![](img/1bd24ab186f69fb18194b4174ca15178_58_1.png)

## 九条命

在这个令人神经紧绷的游戏中，你必须一次猜一个字母来猜出秘密单词。如果猜错，你就会失去一条命。请谨慎选择字母，因为你只有九条命。失去所有命，游戏就结束了！

### 游戏流程

程序会显示一个神秘单词，其中的字母被问号代替。如果你猜对一个字母，程序会用正确字母替换问号。当你认为知道这个单词时，就完整地输入它。一旦你输入正确单词或没有剩余生命，游戏就会结束。

提示会用问号显示神秘单词。

剩余生命数用爱心表示。

```
['?', '?', '?', '?', '?', '?']
Lives left: ♥♥♥♥♥♥♥♥♥
Guess a letter or the whole word: a
['?', '?', '?', '?', '?', 'a']
Lives left: ♥♥♥♥♥♥♥♥♥
Guess a letter or the whole word: i
['?', 'i', '?', '?', '?', 'a']
Lives left: ♥♥♥♥♥♥♥♥♥
Guess a letter or the whole word: y
Incorrect. You lose a life
['?', 'i', '?', '?', '?', 'a']
Lives left: ♥♥♥♥♥♥♥♥
Guess a letter or the whole word: p
['p', 'i', '?', '?', '?', 'a']
Lives left: ♥♥♥♥♥♥♥♥
Guess a letter or the whole word: t
Incorrect. You lose a life
['p', 'i', '?', '?', '?', 'a']
Lives left: ♥♥♥♥♥♥♥
Guess a letter or the whole word: pizza
You won! The secret word was pizza
```

每猜对一个字母，就会揭示秘密单词中的一个或多个字母。

每次猜错都会使一颗爱心消失。

如果你知道这个单词，就输入它来赢得游戏。

> 你还剩七条命。你下一次猜什么？
> 我猜“P”！

![](img/1bd24ab186f69fb18194b4174ca15178_59_0.png)

