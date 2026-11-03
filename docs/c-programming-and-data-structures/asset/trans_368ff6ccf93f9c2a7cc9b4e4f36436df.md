
## 示例 1.1 编写算法以判断给定数字是否为质数

解答

```
Algorithm
Step 1 - Start
Step 2 - Accept a number from the user (num)
Step 3 - Initialize looping counter i = 2
Step 4 - Repeat Step 5 while i < num
Step 5 - If remainder of num divided by i (num%i) is Zero then goto Step 6 else goto Step 4
Step 6 - Display "num is not a prime number" and break from the loop
Step 7 - If i = num then goto Step 8 Else goto Step 9
Step 8 - Display "num is a prime number"
Step 9 - Stop
```

Fig. 1.27 判断给定数字是否为质数的算法

## 示例 1.2 编写算法求学生三科成绩的平均分

解答

```
Algorithm
Step 1 - Start
Step 2 - Accept the marks in three subjects from the user (marks1, marks2, marks3)
Step 3 - Calculate average marks using formula, average = (marks1 + marks2 + marks3)/3
Step 4 - Display the computed average of three subject marks
Step 5 - Stop
```

Fig. 1.28 求三个科目平均分的算法

## 示例 1.3 编写算法判断给定的年份是否为闰年

解答

```
Algorithm
Step 1 - Start
Step 2 - Accept a year value from the user (year)
Step 3 - If remainder of year value divided by 4 (year%4) is 0 then goto Step 4 else goto Step 5
Step 4 - Display "year is a leap year" and goto Step 6
Step 5 - Display "year is not a leap year"
Step 6 - Stop
```

Fig. 1.29 确定闰年的算法

## 示例 1.4 编写算法判断给定数字是偶数还是奇数

解答

```
Algorithm
Step 1 - Start
Step 2 - Accept a number from the user (num)
Step 3 – If remainder of num divided by 2 (num%2) is Zero then goto Step 4 else goto Step 5
Step 4 – Display "num is an even number" and goto Step 6
Step 5 – Display "num is an odd number"
Step 6 – Stop
```

Fig. 1.30 判断数字是偶数还是奇数的算法

## 示例 1.5 编写算法判断给定的字符串是否为回文

解答

```
Algorithm
Step 1 – Start
Step 2 – Accept a string from the user (str)
Step 3 – Calculate the length of string str (len)
Step 4 – Initialize looping counters left=0, right=len-1 and chk = 't'
Step 5 – Repeat Steps 6-8 while left < right and chk = 't'
Step 6 – If str(left) = str(right) goto Step 8 else goto step 7
Step 7 – Set chk = 'f'
Step 8 – Set left = left + 1 and right = right - 1
Step 9 – If chk='t' goto Step 10 else goto Step 11
Step 10 – Display "The string is a palindrome" and goto Step 12
Step 11 – Display "The string is not a palindrome"
Step 12 – Stop
```

Fig. 1.31 确定回文的算法

## 1.10 流程图

流程图可以定义为过程的图形表示，它描述了过程中控制和信息的顺序和流程。信息流以逐步的形式在流程图内部表示。该技术主要用于开发业务工作流程和使用计算机解决问题。

流程图使用不同的符号来表示在过程的不同阶段执行的不同的活动。流程图中使用了各种符号：

- 开始和结束：它由圆角矩形表示。它表示过程的开始和结束。每个过程在某一点开始和结束，因此流程图始终包含一个开始和一个结束符号。图 1.32 显示了流程图中使用开始和结束符号。

![](img/fe6da5f61b1e2c77309bbee135b45e35_40_0.png)

Fig. 1.32 开始和结束符号。

- 输入或输出：它由平行四边形表示。它表示用户向过程提供的输入和过程向用户提供的输出。图 1.33 显示输入或输出符号。

![](img/fe6da5f61b1e2c77309bbee135b45e35_41_0.png)

- 动作或过程：它由矩形表示。它表示过程中发生的动作、逻辑和计算。图 1.34 显示动作或过程符号。

![](img/fe6da5f61b1e2c77309bbee135b45e35_41_1.png)

- 决策或条件：它由菱形或菱形表示。它表示流程图中的条件或决策步骤。决策的结果是一个布尔值，即真或假。这些值中的每一个都将程序的流程带到某一点，这借助箭头显示。图 1.35 显示决策或条件符号。

![](img/fe6da5f61b1e2c77309bbee135b45e35_41_2.png)

- 箭头：它由有向线表示。它表示流程图中的过程流程和步骤顺序。它指导过程的方向和顺序，在执行过程中的各个步骤时应遵循这些方向和顺序。图 1.36 显示箭头符号。

![](img/fe6da5f61b1e2c77309bbee135b45e35_41_3.png)

- 连接器：它在流程图中由圆圈表示。它表示当流程图继续到下一页时步骤流程的延续。字母（a 到 z）或符号（α、β 或 γ）等字符可以放置在流程中断位置的圆圈中，并且相同的字符也放置在流程图继续位置的圆圈中。图 1.37 显示连接器符号。

![](img/fe6da5f61b1e2c77309bbee135b45e35_42_0.png)

Fig. 1.37 连接器符号。

除上述提到的基本流程图符号外，流程图内部还使用某些其他符号来表示高级操作。表 1.2 显示了其中一些高级流程图符号：

| 符号 | 描述 |
|---|---|
|  | 表示计算机系统的内部存储器，如 RAM 和 ROM |
|  | 表示数据库 |
|  | 表示子程序 |
|  | 表示一组文档 |
|  | 表示空闲或等待状态 |
|  | 将多个数据集合并为一个 |
|  | 从单个数据集中提取单个数据项集合 |
|  | 表示合并和提取操作的组合。它从多个输入数据集中提取多个数据集。 |

为了理解流程图如何表示信息流；请考虑 Fig. 1.38 所示的加两个数字的流程图示例。

## 1.32 计算机编程

## 流程图

![](img/fe6da5f61b1e2c77309bbee135b45e35_43_0.png)

### 1.10.1 流程图设计规则

设计流程图时必须遵循的一些标准准则或规则是

- 它必须以“Start”开始并以“Stop”符号结束。
- 标准流程应自上而下或自左向右。
- 流程图中指定的指令必须简洁明了。
- 箭头必须正确对齐，以便清晰地描绘程序控制的流程。
- 通常应避免使用连接器，因为它们会使程序看起来更复杂。
- 流程图中的过程或动作符号必须只有一个输入箭头和一个输出箭头。
- 两个箭头绝不能相交或交叉；如果有此需要，则必须使用适当的桥接或交叉符号。

### 1.10.2 流程图的优点

使用流程图进行程序设计的一些主要优点是

- 它有助于以简单的方式理解程序控制的流程。
- 通过参考其流程图开发程序代码，比从头开始开发程序代码更容易。
- 它有助于避免语义错误。
- 任何概念在视觉表示的帮助下都能更好地理解。这一事实同样适用于流程图。理解编程逻辑的图形表示更容易。
- 流程图可作为流程或程序流程的文档。
- 流程图的使用适用于小型程序设计。

### 1.10.3 流程图的缺点

流程图也有某些局限性，如下所示：

- 对于大型程序，流程图可能会变得非常复杂且令人困惑。
- 修改流程图很困难，需要几乎完全重新制作。
- 由于流程图需要对编程元素进行图形表示，因此创建流程图会变得有点繁琐和耗时。
- 流程图中过度使用连接器有时会使程序员感到困惑。

## 示例 1.6 绘制示例 1.1 中给出的问题的流程图

解答

![](img/fe6da5f61b1e2c77309bbee135b45e35_44_0.png)

Fig. 1.39 判断给定数字是否为质数的流程图
