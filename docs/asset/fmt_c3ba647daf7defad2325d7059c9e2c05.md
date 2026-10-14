
如果提供了`sep`，连续的分隔符不会合并在一起，并且被视为界定空字符串（例如，`'1,2'.split(',')` 返回 `['1', '', '2']`）。`sep` 参数可以由多个字符组成（例如，`'1<<2<<3'.split('<<')` 返回 `['1', '2', '3']`）。使用指定的分隔符分割空字符串返回 `['']`。

如果未指定 `sep` 或为 `None`，则应用不同的分割算法：连续的空格序列被视为单个分隔符，并且如果字符串有前导或尾部空格，结果将不包含开头或结尾的空字符串。因此，使用 `None` 分隔符分割空字符串或仅由空格组成的字符串返回 `[]`。

例如，`'1 2 3'.split()` 返回 `['1', '2', '3']`，而 `'1 2 3'.split(None, 1)` 返回 `['1', '2 3']`。

### `str.splitlines([keeplines])`

返回字符串中行的列表，在行边界处断开。除非提供了 `keepends` 且为真，否则结果列表中不包含换行符。

### `str.startswith(*prefix*[, *start*, *end*])

如果字符串以 `prefix` 开头，则返回 `True`，否则返回 `False`。`prefix` 也可以是用于查找的前缀元组。通过可选参数 `start`，从该位置开始测试字符串。通过可选参数 `end`，在该位置停止比较字符串。

### `str.strip([*chars*])`

返回去除了前导和尾部字符的字符串副本。`chars` 参数是一个指定待删除字符集的字符串。如果省略或为 `None`，`chars` 参数默认为删除空白字符。`chars` 参数不是前缀或后缀；而是移除其值的所有组合。

### `str.swapcase()`

返回转换大小写的字符串副本：大写字符转换为小写，反之亦然。

### `str.title()`

返回标题化版本的字符串：单词以大写字符开头，所有其余的大小写字符均为小写。还有一个方法 `istitle()` 用于判断字符串是否已标题化。

### `str.upper()`

返回转换为大写的字符串副本。

### 附录 B

#### 列表方法

尽管这是一个完整的方法列表，有关 Python 列表的更多信息可以在 Python 网站关于数据结构的讨论中找到。

- `list.append(x)`

  – 在列表末尾添加一项；等效于 `a[len(a):] = [x]`。

- `list.extend(L)`

  – 通过追加给定列表中的所有项来扩展列表；等效于 `a[len(a):] = L`。

- `list.insert(i, x)`

  – 在给定位置插入一项。第一个参数是要插入的元素之前的索引，因此 `a.insert(0, x)` 在列表前端插入，`a.insert(len(a), x)` 等效于 `a.append(x)`。

- `list.remove(x)`

  – 从列表中移除值为 `x` 的第一项。如果不存在该项，则引发错误。

- `list.pop([i])`

  – 移除列表中给定位置的项，并返回该项。如果未指定索引，`a.pop()` 移除并返回列表中的最后一项。（方法签名中 `i` 周围的方括号表示该参数是可选的，而不是你应该在该位置输入方括号。你在 Python 库参考中会经常看到这种表示法。）

- `list.index(x)`

  – 返回列表中第一个值为 `x` 的项的索引。如果不存在该项，则引发错误。

- `list.count(x)`

  – 返回 `x` 在列表中出现的次数。

- `list.sort()`

  – 就地对列表中的项进行排序。

- `list.reverse()`

  – 就地反转列表中的元素。

### 附录 C

#### 字典操作

这些操作以及字典的一般完整文档可以在 Python 文档中找到。

- `len(d)`

  – 返回字典 `d` 中项的数量。

- `d[key]`

  – 返回 `d` 中以 `key` 为键的项。如果 `key` 不在映射中，则引发 `KeyError`。

- `d[key] = value`

  – 将 `d[key]` 设置为 `value`。

- `del d[key]`

  – 从 `d` 中移除 `d[key]`。如果 `key` 不在映射中，则引发 `KeyError`。

- `key in d`

  – 如果 `d` 有键 `key`，则返回 `True`，否则返回 `False`。

- `key not in d`

  – 等效于 `not key in d`。

- `clear()`

  – 移除字典中的所有项。

- `copy()`

  – 返回字典的浅拷贝。

- `fromkeys(seq[, value])`

  – 创建一个新字典，其键来自 `seq`，值设置为 `value`。

  – `fromkeys()` 是一个类方法，返回一个新字典。`value` 默认为 `None`。

- `get(key[, default])`

  – 如果 `key` 在字典中，则返回 `key` 的值，否则返回 `default`。如果未提供 `default`，则默认为 `None`，因此该方法从不引发 `KeyError`。

- `items()`

  – 返回字典的 `(key, value)` 对列表的副本。注意：键和值的列表顺序是任意的，非随机的，因 Python 实现而异，并取决于字典的插入和删除历史。如果调用 `items()`、`keys()`、`values()`、`iteritems()`、`iterkeys()` 和 `itervalues()` 且中间没有对字典进行修改，则这些列表将直接对应。这使得可以使用 `zip()` 创建 `(value, key)` 对：`pairs = zip(d.values(), d.keys())`。`iterkeys()` 和 `itervalues()` 方法也保持相同的关系：`pairs = zip(d.itervalues(), d.iterkeys())` 为 `pairs` 提供相同的值。创建相同列表的另一种方式是 `pairs = [(v, k) for (k, v) in d.iteritems()]`。

- `iteritems()`

  – 返回用于遍历字典 `(key, value)` 对的迭代器。参见 `dict.items()` 的注意事项。

- `iterkeys()`

  – 返回用于遍历字典键的迭代器。参见 `dict.items()` 的注意事项。

- `itervalues()`

  – 返回用于遍历字典值的迭代器。参见 `dict.items()` 的注意事项。

- `keys()`

  – 返回字典的键列表的副本。参见 `dict.items()` 的注意事项。

- `pop([key[, default]])`

  – 如果 `key` 在字典中，移除它并返回其值，否则返回 `default`。如果未提供 `default` 且 `key` 不在字典中，则引发 `KeyError`。

- `popitem()`

  – 从字典中移除并返回一个任意的 `(key, value)` 对。

  – `popitem()` 有助于以破坏性的方式迭代字典，常用于集合算法。如果字典为空，调用 `popitem()` 将引发 `KeyError`。

- `setdefault(key[, default])`

  – 如果 `key` 在字典中，返回其值。如果没有，插入 `key` 并赋值为 `default`，然后返回 `default`。`default` 默认为 `None`。

- `update([other])`

  – 使用 `other` 中的键/值对更新字典，覆盖现有的键。返回 `None`。

### 附录 D

#### 运算符

表 D.1 列出了 Python 中常见的运算符。这些包括标准数学函数、逻辑运算符等。

##### 表 D.1：Python 运算符

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

### 附录 E

#### 示例程序

本节中的所有程序都是为 Python 2.6 或更低版本编写的。然而，这些程序可以在本书的网站上以电子形式获取，并提供 Python 2.x 和 Python 3.x 两个版本。如果您下载了种子文件，那么其中包含了所有软件版本。

##### E.1 掷骰子模拟器

列表 D.1（注：此处原文引用可能有误，下文对应 E.1）是我编写过的最早期的程序之一。我列出了完整的源代码，以展示一个编写良好的程序应包含的各种特性。请先查看代码，之后我将讨论其各个部分。

**列表 E.1：随机骰子滚动器**

```python
##############################################
#Dice_roller.py
#
#Purpose: A random number generation program that simulates
###### various dice rolls.
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

第 30 行从 Python 标准库导入了 `random` 模块。这用于调用 `randint()` 函数来实现程序的随机化部分。第 32-51 行是随机数生成器的实现位置。用户决定要掷哪种骰子，例如 6 面骰或 10 面骰，程序则返回一个随机数。该随机数是一个整数，其值域由用户决定。按照目前的写法，这个生成器程序可以用于多种不同的游戏，从棋盘游戏到角色扮演游戏。

第 53-63 行定义了实际返回模拟掷骰结果的函数。它从用户处接收骰子类型和要“掷”的数量，然后调用前一个代码块中的随机数函数。该函数包含一个 while 循环，它会持续掷骰子，直到达到用户指定的数量，然后返回最终值。

第 65-83 行构成了 `test()` 函数。这是 Python 程序的一个常见功能；它允许程序员验证程序是否正常工作。例如，如果该程序被包含在一个电脑游戏中，但该游戏在掷骰子方面似乎存在问题，通过单独调用此程序，`test()` 函数会被自动调用（由第 85 和 86 行触发）。因此，开发人员可以快速判断此程序的结果是否合理，并决定它是否是导致游戏问题的原因。

如果此程序在没有参数的情况下被单独调用，第 85 和 86 行会调用 `test()` 函数并显示各种结果。然而，如果该程序带参数调用，即从命令行调用或作为独立程序的一部分，则第 85 和 86 行会被忽略，`test()` 函数永远不会被调用。
