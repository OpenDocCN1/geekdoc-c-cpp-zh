

# 无限循环

有些循环会永远运行。如果你将 "while" 循环中的条件设置为 "True"真），它就永远不会变成假，循环也永远不会结束。这可能非常有用，也可能非常烦人。

![](img/72d218a7a73c4d4abc7be582ebd85385_126_0.png)

-   创建一个无限循环
循环条件被设置为 "True"。在循环内部发生的任何事情都不会让 "True" 变成其他值，因此循环会永远运行。

输入的单词存储在变量 "answer" 中

```python
while True:
    # 循环始终为 'True'，永远不会结束
    answer = input('Type a word and press enter: ')
    print('Please do not type ' + answer + ' again.')
```

-   程序运行的样子
在相反的怪物示例中，程序的循环条件会检查用户的答案是什么。如果答案不是 "y"，循环就会停止。上面显示的循环没有检查答案，因此用户无法让它停止。

无论输入什么，这个循环都会持续进行

```python
>>>
Type a word and press enter: tree
Please do not type 'tree' again
Type a word and press enter: hippo
Please do not type 'hippo' again
Type a word and press enter: water
Please do not type 'water' again
Type a word and press enter
```

> 记住
"forever" 模块

Scratch 中的 "forever" 模块？它会重复内部的代码，直到点击红色停止按钮。"True" 循环的作用完全相同。只要程序在运行，它就可以让程序执行某些操作，例如提问或打印数字。

-   专家提示
停止循环
如果你被卡在无限循环中，可以从 IDLE 停止它。点击 Python 壳 窗口，然后按住 "CTRL-C" 键并按下 "CTRL-C"。这会要求 IDLE 停止程序。你可能需要按几次。这类似于点击 Scratch 中的红色按钮。

![](img/72d218a7a73c4d4abc7be582ebd85385_126_1.png)

# 跳出循环

程序可能会卡在循环中，但有方法可以跳出来。单词 "break" 会离开循环（即使是 "forever" 循环），而单词 "continue" 会跳到下一次循环的开头。

# 另请

-   122-123 Python 中的循环
-   124-125 While 循环

## 插入 break

在循环中放入 break 会程序立即跳出循环——即使循环条件为真。循环中 break 之后的任何命令都会被忽略。

```python
table = 7
for i in range(1, 13):
    print('What\'s', i, 'x', table, '?')
    guess = input()
    if guess == ans:
        print('Correct!')
    else:
        print('No, it\'s', ans)
    print('Finished')
```

-   **编写一个简单的程序**
这个程序将测试用户对七九乘法的记忆。程序将持续循环，直到所有 12 个问题都得到回答。在代码窗口中编写此程序，因为它会被编辑。

-   **插入一个 "break"**
可以添加一个 "break" 让用户跳出循环。如果用户输入 "stop"，程序将执行 break。

```python
table = 7
for i in range(1,13):
    print('What\'s', i, 'x', table, '?')
    guess = input()
    if guess == 'stop':
        break
    ans = i * table
    if int(guess):
        print('Correct!')
    else:
        print('No, it\'s', ans)
    print('Finished')
```

> "guess" 等于 "stop"，程序跳过循环的剩余部分并打印 "Finished"
> "ans" 变量持有正确的答案
![](img/72d218a7a73c4d4abc7be582ebd85385_127_0.png)

# 跳出循环

127

>>>

# What’s 1 x 7 ?

1

第一次循环 "i" 等于 1

# No, it’s 7

# What’s 2 x 7 ?

14

下一次循环 "i" 变为 2

# Correct!

# What’s 3 x 7 ?

stop

执行 break 命令，程序退出循环

Finished
![](img/72d218a7a73c4d4abc7be582ebd85385_128_0.png)

# 工作原理

如果用户决定在第三个问题后继续并输入 "stop"，就会执行 break 命令，程序离开循环。

# 跳过

"continue" 关键字可以跳过问题而不离开循环。它告诉程序跳到下一次循环。

# 插入 continue

在循环内部添加一个 "if" 语句查看用户是否回答了 "skip"。如果是，程序将打印 "Skipping" 并执行 "continue" 跳到下一次循环。

```python
table = 7
for i in range(1,13):
    print('What\'s', i, 'x', table, '?')
    guess = input()
    if guess == 'stop':
        break
    ans = i * table
    if guess == 'skip':
        print('Skipping')
        continue
    if int(guess) == ans:
        print('Correct!')
    else:
        print('No, it\'s', ans)
    print('Finished')
```

# 发生了什么

如果用户不想回答问题，他们可以输入 "skip" 并继续到下一个问题。

```python
>>>
What’s 1 x 7 ?
Type "skip"
Skipping
What’s 2 x 7 ?
14
Correct!
What’s 3 x 7 ?
```

当答案正确时，循环会再次进行。

# 列表

如果你需要将一组数据放在一起，可以将它们放在列表中。列表可以包含数字、字符串、其他列表或组合。

# 什么是列表？

列表是 Python 中按顺序存储项的结构。每个条目都有一个数字供你回引。你可以在任何时候更改、删除或添加列表中的项。

# 查看列表

列表中的每个项都位于引号内，并用逗号与下一个项分隔。整个列表位于方括号内。列表存储在变量 `mylist` 中

```python
>>>list = ['apple', 'milk', 'cheese', 'lemonade', 'tea']
```

这个字符用于跨行编写代码。列表中的项位于方括号内。和字符串一样，Python 从零开始计算列表中的项。因此，这里 "apple" 的位置（索引）是 "0"。

# 工作原理

你可以将列表想象成厨房的一排架子。每个架子持有列表中的一项。要对项进行更改，必须引用它所在的架子。输入 `mylist[1] = 'cake'` 将用 "cake" 替换架子 1 上的 "milk"。

```python
[0]
```

`mylist[2]` 的值为 "cheese"

[1]

你可以通过输入 `mylist.insert(3, 'orange')` 在蛋糕前面添加一个橙子。冰淇淋就会移动到位置 4，依此类推

```python
[2]
```

要访问列表上的项，必须去正确的架子。编写 `del mylist[4]` 会从列表中删除 "lemonade"，并将 "tea" 移动到位置 4。

```python
[3]
```

你可以通过编写 `mylist.append('pie')` 在列表末尾添加新项 "pie"。这将添加到 "tea" 之后，位于位置 6

```python
[4]
```

项在列表的位置被称为它的“索引”

```python
[5]
```

![](img/72d218a7a73c4d4abc7be582ebd85385_129_0.png)

# 使用列表

一旦创建了列表，你就可以编写程序来操作其内部的数据——例如在循环中。你还可以组合列表来创建新列表。

![](img/72d218a7a73c4d4abc7be582ebd85385_130_0.png)

# 可变对象

Python 中的列表是可变的。这意味着它们可以改变。你可以添加或删除项，或者交换它们的顺序。Python 中的其他函数，例如元组（第 134-135 页），一旦创建就无法更改。它们被称为“不可变”。

-   列表存储在变量 "names" 中

```python
>>> names = ['Simon', 'Kate', 'Vanya']
>>> for item in names:
    print('Hello', item)
```

-   循环体必须缩进四个空格

Hello Simon
Hello Kate
Hello Vanya

-   运行时，此程序显示 "Hello"，然后是列表上的每个名字。

# 循环中的列表

你可以使用循环处理列表中的每一个项。程序会对一系列名字显示 "Hello"，一个接一个。

```python
x = [1, 2, 3, 4]
y = [5, 6, 7, 8]
z = x + y
print(z)
[1, 2, 3, 4, 5, 6, 7, 8]
```

-   记住，列表包含在方括号内

-   新列表包含 "x" 的所有内容，随后是 "y" 的所有内容

# 添加列表

两个列表可以相加。新列表将包含两个旧列表的所有项。

![](img/72d218a7a73c4d4abc7be582ebd85385_130_1.png)

