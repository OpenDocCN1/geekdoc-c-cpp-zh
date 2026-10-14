

使用 *if/elif* 条件。同样，你可以先使用 *if/elif* 语句创建程序，然后在修改时将其更改为字典或列表。这可以作为常规重构（重写代码以使其更易于管理或阅读）的一部分、查错的一部分，或者用于加速程序。

### 11.5 while 循环

*while* 循环是许多语言中的标准主力。本质上，程序会在某个条件存在时继续执行某事。一旦该条件不再为真，循环就会停止。

Python 的 *while* 语句与其他语言类似。以下是主要格式：

示例 11.7：*while 循环，第一部分*

```python
while <test>:
    #loop test
    <code block>
    #loop body
else:
    #optional else statement
    <code block>
    #run if didn't exit loop with
    #break
```

*break* 和 *continue* 在 C 语言中工作方式完全相同。C 语言中的空语句（一个分号）的等价物是 *pass* 语句，并且 Python 为配合 break 使用而包含了一个 *else* 语句。以下是一个完整的 *while* 循环示例：

示例 11.8：*while 循环，第二部分*

```python
while <test>:
    <statements>
    if <test>: break #exit loop now if true
    if <test>: continue #return to top of loop now if true
else:
    <statements>
    #if we didn't hit a 'break'
```

*break* 语句仅仅强制循环提前退出；当与嵌套循环一起使用时，它只退出最内层（最小的包含）循环。*continue* 语句使循环重新开始，无论循环后面还有什么其他语句。除非 *break* 语句导致循环提前退出，否则 *else* 代码块会在循环的“出口处”运行。

对于仍然感到困惑的人，下一节将展示这些语句在涉及质数的实际程序中是如何使用的。

### 11.6 for 循环

for 循环是 Python 中的序列迭代器。它几乎适用于任何对象：字符串、列表、元组等。我之前讨论过 for 循环，并且在未来的章节中我们会看到很多，所以我不再过多详细阐述。主要格式如下，见示例 11.9。请注意，它本质上与 while 循环相同。

示例 11.9：for 循环

```python
for <target> in <object>:     #assign object items
    #to target
    <statements>
    if <test>: break    #exit loop now, skip else
    if <test>: continue #go to top of loop now
else:
    <statements>        #if we didn’t hit a ‘break’
```

摘自 O'Reilly 出版的《学习 Python》：

> “当 Python 运行 for 循环时，它将序列对象中的项逐一分配给目标，并对每一项执行循环主体。循环主体通常使用赋值目标来引用序列中的当前项，就好像它是一个在序列中移动的游标。从技术上讲，for 通过重复对序列对象进行索引（从零开始，索引依次增加），直到引发索引越界异常来实现。由于 for 循环在后台自动管理序列索引，它替代了你可能习惯于在 C 等语言中编写的许多计数器风格的循环。”

换句话说，当 for 循环开始时，它查看列表中的第一项。该项被赋予值 0（许多编程语言从 0 开始计数，而不是 1）。一旦代码块完成其处理，*for* 循环查看第二个值并赋予其值 1。再次地，代码块完成其处理，*for* 循环查看下一个值并赋予其值 2。这个序列持续进行，直到列表中不再有值为止。在那一点上，*for* 循环停止，控制权转移到程序中的下一条语句。

示例 11.10 展示了一个实用的 *for* 循环版本，实现了 *break* 和 *else* 语句，如**Python 文档**中所述。

示例 11.10：*break* 和 *else* 语句

```python
>>> for n in range(2, 10):
...     for x in range(2, n):
...         if n % x == 0:    #if the remainder
...             #of n/x is 0
...             print n, 'equals', x, '*', n/x
...             break    #exit immediately
...     else:
...         # loop fell through without finding a
...         #factor
...     print n, 'is a prime number'

2 is a prime number
3 is a prime number
4 equals 2 * 2
5 is a prime number
6 equals 2 * 3
7 is a prime number
8 equals 2 * 4
9 equals 3 * 3
```

与 *for* 循环相关的是 *range* 和计数器循环。**range()** 函数会自动为你构建一个整数列表。通常它用于为 *for* 语句创建索引，但你可以在任何地方使用它。

示例 11.11：使用 **range()** 函数

```python
>>> range(5) #create a list of 5 numbers, starting
... at 0
[0, 1, 2, 3, 4]
>>> range(2, 5) #start at 2 and end at 5 (remember
... the index values)
[2, 3, 4]
>>> range(0, 10, 2) #start at 0, end at 10 (index
... value), with an increment of 2
[0, 2, 4, 6, 8]
```

如你所见，单个参数会给你一个整数列表，从 0 开始，到参数减一结束（因为索引的原因）。两个参数提供起始数字和最大值，而三个参数则增加了一个步长值，即每个值之间跳过多少个数字。

计数器循环只是计算循环已处理的次数。在循环结束时，一个变量会自增，以表明循环已完成。一旦达到特定次数的循环，循环就会执行，然后程序的其余部分被执行。

### 11.7 pass 语句

pass 语句只是告诉 Python 继续移动，这里没有实质内容。通常，pass 语句在最初编写程序时使用。你可能创建了一个函数的引用，但尚未实际实现其代码。然而，Python 将寻找该函数内部的某些内容。如果没有可处理的内容，Python 解释器在找不到任何东西时会引发异常并停止。如果你只是在函数中放入一个 pass 语句，它将不会停止地继续运行。

示例 11.12：pass 语句

```python
if variable > 12:
    print "Yeah, that's a big number."
else: pass
```

### 11.8 break 和 continue 语句

前面已提到，这两个语句影响循环内的流程控制。当满足特定条件时，break 语句会“跳出”循环，从而有效地提前结束循环（虽然是以预期的方式）。continue 语句会使循环“短路”，立即使流程控制返回循环顶部。

我很少使用这些语句，但在需要时它们很有用。它们有助于确保你不会永远卡在循环中，也确保你不会没有正当理由而持续迭代循环。

### 11.9 try, except, finally 和 raise 语句

我简要提及了其中一些，将在异常章节中更详细地讨论它们。简要来说，try 创建一个尝试执行操作的块。如果该操作失败，except 块捕获引发的任何异常并对其进行处理。finally 无论是否引发异常，都会执行最后的一些操作。raise 语句手动创建异常。

### 11.10 import 和 from 语句

这两个语句用于包含你希望在程序中使用的其他 Python 库和模块。这有助于保持程序小巧（你不需要将所有代码放在单个模块中）并“隔离”模块（你只导入你需要的内容）。import 实际调用了其他库或模块，而 from 使导入语句具有选择性；你只导入模块的子集，最小化带入程序的代码量。

### 11.11 def 和 return 语句

这些用于函数和方法。函数用于过程式编程，而方法用于面向对象编程。*def* 语句定义函数/方法。*return* 语句从函数或方法返回一个值，允许你将返回值赋值给变量。

示例 11.13：定义函数

```python
>>> a = 2
>>> b = 5
>>> def math_function ():
...     return a * b
...
>>> product = math_function ()
>>> product
10
```

### 11.12 Class 语句

这些是 OOP 的构建块，*class* 创建一个新的对象。该对象可以是任何东西，无论是抽象数据概念还是物理对象的模型，例如椅子。每个类都有独特于该类的特征，包括变量和方法。类非常强大，目前在大多数编程语言中都是“热门话题”。因此，书中后面有专门几章致力于 OOP。

