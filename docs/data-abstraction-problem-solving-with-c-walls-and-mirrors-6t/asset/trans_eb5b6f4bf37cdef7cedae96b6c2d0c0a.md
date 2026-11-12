

success = true
else
{
    success = goNorth(maze, creature)
    if (success)
    {
        success = goWest(maze, creature)
        if (success)
        {
            success = goEast(maze, creature)
            if (success)
            {
                Mark square visited
                Backtrack south
            }
        }
    }
}
else
success = false
return success

goWest 函数将按如下方式检查从当前方块以西的方块开始的所有路径。如果正西方的方块是畅通的、在迷宫内部，并且之前未被访问过，则移入该方块并将其标记为路径的一部分。（请注意，您是从东边移动的。）检查您是否到达出口。如果是，则任务完成。否则，尝试从这里寻找通往出口的路径，方法是尝试从该方块出发的所有路径，除了向东的那条路径（那会把您带回刚才来的方块）（如下所示。调用 goNorth，如果不成功，则调用 goWest；如果也不成功，则调用 goSouth。如果 goSouth 不成功，则将该方块标记为已访问，移回东边的方块，并返回。函数 goEast 和 goSouth 与 goWest 和 goNorth 类似。

表示迷宫的输入数据很简单。例如，之前给出的迷宫由以下输入行表示，这些行可以位于文本文件中：

```
20 7      <- width and height of the maze in squares
0 18      <- row and column coordinate of maze exit
6 12      <- row and column coordinate of maze entrance
xxxxxxxxxxxxxxxxxx x
x   x
x xxxxx xxxxx x x
x xxxxx xxxxx x x
x xxxxx xxxxx xx x
x xxxxx xxxxx xx x
x xxxxxxxxxx xx x
xxxxxxxxxxxxxx xxxxxxx
```

在文件中前三行数值数据之后，接下来的每一行都对应迷宫中的一行，每行中的每个字符都对应迷宫中的一列。x 表示被阻塞的方块（墙的一部分），而空格表示畅通的方块。这种表示法很方便，因为您在设计迷宫时可以看到它的样子。

- 5. 编写一个程序来识别和求值前缀表达式。首先设计并实现一个前缀表达式类。该类应包含识别和求值前缀表达式的方法。本章讨论了实现这些方法所需的算法。

- 6. 实现练习 5 中语言的识别算法。

- 7. 实现本章中描述的算法，将前缀表达式转换为后缀形式。

- 8. 以下是一种语法，当优先级规则消除歧义时，它允许您在中缀代数表达式中省略括号。例如，a + b * c 表示 a + (b * c)。但是，当否则会产生歧义时，该语法要求使用括号。也就是说，当多个运算符具有相同优先级时，该语法不允许从左到右的结合。例如，a / b * c 是非法的。请注意，定义中引入了因子和项。

```
<expression> = <term>|<term> + <term>| <term> - <term>
<term> = <factor>|<factor>*<factor>| <factor>/<factor>
<factor> = <letter>|(<expression>)
<letter> = a | b | ... | z
```

识别算法基于一系列子任务的递归链：查找表达式 → 查找项 → 查找因子。使其成为递归链的是，查找表达式使用查找项，而查找项又使用查找因子。查找因子要么检测基本情况，要么使用查找表达式，从而形成递归链。识别算法的伪代码如下：

```
FIND AN EXPRESSION
// The grammar specifies that an expression is either a single term
// or a term followed by a + or a -, which then must be followed by a second term.
Find a term
if (the next symbol is + or -)
    Find a term
FIND A TERM
// The grammar specifies that a term is either a single factor or
// a factor followed by a * or a /, which must then be followed by a second factor.
Find a factor
if (the next symbol is * or /)
    Find a factor
FIND A FACTOR
// The grammar specifies that a factor is either a single letter (the base case) or
// an expression enclosed in parentheses.
// if (the first symbol is a letter)
Done
else if (the first symbol is a '(')
    Find an expression starting at the character after '('
    Check for ')'
else
    No factor exists
```

根据给定的语法设计并实现一个中缀表达式类。包括一个识别合法中缀表达式的方法。

## 栈

## 目录

- 6.1 抽象数据类型栈 194
- 6.1.1 在解决方案设计过程中开发 ADT 194
- 6.1.2 ADT 栈的规格说明 196
- 6.2 栈的简单用途 201
- 6.2.1 检查平衡括号 201
- 6.2.2 识别语言中的字符串 203
- 6.3 在代数表达式中使用栈 205
- 6.3.1 求值后缀表达式 205
- 6.3.2 将中缀表达式转换为等价后缀表达式 206
- 6.4 使用栈搜索航班地图 210
- 6.5 栈与递归的关系 216
- 小结 218
- 练习 218
- 编程问题 221

## 先决条件

- 第 1 章 数据抽象：墙壁
- C++ 间奏曲 1 C++ 类

迄今为止，在本书中，我们已讨论了与解决方案设计相关的数据抽象，介绍了 C++ 类作为隐藏解决方案实现的一种方式，介绍了可调整大小的数组和链接节点作为许多 ADT 实现中使用的数据结构，并开发了递归作为构建算法时有用的问题求解技术。本书其余部分的主要关注点是涉及数据管理的问题求解方面——即识别和实现一些更常见的数据管理操作。

我们对数据管理的研究有三个目标。第一个是识别有用的操作集——即识别抽象数据类型。第二个目标是考察使用这些抽象数据类型的应用程序。第三个目标是为抽象数据类型构建实现——即开发数据结构和类。正如您将会发现的，抽象数据类型的操作性质，以及您将使用它的应用程序，极大地影响其实现的选择。

第 1 章中讨论的 ADT 袋不组织其数据。但是，您可以按位置或按值组织数据。通常，这些组织方式适用于性质截然不同的应用程序。例如，如果应用程序需要询问队列中第一个人的问题，则应按位置组织数据。另一方面，如果应用程序需要询问名为 Smith 的员工的问题，则应按值组织数据。在本书其余部分中，您将看到几个使用这两种数据组织方式的 ADT。

本章介绍了一种名为栈的著名 ADT。您将看到栈上的操作如何使其具有后进先出（LIFO）行为。本章考虑的栈的几个应用中有两个是求值代数表达式和查找两点之间的路径。最后，本章讨论了栈与递归之间的重要关系。我们将栈的实现留到下一章。

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_220_0.png)

## 6.1 抽象数据类型栈

您可以用来解决特定问题的抽象数据类型的规范可以在问题解决方案的设计过程中出现。以下示例中开发的 ADT 正好是一个重要的 ADT：即 ADT 栈。

### 6.1.1 在解决方案设计过程中开发 ADT

在键盘上输入一行文本时，您可能会出错。如果使用 Backspace 键更正这些错误，每个退格键都会擦除之前输入的字符。连续的退格键会按顺序应用，从而擦除多个字符。例如，如果您输入以下行

```
abcc<--dddd<--<--eg<-fg
```

其中 <- 表示退格字符，更正后的输入将是 abcdefg

程序如何读取原始行并获得正确的输入？在设计此问题的解决方案时，您最终必须决定如何存储输入行。根据 ADT 方法，您应推迟此决定，直到您更清楚需要对数据执行哪些操作。

解决方案的第一个尝试导致以下伪代码：

```
// Read the line, correcting mistakes along the way
// while (not end of line)
{
    Read a new character ch
    if (ch is not a '<-')
        Add ch to the ADT
    else
        Remove from the ADT (discard) the item that was added most recently
}
```

解决方案的初始草稿

