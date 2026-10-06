

## 5.3 计数控制循环与 For 语句

你应该注意，不要在 For 循环体内部放置修改计数器变量的语句。这样做通常会破坏 For 循环的工作机制。

图 5-14 程序 5-8 的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_219_0.png)

> 提示：程序 5-8 有一个常量 MAX_VALUE，它代表计数器变量的最大值。循环的第一行可以写如下，以达到相同的结果：
For counter = 1 To 5
虽然对于这个简单的程序来说，创建命名常量并不是必要的，但创建命名常量来表示重要数值是一个良好的习惯。回想第 2 章，命名常量使程序更易阅读、更易维护。

此语句显示计数器变量的内容。

## 5.3 计数控制循环与 For 语句

图 5-15 显示 1 到 10 的数字及其平方

![](img/c939132f78787c7f339c6977b3fc8c85_221_0.png)

# 程序 5-9

```
// Variables
Declare Integer counter, square
// 用于最大值的常量
Constant Integer MAX_VALUE = 10

// 显示表头。
Display "Number", Tab, "Square"
----------------------

// 显示 1 到 10 的数字
// 它们的平方。
For counter = 1 To MAX_VALUE
  // 计算数字的平方。
  Set square = counter * counter
  // 显示数字和数字平方。
  Display counter, Tab, square
End For
```

# 程序输出

| Number | Square |
| --- | --- |
| 1 | 1 |
| 2 | 4 |
| 3 | 9 |
| 4 | 16 |
| 5 | 25 |
| 6 | 36 |
| 7 | 49 |
| 8 | 64 |
| 9 | 81 |
| 10 | 100 |

# 按非 1 的值递增

For 循环中计数器变量递增的幅度称为步长（step amount）。默认情况下，步长为 1。大多数语言提供了更改步长的方法。这让你能够以任何想要的值递增计数器变量。

在伪代码中，我们使用可选的 Step 子句来指定 For 循环中的步长值。例如，看以下伪代码：

```
For counter = 0 To 100 Step 10
  Display counter
End For
```

## 5.3 计数控制循环与 For 语句

在这个循环中，计数器变量的起始值为 0，结束值为 100。Step 子句指定的步长值为 10，这意味着在每次迭代结束时，计数器都会加 10。在第一次迭代中，counter 为 0；在第二次迭代中，counter 为 10；在第三次迭代中，counter 为 20，以此此类推。

程序 5-10 中的伪代码提供了另一个演示。该程序显示从 1 到 11 的所有数字。

![](img/c939132f78787c7f339c6977b3fc8c85_223_0.png)

```
// 声明计数器变量
Declare Integer counter

// 用于最大值的常量
Constant Integer MAX_VALUE = 11

// 显示 1 到 11 的奇数
For counter = 1 To MAX_VALUE Step 2
    Display counter
End For
```

# 程序输出

- 1
- 3
- 5
- 7
- 9
- 11

# 焦点：使用 For 语句设计计数控制循环

你的朋友 Amanda 刚从她叔叔那里继承了一辆欧洲运动跑车，Amanda 住在美国，她担心自己会收到超速罚单，因为汽车的速度表是以每小时公里为单位的。她请你写一个程序，显示每小时公里速度表，并附带相应的每英里速度值。从每小时公里转换为每英里速度的公式是：

> MPH = KPH × 0.6214

在公式中，MPH 是每英里的速度，KPH 是每小时公的速度。

你的程序显示的表格显示了从 60 公里/小时到 130 公里/小时的速度，每隔 10 增加一次，以及它们转换后的每英里速度。表格应该像这样：

| KPH | MPH |
| 60 | 37.284 |
| 70 | 43.498 |
| 80 | 49.712 |
| etc.... | | |
| 130 | 80.782 |

在考虑这个数值表格后，你决定写一个 For 循环，使用计数器变量来存储每小时公里的速度。计数器的起始值为 60，结束值为 130，并使用步长 10。在循环内部，你将使用计数器变量计算每英里的速度。程序 5-11 显示了伪代码，图 5-16 显示了流程图。

# 程序 5-11

```
// 存储 MPH 和 KPH 速度的变量
Declare Real mph
Declare Integer kph

// 显示表头。
Display "KPH", Tab, "MPH"

// 显示速度。
For kph = 60 To 130 Step 10
  // 计算每英里。
  Set mph = kph * 0.6214
  // 显示 KPH 和 MPH。
  Display kph, Tab, mph
End For
```

# 程序输出

| KPH | MPH |
| --- | --- |
| 60 | 37.284 |
| 70 | 43.498 |
| 80 | 49.712 |
| 90 | 55.926 |
| 100 | 62.14 |
| 110 | 68.354 |
| 120 | 74.568 |
| 130 | 80.782 |

注意变量 kph 被用作计数器。之前我们一直使用 counter。在这个程序中，kph 是计数器的更好的名称，因为它存储的是每小时公里的速度。

## 5.3 计数控制循环与 For 语句

程序 5-11 的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_225_0.png)

# 通过递减计数器变量计数

虽然计数器变量在计数控制循环中通常是递增的，你也可以递减它。递减变量意味着减少它的值。在 for 语句中，你指定一个负步长值来递减计数器。例如，看以下：

```
For counter = 10 To 1
  Display counter
End For
```

在这个循环中，计数器变量的起始值为 10，结束值为 1。步值为 -1，这意味着每次迭代结束后 counter 减 1。第一次迭代中，counter 为 10；第二次迭代中，counter 为 9；以此此类推。如果这是一个实际程序，它将显示 10、9、8 等直到 1。

# 让用户控制迭代次数

在很多情况下，程序员知道循环必须执行的精确迭代次数。例如，回想程序 5-9，它显示从 1 到 10 的数字及其平方。在编写伪代码时，程序员知道要迭代 10 次。常量 MAX_VALUE 初始化为值 10，循环如下：

```
For counter = 1 To MAX_VALUE
```

结果循环迭代了 10 次。然而，程序员可以让用户决定循环应该迭代的次数。例如，如果你想让程序 5-9 更灵活，允许用户指定循环显示的最大值怎么办？程序 5-12 的伪代码显示了如何实现这一点。

| Program 5-12 |
| --- |
| // Variables |
| Declare Integer counter, square, upperLimit |
| // 获取上限。 |
| Display "This program displays numbers, starting at 1," |
| Display "and their squares. How high should I go?" |
| Input upperLimit |
| // 显示表头。 |
| Display "Number", Tab, "Square" |
| Display "----------------------" |
| // 显示数字及其平方。 |
| For counter = 1 To upperLimit |
| // 计算数字平方。 |
| Set square = counter^2 |
| // 显示数字和数字平方。 |
| Display counter, Tab, square |
| End For |

# 程序输出

This program displays numbers, starting at 1, and their squares. How high should I go?
[Enter]

| Number | Square |
| --- | --- |
| 1 | 1 |
| 2 | 4 |
| 3 | 9 |
| 4 | 16 |
| 5 | 25 |

第 5 行和第 6 行询问用户表格中的数字到多少，第 7 行的状态将用户的输入存入 upperLimit 变量。然后，For 循环使用 upperLimit 变量作为计数器的结束值：

```
For counter = 1 To upperLimit
```

结果是计数器的值从 1 开始，以 upperLimit 的值结束。除了指定计数器的结束值外，你还可以指定它的起始值。程序 5-13 的伪代码是一个示例。在这个程序中，用户指定了计数器的起始值和结束值。注意第 20 行，For 循环使用变量来指定计数器变量在起始和结束值期间显示的数字。

# 程序 5-13

```
// Variables
Declare Integer counter, square,
    lowerLimit, upperLimit

// 获取下限。
Display "This program displays numbers, starting at 1,"
Display "and their squares. What number should I start with?"
Input lowerLimit

// 获取上限。
Display "What number should I end with?"
Input upperLimit

// 显示表头。
Display "Number", Tab, "Square"

// 显示数字及其平方。
For counter = lowerLimit To upperLimit
  // 计算数字平方。
  Set square = counter^2
  // 显示数字和数字平方。
  Display counter, Tab, square
End For
```

