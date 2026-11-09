

### 输出：

```
8 + 2 = [        ]
```

这是一个游戏，你需要找出两个整数 n1 和 n2 的基本数学运算

游戏会持续要求输入这 4 个问题的答案，下面是所有答案输入后的最终输出。

```
This is a game where you find basic mathematical operations for 2 integer numbers n1 and n2

8 + 2 = 10
8 - 2 = 6
8 * 2 = 16
8 % 2 = 0

You have got 4 answers correct
```

这是一个很棒的练习程序。但你可能会想，孩子们只能使用这个程序一次，因为我们总是使用相同的数字。为了解决这个问题，我们在下一个游戏中生成随机数。

## 游戏 3 – 随机数数学测验

在下面的程序中，有 5 道数学题由 10 个随机数生成。这 10 个随机数是变量 **n1** 到 **n10**。问题的答案被计算出来并存储在变量 **ans1** 到 **ans5** 中。这 15 个变量被称为全局变量，因为它们位于任何函数之外。这意味着它们的值可以在程序中的任何位置被任何函数访问。函数 **print_ans()** 使用 5 个变量 **ans1** 到 **ans5** 来写出测验答案。这些答案（**answer1-answer5**）会使用 **check_ans** 函数中的 5 个不同 if 条件语句与用户答案（**user_ans1- user_ans5**）进行核对。每当有一个正确答案时，计数器就会递增。最后，打印计数器以显示正确答案的数量。这些问题是随机生成的，这意味着用户每次都会得到不同的问题。

### 程序

```python
#Game 3 - Math Quiz with Random Numbers

import random

Max_int = 10

# Assign random integers between 1 and Max_int inclusive
n1 = random.randint(1, Max_int)
n2 = random.randint(1, Max_int)
n3 = random.randint(1, Max_int)
n4 = random.randint(1, Max_int)
n5 = random.randint(1, Max_int)
n6 = random.randint(1, Max_int)
n7 = random.randint(1, Max_int)
n8 = random.randint(1, Max_int)
n9 = random.randint(1, Max_int)
n10 = random.randint(1, Max_int)

ans1 = n1 + n2
ans2 = n3 - n4
ans3 = n5 * n6
ans4 = n7 * n8
ans5 = n9 % n10

user_ans1 = int(input(f"{n1} + {n2} = "))
user_ans2 = int(input(f"{n3} - {n4} = "))
user_ans3 = int(input(f"{n5} * {n6} = "))
user_ans4 = int(input(f"{n7} * {n8} = "))
user_ans5 = int(input(f"{n9} % {n10} = "))
print()
```

### 输出：

```
7 + 6 = 13
7 - 10 = -3
2 * 1 = 2
6 * 2 = 12
2 % 7 = 0

Answer 1 = 13
Answer 2 = -3
Answer 3 = 2
Answer 4 = 12
Answer 5 = 2
```

你答对了 4 道题。

### 练习题

- 1. 编写一个程序，生成两个 0 到 10（含）之间的随机数。然后输出它们的和、乘积、余数和幂。
- 2. 编写一个随机密码生成器，程序从用户处获取密码长度 n，并创建 n 位长的密码。
- 3. 编写一个程序，从用户处获取三角形的 3 条边长，然后判断它是锐角、直角还是钝角三角形（提示：使用勾股定理进行检查）。

## 列表、元组和字典

### 数据结构简介

数据结构是用于存储和分组数据的结构，以便能够轻松访问并高效操作数据。每种数据结构都有其优缺点。选择特定数据结构取决于你想要优化的方面。有不同方面可以优化，例如访问速度、存储大小或数据修改速度。这些方面中的每一个都需要针对该方面优化的不同类型的数据结构。

在本章中，我们将探索三种基本的 Python 内置数据结构：列表、元组和字典。这些数据结构非常有用。它们使你的程序更易于编写且更高效，而且你不必从头实现自己的数据结构。请注意，这些数据结构也称为容器，因为它们持有/包含其他对象。

### 列表

列表是存储项目集合的序列。列表因其多功能性而成为最常用的容器之一。列表可以保存不同类型的数据。它们是异构的，意味着它们不必存储相似的数据类型。列表是可变的，因此你可以在创建列表后修改它。

要创建列表，请将逗号分隔的值放在方括号中。

```
my_list = []  or
my_list = list()
```

下面的代码创建数字列表、字符串列表，以及同时包含数字和字符串的异构列表。

```python
# create list either by square brackets or list()
my_list = []
my_list = list()

# Define list L1, L2, L3
# list1 sequence of numbers
list1 = [1, 2, 3]

# list2 sequence of strings
list2 = ["Nick", "Tom", "Jane"]

# list3 sequence of numbers and strings
list3 = ["Nick", 10, "Python", 50]

# list4 a list containing other lists
list4 = [list1, list2, list3]

print("list1 is:", list1)
print("list2 is:", list2)
print("list3 is:", list3)
print("list4 is:", list4)

list1 is: [1, 2, 3]
list2 is: ['Nick', 'Tom', 'Jane']
list3 is: ['Nick', 10, 'Python', 50]
list4 is: [[1, 2, 3], ['Nick', 'Tom', 'Jane'], ['Nick', 10, 'Python', 50]]
```

### 列表方法

与前面章节讨论的字符串方法类似。列表附带了有用的方法可供使用。我们将在这里学习常用的列表方法；要查找并学习更多方法，请访问以下 Python 文档链接。
[https://docs.python.org/3/tutorial/datastructures.html](https://docs.python.org/3/tutorial/datastructures.html)

### 基本列表操作

下表总结了基本列表操作。

| 表达式 | 名称 | 输出 |
|---|---|---|
| `len(['a', 'b', 'c'])` | 长度 | `3` |
| `['a', 'b', 'c'] + ['d', 'e', 'f']` | 列表拼接 | `['a', 'b', 'c', 'd', 'e', 'f']` |
| `['Hi!'] * 4` | 重复 | `['Hi!', 'Hi!', 'Hi!', 'Hi!']` |
| `'a' in ['a', 'b', 'c']` | 成员关系 | `True` |
| `for num in [1, 2, 3]:<br>    print(num)` | 列表迭代 | `1<br>2<br>3` |
| `n = ['a', 'b', 'c']<br>n[0] = 'z'<br>print(n)` | 列表元素赋值 | `['z', 'b', 'c']` |

- **list[index]** – 索引运算符，从列表中选择单个值。方括号内的数字称为索引，它是一个整数值。Python 中的索引从零开始。与字符串类似，你也可以使用负索引，此时会从后向前开始索引。

```
list1 = ['Python', 'C++', 'C', 'Java Script']
list1[0] value is 'Python'
list1[2] value is 'C'
list1[-1] value is 'Java Script'
list1[-2] value is 'C'
```

- **list[starting_index: ending_index]** – 切片运算符，从起始索引处切片列表，并在结束索引前一个元素处结束。

```
list1 = ['Python', 'C++', 'C', 'Java Script']
list1[0:2] = ['Python', 'C++']
list1[0:-1] = ['Python', 'C++', 'C']
```

- **list.append(elem)** – *将元素追加到列表。*

```
list1 = [1, 2, 3]
list1.append(4)
list1 value is [1, 2, 3, 4]
```

- **list.clear()** – 清除列表值。

```
list1 = [1,2,3]
list1.clear()
list1 value is []
```

- **list.count(elem)** – 统计元素 elem 在列表中出现的次数。

```
list1 = [1,2,2,2,3,4]
list1.count(2) outputs 3
```

- **list.extend(list2)** — 将 list2 的元素添加到列表中。此方法执行与使用 '+' 运算符进行列表拼接相同的工作。

```
list1 = [1, 2, 3]
list2 = [4, 5]
list1.extend(list2)
list1 is [1,2,3,4,5]
```

- **list.insert(elem_index, elem)** — 将元素 elem 插入到列表中的索引 elem_index 处。

```
list1 = [1, 2, 3]
list1.insert(3, 4)
list1 is [1,2,3,4]
```

- **list.pop()** — 移除列表的最后一个元素。

```
list1 = [1, 2, 3, 4]
list1.pop() removes 4
list1 is [1,2,3]
```

- **list.index(elem)** — 返回 elem 第一次出现的索引。

```
list1 = [1, 2, 3, 4]
list1.index(2) returns 3
```

### 示例 1：列表基本操作

这里我们有一个综合示例，演示上面讨论的各种列表方法。请试验这段代码以理解它。

```python
# List basic operations

# List iteration and indexing
even_nums = [0, 2, 4, 6, 8, 10]

# Length of even_nums list
print("Length of even_nums list is:", len(even_nums))
print('\n')

print("Even numbers are:")
for number in even_nums:
    print(number)

# print 2 new lines, new line symbol is \n
print('\n')

# Slicing
# print even number list less than 5
even_nums_less_5 = even_nums[0:3]
print("Even numbers less than 5 are: ", even_nums_less_5)
print('\n')

# Append additional even number
even_nums.append(12)
print("Even number list after appending is: ", even_nums)
print('\n')

# count how many times 12 is in list
count = even_nums.count(12)
print(f"12 occurs {count} times in even_nums list")
print('\n')
```

