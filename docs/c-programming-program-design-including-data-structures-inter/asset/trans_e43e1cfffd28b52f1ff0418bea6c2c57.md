
- e. 编写关闭输入文件和输出文件的语句。
- f. 编写一个 C++ 程序，测试 a 到 e 部分中的语句。

- 2. 考虑以下程序，其中语句的顺序不正确。重新排列这些语句，使程序提示用户输入圆柱体的高度和底面半径，并输出圆柱体的体积和表面积。将输出格式化为两位小数。

```cpp
#include <iomanip>
#include <cmath>

int main()
{ }

    double height;

    cout << "Volume of the cylinder = "
         << PI * pow(radius, 2.0) * height << endl;

    cout << "Enter the height of the cylinder: ";
    cin >> radius;
    cout << endl;

    return 0;

    double radius;

    cout << "Surface area: "
         << 2 * PI * radius * height + 2 * PI * pow(radius, 2.0)
         << endl;
    cout << fixed << showpoint << setprecision(2);

    cout << "Enter the radius of the base of the cylinder: ";
    cin >> height;
    cout << endl;

#include <iostream>
const double PI = 3.14159;

using namespace std;
```

- 3. 编写一个程序，提示用户输入一个人的体重（千克），并输出等效的磅数。输出两个体重值，均四舍五入到两位小数。（注意 1 千克 = 2.2 磅。）将输出格式化为两位小数。

- 4. 每年夏天，John 和 Jessica 都会在后院种植蔬菜，并从当地苗圃购买种子和肥料。该苗圃提供不同袋装规格的多种蔬菜肥料。购买某种肥料时，他们想知道该肥料每磅的价格以及每平方英尺的施肥成本。以下程序提示用户输入一袋肥料的重量（磅）、该袋肥料的成本，以及该袋肥料可覆盖的面积（平方英尺）。程序应输出所需结果。但是，该程序包含逻辑错误。找出并纠正逻辑错误，使程序正常工作。

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
    cout << "The cost of fertilizing per square foot is: $"
         << area / cost << endl;

    return 0;
}
```

- 5. 一位足球场经理希望你编写一个程序，计算每场比赛后的门票销售总额。门票有四种类型——包厢票、边线票、贵宾票和普通票。每场比赛后，数据按以下形式存储在文件中：

| 票价 | 售出门票数量 |
|---|---|
| ... | ... |

示例数据如下：

| 票价 | 售出门票数量 |
|---|---:|
| 250 | 5750 |
| 100 | 28000 |
| 50 | 35750 |
| 25 | 18570 |

第一行表示票价为 250 美元，并且以该价格售出了 5750 张门票。输出售出的门票数量和总销售额。将输出格式化为两位小数。

- 6. 重做第 2 章中的编程练习 21，使每个字符串都能存储一行文本。

- 7. 一家公司的三名员工即将获得一次特殊的加薪。给定一个文件，例如 `Ch3_Ex7Data.txt`，其中包含以下数据：

```text
Miller Andrew 65789.87 5
Green Shiloh 75892.56 6
Sethi Amit 74900.50 6.1
```

每个输入行由员工的姓、名、当前工资和工资增长百分比组成。例如，在第一个输入行中，员工的姓是 Miller，名是 Andrew，当前工资是 65789.87，工资增长为 5%。编写一个程序，从指定文件读取数据，并将输出存储到文件 `Ch3_Ex7Output.dat` 中。对于每位员工，数据必须按以下形式输出：

`firstName lastName updatedSalary`。将十进制数的输出格式化为两位小数。

- 8. 编写一个程序，接受质量（克）和密度（克/立方厘米）作为输入，并使用公式 `volume = mass / density` 输出物体的体积。将输出格式化为两位小数。

- 9. 信用卡未付余额的利息使用平均每日余额计算。假设 `netBalance` 是账单中显示的余额，`payment` 是已支付的款项，`d1` 是账单周期内的天数，`d2` 是在账单周期前支付款项的天数。那么，平均每日余额为：

$$averageDailyBalance = \frac{netBalance * d1 - payment * d2}{d1}$$

如果月利率为，例如 0.0152，则未付余额的利息为：

$$interest = averageDailyBalance * 0.0152$$

编写一个程序，接受 *净余额*、还款额、d1、d2 和月利率作为输入。程序输出利息。将输出格式化为两位小数。

- 10. Linda 正在创办一家新的化妆品和服装企业，并希望在支付所有费用（包括商品成本、店铺租金、员工工资和店铺电费）后获得约 10% 的净利润。她想知道商品应加价多少，以便在年底支付所有费用后，她能获得约商品成本 10% 的净利润。注意，在给商品加价后，她希望将该商品按 15% 的折扣销售。编写一个程序，提示 Linda 输入商品总成本、员工工资（包括她自己的工资）、年租金和预计电费。然后程序输出商品应加价多少，以便 Linda 获得期望的利润。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_226_0.png)

## 第 4 章

## 控制结构 I（选择）

### 本章中，你将：

- 学习控制结构
- 考察关系运算符和逻辑运算符
- 探索如何构造和求值逻辑（布尔）表达式
- 了解如何在程序中使用选择控制结构 `if`、`if...else` 和 `switch`
- 学习如何通过避免一知半解的概念来避免错误
- 学习使用 `assert` 函数终止程序

第 2 章将程序定义为一系列语句，其目标是完成某项任务。到目前为止你检查过的程序都很简单直接。为了处理程序，计算机从第一条可执行语句开始，按顺序执行语句，直到结束。在本章和第 5 章中，你将学习如何告诉计算机它不必遵循简单的顺序语句顺序；它还可以做出决策，并反复执行某些语句，直到满足某些条件。

### 控制结构

计算机可以通过以下方式之一处理程序：按顺序；有选择地，通过做出选择，这也称为分支；重复地，通过反复执行语句，使用称为循环的结构；或通过调用函数。图 4-1 说明了前三种程序流程。（在第 6 章中，我们将展示函数调用如何工作。）第 2 章和第 3 章中的编程示例包括简单的顺序程序。对于这样的程序，计算机从开头开始并按顺序执行语句。没有做出选择；没有重复。控制结构提供了顺序程序执行的替代方案，并用于改变顺序执行流程。两种最常见的控制结构是选择和重复。在选择中，程序根据某些条件执行特定语句。在重复中，程序根据某些条件将特定语句重复一定次数。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_227_0.png)

图 4-1 执行流程

