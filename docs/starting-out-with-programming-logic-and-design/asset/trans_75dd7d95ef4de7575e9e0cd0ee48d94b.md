

## 11.1 菜单驱动程序简介 437

## 图 11-3 程序 11-2 的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_461_0.png)

## 第 11 章 菜单驱动程序

> 注意：作为第三种备选方案，程序也可以被修改为使用 If-Else If 语句。

## 验证菜单选择

任何允许用户从菜单中选择项目的程序都应该验证用户的选择。程序 11-1 通过 `case` 结构中的 `Default` 部分（第 45 到 47 行）验证了用户的菜单选择。程序 11-2 则通过 `Else` 子句（第 43 到 45 行）验证了菜单选择。

另一种方法是在读取用户选择的 `Input` 语句之后立即使用一个输入验证循环。如果菜单选择无效，循环将显示一条错误消息并提示用户重新输入。只要输入无效，循环就会一直重复。

程序 11-3 中的伪代码展示了如何修改程序 11-1 以使用输入验证循环。输入验证循环出现在第 25 到 25 行。注意 `case` 结构没有 `Default` 部分。输入验证循环确保在程序进入 `case` 结构之前，`menuSelection` 变量被设置为 1 到 3 之间的值。图 11-4 显示了程序的流程图。

## 程序 11-3

```
1 // 定义一个变量来存储
2 // 用户的菜单选择。
3 Declare Integer menuSelection
4
5 // 定义变量来存储度量的
6 // 单位。
7 // 声明英寸、厘米、英尺、米、
8 英里、公里
9
10 // 显示菜单。
11 Display "1. 将英寸转换为厘米。"
12 Display "2. 将英尺转换为米。"
13 Display "3. 将英里转换为公里。"
14 Display
15
16 // 提示用户进行选择
17 Display "Enter your selection."
18 Input menuSelection
20 // 验证菜单选择。
21 While menuSelection < 1 OR menuSelection > 3
22 Display "That is an invalid selection. ",
23     "Enter 1, 2, or 3."
24 Input menuSelection
25 End While
26
27 // 执行选择的操作。
28 Select menuSelection
29 Case: 1:
30 // 将英寸转换为厘米。
31 Display "Enter the number of inches."
32 Input inches
33 Set centimeters = inches * 2.54
34 Display "That is equal to ", centimeters,"
35     centimeters."
36
37 Case: 2:
38 // 将英尺转换为米。
39 Display "Enter the number of feet."
40 Input feet
41 Set meters = feet * 0.3048
42 Display "That is equal to ", meters, " meters."
43
44 Case: 3:
45 // 将英里转换为公里。
46 Display "Enter the number of miles."
47 Input miles
48 Set kilometers = miles * 1.609
49 Display "That is equal to ", kilometers,
50     "kilometers."
51 End Select
```

**程序输出（输入部分加粗显示）**

- 1. 将英寸转换为厘米。
- 2. 将英尺转换为米。
- 3. 将英里转换为公里。

Enter your selection.
**[Enter]**
That is an invalid selection. Enter 1, 2, or 3.
**[Enter]**
Enter the number of inches.
**[Enter]**
That is equal to 25.4 centimeters.

![](img/c939132f78787c7f339c6977b3fc8c85_464_0.png)

## 图 11-4 程序 11-3 的流程图（续）

![](img/c939132f78787c7f339c6977b3fc8c85_465_0.png)

## 检查点

- 11.1 什么是菜单驱动程序？
- 11.2 菜单中显示的元素前面通常有一个数字、字母或其他字符。这个字符的目的是什么？
- 11.3 在程序中用哪种结构来执行用户从菜单中选择的操作？

## 菜单驱动程序的模块化

概念：菜单驱动程序应该是模块化的，每个任务都写在它自己的模块中。菜单驱动程序通常能够执行多项任务，并允许用户选择他想要执行的任务。在大多数情况下，菜单驱动程序应该被分解为执行单个任务的模块。例如，查看程序 11-4 中的伪代码。这是程序 11-3 的改进版本，使用模块将程序拆分为小的、易于管理的片段。

以下是程序 11-4 中使用的模块摘要：

- `main` 模块是程序的起点。它调用其他模块。
- `displayMenu` 在屏幕上显示菜单，获取用户的选择并对其进行验证。
- `inchesToCentimeters` 模块提示用户输入英寸并将其转换为厘米。当用户选择 1 时，由主模块调用该模块。
- `feetToMeters` 模块提示用户输入英尺并将其转换为米。当用户选择 2 时，由主模块调用该模块。
- `milesToKilometers` 模块提示用户输入英里并将其转换为公里。当用户选择 3 时，由主模块调用该模块。

图 11-5 显示了主模块的流程图。将此与程序 11.3 比较，你可以看到模块是如何简化设计的。图 11-6 显示了其他模块的流程图。

## 程序 11-4

```
1 // 定义一个变量来存储
2 // 用户的菜单选择。
3 Declare Integer menuSelection
4
5 // 定义变量来存储度量的
6 // 单位。
7 // 声明英寸、厘米、英尺、米、
8 英里、公里
9
10 // 显示菜单。
11 Display "1. 将英寸转换为厘米。"
12 Display "2. 将英尺转换为米。"
13 Display "3. 将英里转换为公里。"
14 Display
15
16 // 提示用户进行选择
17 ...
```

## 11.2 菜单驱动程序的模块化 443

```basic
1 // main 模块是程序的起点。
2 // 它调用其他模块。
3 Module main()
4 // 定义一个变量来存储
5 // 用户的菜单选择。
6 Declare Integer menuSelection
7
8 // 调用显示模块
9 Call displayMenu(menuSelection)
10 // 执行选择的操作。
11 Select menuSelection
12 Case: 1:
13     Call inchesToCentimeters()
14 Case: 2:
15     Call feetToMeters()
16 Case: 3:
17     Call milesToKilometers()
18 End Select
19 End Module

20 // displayMenu 模块在屏幕上显示菜单，
21 // 获取用户的选择并对其进行验证。
22 Module displayMenu(ref selection)
23 // 显示菜单。
24 Display "1. 将英寸转换为厘米。"
25 Display "2. 将英尺转换为米。"
26 Display "3. 将英里转换为公里。"
27
28 // 提示用户进行选择。
29 Display "Enter your selection."
30 Input selection
31 // 验证菜单选择。
32 While selection < 1 OR selection > 3
33     Display "That is an invalid selection. ",
34         "Enter 1, 2, or 3."
35     Input selection
36 End While
37 End Module

38 // inchesToCentimeters 模块提示用户输入英寸
39 并将其转换为厘米。
40 Module inchesToCentimeters()
41 // 定义变量
42 Declare Real inches, centimeters
43 // 获取英寸数量。
44 Display "Enter the number of inches."
45 Input inches
46 // 将英寸转换为厘米。
47 Set centimeters = inches * 2.54
48 // 显示结果。
49 Display "That is equal to ", centimeters,"
50     "centimeters."
51 End Module

52 // feetToMeters 模块提示用户输入英尺
53 并将其转换为米。
54 Module feetToMeters()
55 // 定义变量
56 Declare Real feet, meters
57 // 获取英尺数量。
58 Display "Enter the number of feet."
59 Input feet
60 // 将英尺转换为米。
61 Set meters = feet * 0.3048
62 // 显示结果。
63 Display "That is equal to ", meters, " meters."
64 End Module

65 // milesToKilometers 模块提示用户输入英里
66 并将其转换为公里。
67 Module milesToKilometers()
68 // 定义变量
69 Declare Real miles, kilometers
70 // 获取英里数量。
71 Display "Enter the number of miles."
72 Input miles
73 // 将英里转换为公里。
74 Set kilometers = miles * 1.609
75 // 显示结果。
76 Display "That is equal to ", kilometers,
77     "kilometers."
78 End Module
```

## 11.2 菜单驱动程序的模块化 444

（输出与程序 11-3 相同。）

## 11.2 菜单驱动程序的模块化 445

