

![](img/d61019b035dd82beb581604273c0ee6b_166_0.png)

## 工作示例 3.1

### 提取中间字符

### 问题陈述

你的任务是从给定字符串 str 中提取包含中间字符的字符串。例如，如果字符串是 "crate"，结果是字符串 "a"。但是，如果字符串有偶数个字母，则提取中间两个字符。如果字符串是 "crates"，结果是 "at"。

### 第 1 步 决定分支条件。

我们需要对奇数长度和偶数长度的字符串采取不同的操作。因此，条件是 *字符串的长度是否为奇数？* 在 C++ 中，使用除以 2 的余数来判断一个值是偶数还是奇数。于是测试变为

```
if (str.length() % 2 == 1)
```

### 第 2 步 给出当条件为真时需要完成的工作的伪代码。

我们需要找到中间字符的位置。如果长度为 5，则位置是 2。

| c | r | a | t | e |
| 0 | 1 | 2 | 3 | 4 |

一般情况下，

```
position = str.length() / 2  (with the remainder discarded)
result = str.substr(position, 1)
```

### 第 3 步 给出当条件不为真时需要完成的工作（如果有）的伪代码。

同样，我们需要找到中间字符的位置。如果长度为 6，起始位置是 2，结束位置是 3，子字符串长度为 2。

| c | r | a | t | e | s |
| 0 | 1 | 2 | 3 | 4 | 5 |

一般情况下，

```
position = str.length() / 2 - 1
result = str.substr(position, 2)
```

### 第 4 步 仔细检查关系运算符。

我们真的需要 str.length() % 2 == 1 吗？例如，当长度为 5 时，5 % 2 是 5 / 2 的余数，即 1。一般来说，奇数除以 2 余 1。（实际上，负奇数除以 2 余 -1，但字符串长度永远不会为负。）因此，我们的条件是正确的。

### 第 5 步 去除重复。

这是我们开发出的语句：

```
If the length of str is odd
  position = str.length() / 2  (with remainder discarded)
  result = str.substr(position, 1)
Else
  position = str.length() / 2 - 1
  result = str.substr(position, 2)
```

每个分支中的第二条语句几乎相同，只是子字符串的长度不同。让我们在每个分支中设置长度：

```
If the length of str is odd
    position = str.length() / 2 (with remainder discarded)
    length = 1
Else
    position = str.length() / 2 - 1
    length = 2
result = str.substr(position, length)
```

### 第 6 步

测试两个分支。

我们将使用一组不同的字符串进行测试。对于奇数长度的字符串，考虑 "monitor"。我们得到

```
position = str.length() / 2 = 7 / 2 = 3 (with remainder discarded)
length = 1
result = str.substr(3, 1) = "i"
```

对于偶数长度的字符串 "monitors"，我们得到

```
position = str.length() / 2 - 1 = 8 / 2 - 1 = 3 (with remainder discarded)
length = 2
result = str.substr(3, 2) = "it"
```

### 第 7 步

在 C++ 中组装 if 语句。

这是完整的代码段（完整程序参见 worked_example_1/middle.cpp）：

```
if (str.length() % 2 == 1)
{
    position = str.length() / 2;
    length = 1;
}
else
{
    position = str.length() / 2 - 1;
    length = 2;
}
result = str.substr(position, length);
```

## 第 4 章

### 循环

![](img/d61019b035dd82beb581604273c0ee6b_168_0.png)

© photo75/Stockphoto.

### 本章目标

- 实现 while、for 和 do 循环
- 避免无限循环和差一错误
- 理解嵌套循环
- 实现读取和处理数据集的程序
- 使用计算机进行模拟

### 本章内容

4.1 while 循环 96  
SYN while 语句 97  
CE1 无限循环 100  
CE2 不要想“我们到了吗？” 101  
CE3 差一错误 101  
C&S 第一个 Bug 102  

4.2 问题求解：手工跟踪 103  

4.3 for 循环 106  
SYN for 语句 106  
PT1 仅将 for 循环用于其预期目的 109  
PT2 选择与任务匹配的循环边界 110  
PT3 计算迭代次数 110  

4.4 do 循环 111  
PT4 循环流程图 111  

4.5 处理输入 112  
ST1 清除失败状态 115  
ST2 循环半途问题和 break 语句 116  
ST3 输入和输出的重定向 116  

4.6 问题求解：故事板 117  

4.7 常见循环算法 119  
HT1 编写循环 123  
WE1 信用卡处理 126  

4.8 嵌套循环 126  
WE2 操作图像中的像素 129  

4.9 问题求解：先解决更简单的问题 130  

4.10 随机数与模拟 134  
C&S 数字盗版 138  

在循环中，程序的一部分会被一遍又一遍地重复执行，直到达到特定目标。循环对于需要重复步骤的计算以及处理包含许多数据项输入的程序非常重要。在本章中，你将学习 C++ 中的循环语句，以及编写处理输入和模拟现实世界活动的程序的技术。

![](img/d61019b035dd82beb581604273c0ee6b_169_0.png)

## 4.1 while 循环

在本节中，你将学习如何重复执行语句直到达到目标。

回想第 1 章中的投资问题。你将 10,000 美元存入一个年利率为 5% 的银行账户。账户余额需要多少年才能翻倍？

在第 1 章中，我们为这个问题开发了以下算法：

从年份值 0、利率列和余额 $10,000 开始。

| 年 | 利息 | 余额 |
|------|----------|---------|
| 0    |          | $10,000 |

- 当余额小于 $20,000 时，重复以下步骤
- 将年份值加 1。
- 计算利息为 balance x 0.05（即 5% 的利息）。
- 将利息加到余额上。
- 将最终年份值作为答案报告。

现在你已经知道如何在 C++ 中定义和更新变量。你还不知道的是如何执行“当余额小于 $20,000 时重复步骤”。

![](img/d61019b035dd82beb581604273c0ee6b_169_1.png)

因为所赚取的利息也会产生利息，所以银行余额呈指数增长。

![](img/d61019b035dd82beb581604273c0ee6b_169_2.png)

在粒子加速器中，亚原子粒子多次穿过环形隧道，获得物理实验所需的速度。类似地，在计算机科学中，循环中的语句在条件为真时执行。

### 语法 4.1 while 语句

![](img/d61019b035dd82beb581604273c0ee6b_170_0.png)

> 只要条件保持为真，循环就会重复执行代码块。

在 C++ 中，while 语句实现了这种重复（参见语法 4.1）。代码

```
while (condition)
{
    statements
}
```

在条件为真时持续执行这些语句。在我们的例子中，我们希望当余额小于 $20,000 的目标余额时递增年份计数器并添加利息：

```
while (balance < TARGET)
{
    year++;
    double interest = balance * RATE / 100;
    balance = balance + interest;
}
```

while 语句是循环的一个示例。如果绘制流程图，执行流会再次循环到条件测试的位置（见图 1）。

![](img/d61019b035dd82beb581604273c0ee6b_170_1.png)

### 图 1 while 循环流程图

当你在循环体内定义变量时，该变量会在循环的每次迭代中创建，并在每次迭代结束后移除。例如，考虑这个循环中的 interest 变量：

```
while (balance < TARGET)
{
    year++;
    double interest = balance * RATE / 100;
    balance = balance + interest;
} // interest no longer defined here
```

> 每次迭代都会创建一个新的 interest 变量。

相反，balance 和 year 变量是在循环体外定义的。这样，循环的所有迭代都使用相同的变量。

下面是解决投资问题的程序。图 2 展示了程序的执行过程。

### sec01/doublinv.cpp

```
#include <iostream>
using namespace std;

int main()
{
    const double RATE = 5;
    const double INITIAL_BALANCE = 1000;
    const double TARGET = 2 * INITIAL_BALANCE;

    double balance = INITIAL_BALANCE;
    int year = 0;

    while (balance < TARGET)
    {
        year++;
        double interest = balance * RATE / 100;
        balance = balance + interest;
    }

    cout << "The investment doubled after "
         << year << " years." << endl;

    return 0;
}
```

### 程序运行

```
The investment doubled after 15 years.
```

![](img/d61019b035dd82beb581604273c0ee6b_171_0.png)

图 2 doublinv 循环的执行过程

