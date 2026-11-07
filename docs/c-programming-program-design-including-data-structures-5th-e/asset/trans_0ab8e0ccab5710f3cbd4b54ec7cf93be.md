
```cpp
cout << "Surface area: "
     << 2 * radius * 2 + 2 * PI * pow(radius, 2.0) << endl;
cout << fixed << showpoint << setprecision(2);

cout << "Enter the radius of the base of the cylinder: ";
cin >> height;
cout << endl;

#include <iostream>
const double PI = 3.14159;

using namespace std;
```

- 3. 编写一个程序，提示用户输入一个人的体重（千克），并输出等价的体重（磅）。输出这两个体重值，均四舍五入到两位小数。（注意 1 千克 = 2.2 磅。）将输出格式化为两位小数。

- 4. 每年夏天，John 和 Jessica 都会在后院种植蔬菜，并从当地苗圃购买种子和肥料。该苗圃出售不同袋装规格的各种蔬菜肥料。购买某种肥料时，他们想知道每磅肥料的价格以及每平方英尺的施肥成本。下面的程序提示用户输入肥料袋的规格（磅）、该袋肥料的成本，以及该袋肥料可覆盖的面积（平方英尺）。该程序应输出所需结果。然而，程序中存在逻辑错误。找出并改正逻辑错误，使程序正常工作。

```cpp
//Logic errors.

#include <iostream>
#include <iomanip>

using namespace std;

int main()
{
    double cost;
    double area;

    double bagSize;

    cout << fixed << showpoint << setprecision(2);

    cout << "Enter the amount of fertilizer, in pounds, "
         << "in one bag: ";
    cin >> bagSize;
    cout << endl;

    cout << "Enter the cost of the " << bagSize
         << " pound fertilizer bag: ";
    cin >> cost;
    cout << endl;

    cout << "Enter the area, in square feet, that can be "
         << "fertilized by one bag: ";
    cin >> area;
    cout << endl;

    cout << "The cost of the fertilizer per pound is: $"
         << bagSize / cost << endl;
    cout << "The cost of fertilizer per square foot is: $"
         << area / cost << endl;

    return 0;
}
```

- 5. 某足球场经理希望你编写一个程序，计算每场比赛后的门票销售总额。门票有四种类型——包厢票、边线票、贵宾票和普通入场票。每场比赛后，数据以如下形式存储在文件中：

```
ticketPrice    numberOfTicketsSold
...
```

示例数据如下：

| 票价 | 售出票数 |
|---|---|
| 250 | 5750 |
| 100 | 28000 |
| 50 | 35750 |
| 25 | 18750 |

第一行表示票价为 $250，并且以该价格售出了 5750 张票。输出售出的票数和总销售额。将输出格式化为两位小数。

- 6. 编写一个程序，计算并打印某员工的月薪。净工资是在扣除以下项目后计算得出的：

  - 联邦所得税：15%
  - 州税：3.5%
  - 社会保障税：5.75%
  - 医疗保险/医疗补助税：2.75%
  - 养老金计划：5%
  - 健康保险：$75.00

  你的程序应提示用户输入总金额和员工姓名。输出将存储在文件中。将输出格式化为两位小数。示例输出如下：

```
Bill Robinson
Gross Amount: ............ $3575.00
Federal Tax: ............. $ 536.25
State Tax: ............... $ 125.13
Social Security Tax: ..... $ 205.56
Medicare/Medicaid Tax: .... $ 98.31
Pension Plan: ........... $ 178.75
Health Insurance: ........ $ 75.00
Net Pay: ................ $2356.00
```

注意第一列左对齐，右列右对齐。

- 7. 重做第2章的编程练习21，使每个字符串都能存储一行文本。

- 8. 某公司有三名员工即将获得一次特殊加薪。给定一个文件，例如 `Ch3_Ex8Data.txt`，其中包含以下数据：

| 姓 | 名 | 当前工资 | 工资增长百分比 |
|---|---|---|---|
| Miller | Andrew | 65789.87 | 5 |
| Green | Sheila | 75892.56 | 6 |
| Sethi | Amit | 74900.50 | 6.1 |

每个输入行由员工的姓、名、当前工资和工资增长百分比组成。例如，在第一个输入行中，员工的姓是 Miller，名是 Andrew，当前工资是 65789.87，工资增长为 5%。编写一个程序，从指定文件读取数据，并将输出存储到文件 `Ch3_Ex8Output.dat` 中。对于每位员工，数据必须按以下形式输出：`firstName lastName updatedSalary`。将十进制数的输出格式化为两位小数。

- 9. 编写一个程序，接受质量（克）和密度（克/立方厘米）作为输入，并使用公式 $density = mass / volume$ 输出物体的体积。将输出格式化为两位小数。

- 10. 信用卡未偿还余额的利息使用平均每日余额计算。假设 `netBalance` 是账单中显示的余额，`payment` 是已支付的款项，`d1` 是账单周期中的天数，`d2` 是在账单周期前付款的天数。那么，平均每日余额为：

  $$averageDailyBalance = (netBalance * d1 − payment * d2)/d1$$

  如果月利率为，比如说，0.0152，那么未偿还余额的利息为：

  $$interest = averageDailyBalance * 0.0152$$

  编写一个程序，接受 `netBalance`、`payment`、`d1`、`d2` 和月利率作为输入。程序输出利息。将输出格式化为两位小数。

![](img/f97f778697507bb6fdd80c5991210cba_216_0.png)

## 第4章

## 控制结构 I（选择）

在本章中，你将：

- 学习控制结构
- 考查关系运算符和逻辑运算符
- 探索如何形成和求值逻辑（布尔）表达式
- 发现如何在程序中使用选择控制结构 if、if...else 和 switch
- 学习如何通过避免一知半解的概念来避免错误
- 学习使用 assert 函数终止程序

第2章将程序定义为一系列语句，其目标是完成某项任务。到目前为止，你检查过的程序都很简单直接。为了处理一个程序，计算机从第一条可执行语句开始，按顺序执行语句，直到到达末尾。在本章和第5章中，你将学习如何告诉计算机它不必遵循简单的顺序语句顺序；它还可以做出决策，并重复执行某些语句，直到满足某些条件。

### 控制结构

计算机可以通过以下方式之一处理程序：顺序执行；选择性地执行，即做出选择，也称为分支；重复执行，即使用称为循环的结构反复执行一条语句；或者调用函数。图4-1说明了前三种程序流程。（在第7章中，我们将展示函数调用如何工作。）第2章和第3章中的编程示例包括简单的顺序程序。对于这样的程序，计算机从开头开始，并按顺序执行语句。没有做出选择；没有重复。控制结构提供了顺序程序执行的替代方式，用于改变执行的顺序流程。两种最常见的控制结构是选择和重复。在*选择*中，程序根据某些条件执行特定语句。在*重复*中，程序根据某些条件将特定语句重复一定次数。

![](img/f97f778697507bb6fdd80c5991210cba_217_0.png)

**图4-1** 执行流程

在学习选择和重复之前，你必须理解条件语句的性质以及如何使用它们。考虑以下三条语句：

- 1. `if (score is greater than or equal to 90)`  
  `grade is A`

- 2. `if (hours worked are less than or equal to 40)`  
  `wages = rate * hours`  
  `otherwise`  
  `wages = (rate * 40) + 1.5 * (rate * (hours − 40))`

- 3. `if (temperature is greater than 70 degrees and it is not raining)`  
  `Go golfing!`

这些语句是条件语句的示例。你可以看到，某些语句只有在满足某些条件时才会执行。如果条件求值为**真**，则满足条件。例如，在语句1中：

`score is greater than or equal to 90`

如果 score 的值大于或等于 90，则为**真**；否则为**假**。例如，如果 score 的值为 95，则该语句求值为**真**。类似地，如果 score 的值为 86，则该语句求值为**假**。

如果计算机能够识别这些类型的语句对于适当的值是否为真，那将很有用。此外，在某些情况下，语句的真假可能取决于多个条件。例如，在语句3中，“温度大于70度”和“没有下雨”都必须为真，才建议去打高尔夫球。

如你所见，为了让计算机做出决策并重复语句，它必须能够对程序执行时存在的条件做出反应。接下来几节讨论如何在 C++ 中表示和求值条件语句。

### 关系运算符

为了做出决策，你必须能够表达条件并进行比较。例如，支票账户的利率和服务费可能取决于月末余额。如果余额低于某个最低余额，不仅利率较低，而且通常还会收取服务费。因此，为了确定利率，你必须能够说明最低余额，并将账户余额与最低余额进行比较（一个条件）。保险单的保费也通过说明条件和进行比较来确定。例如，为了确定保险费，你必须能够检查投保人的吸烟状况。不吸烟者（条件）获得的保费低于吸烟者。这两个例子都涉及比较项目。某些项目被比较

![](img/f97f778697507bb6fdd80c5991210cba_218_0.png)
