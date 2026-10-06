

## 5.4 计算累加和 211

```text
// 解释我们正在做什么。
// 显示“此程序计算”
// 显示“五个数字的总和。”

// 获取五个数字并进行累加。
For counter = 1 To 5
    Display "Enter a number."
    Input number
    Set total = total + number
End For

// 显示数字的总和。
Display "The total is ", total
```

程序输出（输入部分用**粗体**显示）

此程序计算
五个数字的总和。
输入一个数字。
2 [回车]
输入一个数字。
4 [回车]
输入一个数字。
6 [回车]
输入一个数字。
8 [回车]
输入一个数字。
10 [回车]
总和是 30

首先，让我们看看变量声明。第 3 行声明的 `number` 变量用于存储用户输入的数字。第 7 行声明的 `total` 变量是累加器。注意它被初始化为值 0。第 10 行声明的 `counter` 变量将用作循环计数器。

第 17 行到 21 行的 `For` 循环负责从用户那里收集数字并计算总和。第 18 行提示用户输入数字，第 19 行更新并将其存储在 `number` 变量中。然后，第 20 行的后续语句将 `number` 加到 `total`：

```text
Set total = total + number
```

执行此语句后，`number` 变量中的值将加到 `total` 变量的值上。循环结束后，`total` 变量将保存所有加过的数字之和。该值在第 24 行显示。见图 5-18。

### 图 5-19 程序 5-18 的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_236_0.png)

## 检查点

5.19 计算一系列数字总和的程序通常包含两个元素？

5.20 什么是累加器？

5.21 累加器是否应该初始化为任何特定值？为什么或为什么不？

5.22 观察以下伪代码。如果这是一个真实程序，它会显示什么？

```text
Declare Integer number1 = 10, number2 = 5
Set number1 = number1 + number2
Display number1
Display number2
```

5.23 观察以下伪代码。如果这是一个真实程序，它会显示什么？

```text
Declare Integer counter, total = 0
For counter = 1 To 5
Set total = total + counter
End For
Display total
```

## 哨兵值 (Sentinels)

> 概念：哨兵值是一个标记值列表结束的特殊值。

考虑以下场景：你正在设计一个程序，使用循环来处理值列表。在设计程序时，你并不知道列表中会有多少值。事实上，列表中的值数量在每次程序执行时都可能不同。设计这种循环的最佳方法是什么？以下是你在在本章中已经过的一些技术，以及在处理值列表时使用它们的缺点：

- 在每次循环迭代结束时询问用户是否有另一个值需要处理。如果值列表很长，在每次迭代结束时问这个问题可能会让程序对用户变得繁琐。
- 在程序开始时询问用户列表包含多少项。然而，这可能也会给用户带来不便。如果列表非常长且用户不知道列表中项的数量，则需要用户自己去数。

在每次循环迭代结束时询问用户是否有另一个值需要处理。如果值列表很长，在每次迭代结束时问这个问题可能会让程序对用户变得繁琐。
在程序开始时询问用户列表包含多少项。然而，这可能也会给用户带来不便。如果列表非常长且用户不知道列表中项的数量，则需要用户自己去数。

哨兵值是一个标记值列表结束的特殊值。

哨兵值是一个标记值列表结束的特殊值。

在处理值列表时，哨兵值是一个标记值列表结束的特殊值。

，哨兵值是一个标记值列表结束的特殊值。

哨兵值是一个标记值列表结束的特殊值。

在处理值列表时，哨兵值是一个标记标记列表列表结束。

哨兵值是一个标记值列表结束的特殊值。

## 聚光灯下：使用哨兵值

税务局使用以下公式计算年度税收：

> 税收 = 属性 × 0.065

在与税务局工作人员的交流中，你了解到每个属性都分配了一个数字。你决定使用使用 0 作为哨兵值的循环。图 5-19 显示伪代码，5-20 显示流程图。

```text
Declare main()
// 获取第一个数字
Declare Integer lotNumber
// 税收局部变量
Declare Real total
// 只要 lotNumber 不为 0 就继续
While lotNumber != 0
    // 获取数字
    Display("Enter property number")
    Input lotNumber
    // 计算税收
    Set total = total + lotNumber * 0.065
    // 显示总和
    Display("The total is ", total)
End While
```

214 第5章重复结构

## 5.5 哨兵值

```text
Declare Integer seconds
For seconds = 0 To 59
  Display seconds
End For
```

```text
Declare Integer minutes, seconds
For minutes = 0 To 59
  For seconds = 0 To 59
    Display minutes, ":", seconds
  End For
End For
```

```text
Declare Integer hours, minutes, seconds
For hours = 0 To 23
  For minutes = 0 To 59
    For seconds = 0 To 59
      Display hours, ":", minutes, ":", seconds
    End For
  End For
End For
```

如果这是一个真实程序，它的输出将是：

```
0:0:0
0:0:1
0:0:2
```

（程序将计算24小时内的每一秒。）
23:59:59

内层循环对于每次外层循环都会执行 60 次。中间循环对于每次外层循环都会执行 60 次。当外层循环执行 24 次时，中间循环执行了 1440 次，而内层循环执行了 86400 次！图 5-21 显示了之前所示完整时钟模拟程序的流程图。

### 图 5-20 程序 5-19 的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_240_0.png)

5.24 什么是哨兵值？

5.25 为什么选择哨兵值时应该选择一个唯一的值？

