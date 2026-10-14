

## 附录 D

### 运算符

表 D.1 列出了 Python 中常见的运算符。这些包括标准数学函数、逻辑运算符等。

#### 表 D.1：Python 运算符

| 符号 | 类型 | 功能 |
| :--- | :--- | :--- |
| + | 数学 | 加法 |
| - | 数学 | 减法 |
| * | 数学 | 乘法 |
| / | 数学 | 除法（浮点数） |
| // | 数学 | 除法（截断） |
| ** | 数学 | 幂运算 |
| % | 取模 | 返回除法的余数 |
| << | 位移 | 左移（按位） |
| >> | 位移 | 右移（按位） |
| & | 逻辑 | 与 |
| | | 逻辑 | 或 |
| ^ | 逻辑 | 按位异或 |
| ~ | 逻辑 | 按位取反 |
| < | 比较 | 小于 |
| > | 比较 | 大于 |
| == | 比较 | 完全相等 |
| != | 比较 | 不相等 |
| >= | 比较 | 大于或等于 |
| <= | 比较 | 小于或等于 |
| = | 赋值 | 分配值 |
| += | 赋值 | 加法并赋值 |
| -= | 赋值 | 减法并赋值 |
| *= | 赋值 | 乘法并赋值 |
| /= | 赋值 | 除法并赋值 |
| //= | 赋值 | 截断除法并赋值 |
| **= | 赋值 | 幂运算并赋值 |
| %= | 赋值 | 取模并赋值 |
| >>= | 赋值 | 右移并赋值 |
| <<= | 赋值 | 左移并赋值 |
| And | 布尔 | |
| Or | 布尔 | |
| Not | 布尔 | |

## 附录 E

### 示例程序

本节中的所有程序都是为 Python 2.6 或更低版本编写的。然而，这些程序可以在本书的网站上以电子形式获取，并提供 Python 2.x 和 Python 3.x 两个版本。如果您下载了种子文件，那么其中包含了所有软件版本。

#### E.1 掷骰子模拟器

列表 D.1（注：此处原文引用可能有误，下文对应 E.1）是我编写过的最早期的程序之一。我列出了完整的源代码，以展示一个编写良好的程序应包含的各种特性。请先查看代码，之后我将讨论其各个部分。

**列表 E.1：随机骰子滚动器**

```python
##############################################
#Dice_roller.py
#
#Purpose: A random number generation program that simulates
#         various dice rolls.
#Author: Cody Jackson
#Date: 4/11/06
#
#Copyright 2006 Cody Jackson
#
#This program is free software; you can
#redistribute it and/or modify it
#under the terms of the GNU General Public License
#as published by the Free
#Software Foundation; either version 2 of the
#License, or (at your option)
#any later version.
#
#This program is distributed in the hope that it
#will be useful, but
#WITHOUT ANY WARRANTY; without even the implied
#warranty of
#MERCHANTABILITY or FITNESS FOR A PARTICULAR
#PURPOSE. See the GNU
#General Public License for more details.
#
#You should have received a copy of the GNU
#General Public License
#along with this program; if not, write to the
#Free Software Foundation,
#Inc., 59 Temple Place, Suite 330, Boston, MA
#02111-1307 USA
#
#Version 1.0
#
#Initial build
#Version 2.0
#
#Added support for AD&D 1st edition dice (d4,
#d8, d12, d20)
################################################

import random #randint

def randomNumGen(choice):
    """Get a random number to simulate a d6, d10,
    or d100 roll."""
    
    if choice == 1: #d6 roll
        die = random.randint(1, 6)
    elif choice == 2: #d10 roll
        die = random.randint(1, 10)
    elif choice == 3: #d100 roll
        die = random.randint(1, 100)
    elif choice == 4: #d4 roll
        die = random.randint(1, 4)
    elif choice == 5: #d8 roll
        die = random.randint(1, 8)
    elif choice == 6: #d12 roll
        die = random.randint(1, 12)
    elif choice == 7: #d20 roll
        die = random.randint(1, 20)
    else: #simple error message
        print "Shouldn't be here. Invalid choice"
    return die

def multiDie(dice_number, die_type):
    """Add die rolls together, e.g. 2d6, 4d10, etc
        ."""
    #---- Initialize variables
    final_roll = 0
    val = 0

    while val < dice_number:
        final_roll += randomNumGen(die_type)
        val += 1
    return final_roll

def test():
    """Test criteria to show script works."""

    _1d6 = multiDie(1,1)    #1d6
    print "1d6 = ", _1d6,
    _2d6 = multiDie(2,1)    #2d6
    print "\n2d6 = ", _2d6,
    _3d6 = multiDie(3,1)    #3d6
    print "\n3d6 = ", _3d6,
    _4d6 = multiDie(4,1)    #4d6
    print "\n4d6 = ", _4d6,
    _1d10 = multiDie(1,2)   #1d10
    print "\n1d10 = ", _1d10,
    _2d10 = multiDie(2,2)   #2d10
    print "\n2d10 = ", _2d10,
    _3d10 = multiDie(3,2)   #3d10
    print "\n3d10 = ", _3d10,
    _d100 = multiDie(1,3)   #d100
    print "\n1d100 = ", _d100,

if __name__ == "__main__":  #run test() if calling
    # as a separate program
    test()
```

第一部分（第 1-28 行）是描述性标题和许可证信息。它给出了文件名、用途声明、作者、创建日期以及分发的许可证类型。在这种情况下，我是在 GNU 通用公共许可证（GPL）下发布该软件的，这意味着任何人都可以自由地获取和使用此软件，只要它在 GPL 条款下保持“自由”（即言论/行动的自由，而非免费）。为了方便，我在附录 F 中包含了 GPL 的副本。显然，您可以自由选择使用何种类型的许可证来发布您的软件，无论是将其作为开源软件发布，还是完全将其作为专有软件锁定。

第 30 行从 Python 标准库导入了 random 模块。这用于调用 `randint()` 函数来实现程序的随机化部分。第 32-51 行是随机数生成器的实现位置。用户决定要掷哪种骰子，例如 6 面骰或 10 面骰，程序则返回一个随机数。该随机数是一个整数，其值域由用户决定。按照目前的写法，这个生成器程序可以用于多种不同的游戏，从棋盘游戏到角色扮演游戏。

第 53-63 行定义了实际返回模拟掷骰结果的函数。它从用户处接收骰子类型和要“掷”的数量，然后调用前一个代码块中的随机数函数。该函数包含一个 while 循环，它会持续掷骰子，直到达到用户指定的数量，然后返回最终值。

第 65-83 行构成了 **test()** 函数。这是 Python 程序的一个常见功能；它允许程序员验证程序是否正常工作。例如，如果该程序被包含在一个电脑游戏中，但该游戏在掷骰子方面似乎存在问题，通过单独调用此程序，**test()** 函数会被自动调用（由第 85 和 86 行触发）。因此，开发人员可以快速判断此程序的结果是否合理，并决定它是否是导致游戏问题的原因。

如果此程序在没有参数的情况下被单独调用，第 85 和 86 行会调用 **test()** 函数并显示各种结果。然而，如果该程序带参数调用，即从命令行调用或作为独立程序的一部分，则第 85 和 86 行会被忽略，**test()** 函数永远不会被调用。

这是一个非常简单的程序，但它具备了 Python 的许多基本组成部分。它包含 *if/else* 语句、*while* 循环、返回语句、函数、模块导入等。您可以随意修改此程序，或者尝试编写类似的程序，例如一个发牌模拟器。您对编写简单程序越熟练，当您的程序变大并包含更多功能时，工作就会越轻松。

#### E.2 温度转换

**列表 E.2：华氏转摄氏转换器**

```python
#################################################
#Create a chart of fahrenheit to celsius conversions from 0 to 100 degrees.
#Author: Cody Jackson
#Date: 4/10/06
#################################################

def fahrenheit(celsius):
    """Converts celsius temperature to fahrenheit """
```

