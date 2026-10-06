

记录已经按照销售人员 ID 完成了排序。Brewster 要求你设计一个程序来打印销售报告。该报告应显示每位销售人员的销售额以及该销售人员的总销售额。报告还应该显示该月所有销售人员的总销售额。以下是销售报告的显示示例：

# Brewster's Used Cars, Inc.
销售报告

| 销售人员 ID | 销售金额 |
| :--- | :--- |
| 100 | $10,000.00 |
| 100 | $12,000.00 |
| 100 | $5,000.00 |
| **该销售人员总销售额:** | **$27,000.00** |
| | |
| 101 | $14,000.00 |
| 101 | $18,000.00 |
| 101 | $12,500.00 |
| **该销售人员总销售额:** | **$44,500.00** |
| | |
| 102 | $13,500.00 |
| 102 | $14,500.00 |
| 102 | $20,000.00 |
| **该销售人员总销售额:** | **$48,000.00** |
| **所有销售总额:** | **$119,500.00** |

## 第 11 章 菜单驱动程序

- 11.1 菜单驱动程序导论
- 11.2 菜单驱动程序的模块化
- 11.3 使用循环重复菜单
- 11.4 多级菜单

## 11.1 菜单驱动程序导论

**概念：** 菜单是程序显示的操作列表。用户可以选择其中某一项操作，程序将执行该操作。

菜单驱动程序在屏幕上显示其可以执行的操作列表，并允许用户选择其希望程序执行的操作。显示在屏幕上的操作列表被称为*菜单*。例如，一个管理邮件列表的程序可能会显示图 11-1 所示的菜单。

图 11-1 一个菜单

![](img/c939132f78787c7f339c6977b3fc8c85_455_0.png)

注意，此特定菜单中的每个项目前面都有一个数字。用户通过输入旁边的数字来选择其中一项操作。例如，输入 1 可以向邮件列表添加一个名称，输入 4 则让程序打印邮件列表。允许用户在键盘上输入选择的菜单驱动程序通常为每个菜单项显示一个字符（如数字或字母）。用户输入与其想要选择的菜单项对应的字符。

> 注意：在使用图形用户界面 (GUI) 的程序中，用户通常通过鼠标点击来进行选择。你将在第 15 章中学习图形用户界面。

### 使用决策结构执行菜单选择

当用户从菜单中选择一个项目时，程序必须使用决策结构根据该选择执行操作。在大多数语言中，`case` 结构是实现这一点的良好机制。让我们来看一个简单的例子。假设我们需要一个程序将以下测量值从英制转换为公制单位：

- 将英寸转换为厘米
- 将英尺转换为米
- 将英里转换为公里

以下是进行这些转换的公式：

centimeters = inches * 2.54
meters = feet * 0.3048
kilometers = miles * 1.609

程序应该显示一个如下所示菜单，允许用户选择他们想要执行的转换。

1. 将英寸转换为厘米。
2. 将英尺转换为米。
3. 将英里转换为公里。

输入你的选择。

程序 11-1 显示了程序的伪代码以及程序的四次示例执行情况。第 21 到 48 行的 `case` 结构执行用户从菜单中选择的操作。注意，第 45 到 47 行出现了一个 `Default` 情况。如果用户在菜单提示处输入 1、2 或 3 以外的任何值，将会显示错误信息。前两个示例会话显示了用户从菜单中做出有效选择时发生的情况。最后一个示例会话显示了用户做出无效菜单选择时发生的情况。图 11-2 显示了程序的流程图。

## 11.1 菜单驱动程序导论 433

### 程序 11-1

```
1 // 声明一个变量来存储
2 // 用户菜单选择。
3 Declare Integer menuSelection
4
5 // 声明变量来存储测量
6 // 单位。
7 Declare Real inches, centimeters, feet, meters,
8 miles, kilometers
9
10 // 显示菜单。
11 Display "1. Convert inches to centimeters."
12 Display "2. Convert feet to meters."
13 Display "3. Convert miles to kilometers."
14 Display
15
16 // 提示用户进行选择
17 Display "Enter your selection."
18 Input menuSelection
19
20 // 执行选定的操作。
21 Select menuSelection
22 Case 1:
23 // 将英寸转换为厘米。
24 Display "Enter the number of inches."
25 Input inches
26 Set centimeters = inches * 2.54
27 Display "That is equal to ", centimeters.
28
29 Case 2:
30 // 将英尺转换为米。
31 Display "Enter the number of feet."
32 Input feet
33 Set meters = feet * 0.3048
34 Display "That is equal to ", meters.
35
36 Case 3:
37 // 将英里转换为公里。
38 Display "Enter the number of miles."
39 Input miles
40 Set kilometers = miles * 1.609
41 Display "That is equal to ", kilometers.
42
43 Default:
44 // 显示错误信息。
45 Display "That is an invalid selection."
46 Select
```

> 这显示了菜单并提示用户进行选择。用户的输入存储在 `menuSelection` 变量中。

> 如果用户输入 1，则执行。

> 如果用户输入 2，则执行。

> 如果用户输入 3，则执行。

> 如果用户输入 1、2 或 3 以外的任何值，则执行。

### 示例输出（加粗）

1. 将英寸转换为厘米。
2. 将英尺转换为米。
3. 将英里转换为公里。

输入你的选择。
输入英寸数。
等于 254 厘米。

### 示例输出（加粗）

1. 将英寸转换为厘米。
2. 将英尺转换为米。
3. 将英里转换为公里。

输入你的选择。
输入英尺数。
等于 3.48 米。

### 示例输出（加粗）

1. 将英寸转换为厘米。
2. 将英尺转换为米。
3. 将英里转换为公里。

输入你的选择。
输入英里数。
等于 1609 公里。

### 示例输出（加粗）

1. 将英寸转换为厘米。
2. 将英尺转换为米。
3. 将英里转换为公里。

输入你的选择。
这是一个无效的选择。

虽然 `case` 结构通常是菜单驱动程序中最简单且直接的决策结构，但也可以采取其他方法。例如，可以使用嵌套的 `If-Then-Else` 语句，如程序 11-2 所示。图 11-3 显示了该程序的流程图。

图 11-2 程序 11 的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_459_0.png)

### 程序 11-2

```
1 // 声明一个变量来存储
2 // 用户菜单选择。
3 Declare Integer menuSelection
4
5 // 声明变量来存储测量
6 // 单位。
7 Declare Real inches, centimeters, feet, meters,
8 miles, kilometers
9
10 // 显示菜单。
11 Display "1. Convert inches to centimeters."
12 Display "2. Convert feet to meters."
13 Display "3. Convert miles to kilometers."
14 Display
15
16 // 提示用户进行选择
17 Display "Enter your selection."
18 Input menuSelection
19
20 // 执行选定的操作。
21 If menuSelection == 1 Then
22 // 将英寸转换为厘米。
23 Display "Enter the number of inches."
24 Input inches
25 Set centimeters = inches * 2.54
26 Display "That is equal to ", centimeters.
28 Else
29 If menuSelection == 2 Then
30 // 将英尺转换为米。
31 Display "Enter the number of feet."
32 Input feet
33 Set meters = feet * 0.3048
34 Display "That is equal to ", meters.
35 Else
36 If menuSelection == 3 Then
37 // 将英里转换为公里。
38 Display "Enter the number of miles."
39 Input miles
40 Set kilometers = miles * 1.609
41 Display "That is equal to ", kilometers.
43 Else
44
45 // 显示错误信息。
46 Display "That is an invalid selection."
47 End If
48 End If
```

