

## 分支

布尔表达式可以用于确定程序应该遵循哪条路径，取决于表达式的答案是“真”（True）还是“假”（False）。这被称为“分支”。

另另
| 64–65 | 决策与分支 |
| 118–119 | 决策 |

## 执行或不执行

“if”命令意味着如果条件为“真”，则程序将运行一段命令。如果条件不为“真”，则跳过该代码块。“if”命令后的代码块始终缩进四个空格。

- * if condition*（如果条件）
这段代码询问用户是否是生日。它检查答案是否为“y”。如果是，则会打印一条生日消息。

```python
ans = input('Is it your birthday?')
if ans == 'y':
    print('Happy Birthday!')
```

- * 当条件为“真”时输出
运行程序并输入“y”。会打印消息。如果输入其他内容，则不会显示。

Is it your birthday? (y/n)y
Happy Birthday!

“if”命令可以与“else”命令结合使用。这种组合意味着如果某事为“真”，就会发生一件事；如果不是，则什么都不会发生。

- * if-else condition（if-else 条件）
如果输入“y”，程序会打印一条特殊的新年消息。如果输入其他内容，则会显示一条不同的消息。

```python
ans = input('Is it New Year? (y/n) ')
if ans == 'y':
    print('Happy New Year!')
    print('Time for Fireworks.')
else:
    print('Not yet!')
```

![](img/72d218a7a73c4d4abc7be582ebd85385_121_0.png)

## 分支
## 121

## 当条件为“真”时输出

## “else”条件输出

运行程序并输入“y”。程序显示你的新年消息。它不会显示另一条消息。

输入“n”或任何其他字符，就不会显示新年消息。相反，会出现“Not yet!”。

输入“n”
Is it New Year? (y/n)
Happy New Year!
Time for Fireworks.

Is it New Year? (y/n)
Not yet!

出现了一条不同的消息

## 执行这些操作之一

“elif”命令是“else-if”的缩写。它的意思是如果某事为“真”，则执行一件事；否则，检查另一件事是否为“真”，如果是，则执行另一件事。下面的计算器程序使用了“elif”命令。

![](img/72d218a7a73c4d4abc7be582ebd85385_122_0.png)

## if-elif-if 条件

## 当条件为“真”时的输出

此程序检查输入的内容。如果是“add”、“sub”、“mul”或“div”，则会显示求和的结果。

测试程序。输入两个数字并输入“sub”。答案将是第一个数字减去第二个数字。

要求用户输入数字
记得加上引号和括号

| a = int(input('a = ')) |
| b = int(input('b = ')) |
| op = input('add/mul/div: ') |
| if op == 'add': |
| c = a + b |
| elif op == 'sub': |
| c = a - b |
| elif op == 'mul': |
| c = a * b |
| elif op == 'div': |
| c = a / b |

| a = 7 | 输入两个数字 | 输入“sub” |
| b = 5 | 进行减法 |
| add/mul/div:sub | 从 7 中减去 5 |
| Answer = 2 | |

输入“add”相加变量
Answer 是通过从 b 中减去 a 计算出的
输入“div”除以变量

## “else”条件输出

如果输入的不是“add”、“sub”、“mul”或“div”，则运行“else”条件，并显示错误消息。

当输入其他内容时，会在“c”中显示错误消息。

| a = 7 | 输入其他内容 |
| b = 5 | |
| add/mul/div:try | 错误消息显示 |
| Answer = Error | |

```python
else:
  c = 'Error'
print('Answer = ',c)
```

## Python 中的循环

包含重复代码的程序编写起来很耗时且难以理解。更清晰的写法是使用循环。最简单的循环是重复特定次数的循环，例如“for”循环。

另另
| 48–49 | 画笔与乌龟 |
| 124–125 | While 循环 |
| 126–127 |

## 重复内容

“for”循环不需要重复输入代码。它可以用于重复某些次数，例如，如果你想打印 30 个学生的名字。

![](img/72d218a7a73c4d4abc7be582ebd85385_123_0.png)

- “for”循环也可以用于缩短代码。此程序允许用户通过控制乌龟的移动在屏幕上绘制形状。

```python
from turtle import *
forward(100)
right(120)
forward(100)
right(120)
forward(100)
right(120)
```

“for”循环告诉程序重复三次指令——三角形的每边一次。另一种方法是在“for”循环内部使用这两个命令。尝试使用下面的代码画一个三角形。

```python
for i in range(3):
    forward(100)
    right(120)
```

![](img/72d218a7a73c4d4abc7be582ebd85385_123_1.png)

Python 中的乌龟。循环中的指令块缩进四个空格。程序画了一个三角形。

## 循环变量
## PYTHON 中的循环
## 123

循环变量计算循环重复的次数。它从范围中的第一个值（0）开始，在最后一个值之前停止。

```python
for i in range(10):
    print(i, end=' ')
```
>>> 0 1 2 3 4 5 6 7 8

## 简单循环变量

在这里，循环的范围没有指定起始值。因此 Python 从 0 开始计数，就像它处理字符串一样。![](img/72d218a7a73c4d4abc7be582ebd85385_124_0.png)

```python
for i in range(2, 11, 2):
    print(i, end=' ')
```

```python
for i in range(10, 0, -1):
    print(i, end=' ')
```

输出是两次一次的。
>>> 2 4 6 8 10
>>> 10 9 8 7 6 5 4 3 2 1

## 两次计数

这个循环的范围有一个第三个值，告诉循环两次计数。它停止在 10，一个循环变量到了 11。

## 倒数

这次程序从 10 开始倒数，就像火箭发射一样。循环变量从 10 开始，以 -1 为步长计数直到到达 1。

## 嵌套循环

循环内部循环被称为被称为嵌套循环”。在嵌套循环中，只有在内部循环运行完所需的次数后，外层循环才会重复。

要让循环重复“n” 次，范围中的最后一个数字必须是“n + 1”。

| "b" 的值 | |
|---|---|
| 1 * x = 1 | 外层循环第一次（内部循环重复三次） |
| 2 * x = 2 | |
| 3 * x = 3 | |
| 2 * x = 4 | 外层循环第二次 |
| 3 * x = 6 | |
| 1 * x = 3 | 外层循环第三次 |
| 2 * x = 6 | |
| 3 * x = 9 | |

```python
n = 3
for a in range(1, n + 1):
    for b in range(1, n + 1):
        print(b, 'x', a)
```

外层循环

 循环内部的循环

在这个例中，每当外层循环运行一次，内部循环就会运行三次。所以总共外层循环执行了三次，内部循环执行了九次。

## 125

## While 循环

当你知道任务需要重复多少次时，“for”循环非常有用。但有时你需要一个循环来持续重复直到某些发生变化。“while”循环只要特定条件为真就会一直运行。这个条件被称为“循环条件”，它的值是真或假。

- * 工作原理
循环检查条件是否为真。如果是，它再次运行循环。如果不是，它跳过循环。

- * 创建循环
在循环条件中设置变量“answer”的初始值。循环条件必须初始为真，否则循环将不会运行。

```python
answer = 'y'
while answer == 'y':
    print('Stay very still')
    answer = input('Is the monster friendly?')
    print('Run away!')
```

![](img/72d218a7a73c4d4abc7be582ebd85385_125_0.png)

- * 程序的样子
输入的值存储在变量“answer”中。循环条件是“answer=='y{}'.如果你输入“y”，循环继续。如果你输入“n”，循环停止。

> 记得
repeat直到"块

```
>>>
Stay very still
Is the monster friendly? (y/n)
Stay very still
Is the monster friendly? (y/n)
Stay very still
Is the monster friendly? (y/n) n
Run away!
```

Python 的“while”类似于 Scratch 中的“repeat直到”块。两者都会持续让程序中发生不同的事情。

![](img/72d218a7a73c4d4abc7be582ebd85385_125_1.png)

