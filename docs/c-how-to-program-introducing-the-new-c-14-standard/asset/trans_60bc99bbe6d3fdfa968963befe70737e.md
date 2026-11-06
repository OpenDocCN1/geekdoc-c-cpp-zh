
## 基于整数的货币计算

贯穿本书，我们专注于*构建有价值的类*。在本节中，我们开始开发一个 `DollarAmount` 类，以精确控制货币金额。该类以整数美分来表示美元金额——例如，$1,000 存储为 100000。这种方法的一个关键优势是整数值在内存中能够*精确*表示。

首先，我们假设类 `DollarAmount` 已经存在，具备以下功能：

-   一个构造函数，用于将 `DollarAmount` 对象初始化为整数美分
-   一个 `add` 成员函数，用于将一个 `DollarAmount` 对象加到调用该函数的 `DollarAmount` 对象上
-   一个 `subtract` 成员函数，用于从调用该函数的 `DollarAmount` 对象中减去一个 `DollarAmount` 对象
-   一个 `addInterest` 成员函数，用于计算调用该函数的 `DollarAmount` 对象中金额的年利息，并将该利息加到该对象的金额中
-   一个 `toString` 成员函数，用于返回 `DollarAmount` 的 `string` 表示。

该类使用整数运算来执行*所有计算*——不使用浮点数运算，因此 `DollarAmount` 对象总是精确表示其值。我们将在**图5.7**中使用这些功能来演示 `DollarAmount` 对象的加法和减法，并使用 `DollarAmount` 对象重新实现**图5.6**中的复利示例。然后我们将展示该类并逐段讲解代码。正如你将看到的，利息计算仍然需要舍入，但 `DollarAmount` 类将使用整数运算精确控制舍入的方式。

这个版本的 `DollarAmount` 类会显得有些笨拙，要求你调用诸如 `add`、`subtract`、`addInterest` 和 `toString` 之类的成员函数。在**第10章**运算符重载中，我们会做得更好。在那里，你将看到如何使用你已经用于基本类型的运算符（如 `+`、`-`、`>>` 和 `<<`）来方便地操作 `DollarAmount` 对象。在后续章节中，你还可以对这个类进行其他改进。构建一个像 `DollarAmount` 这样有价值的类——它能帮助你解决实际世界中的具体问题——是学习C++中的关键“顿悟时刻”之一。我们将在接下来的章节中指出其他类似的时刻。

### 表示货币金额是一个复杂问题

处理货币金额比我们这里展示的要复杂得多。全世界有许多货币，其千位分隔符、小数点分隔符、货币符号等惯例各不相同。此外，舍入规则可能因货币、政府、公司等而异。某些编程语言提供了更易于处理货币值的类型。各种C++库都有用于此目的的类，但它们往往复杂且超出我们的讨论范围。Boost的C++多精度库就是这样一个例子。

### 5.7.1 演示 `DollarAmount` 类

**图5.7**使用 `DollarAmount` 对象进行加法、减法以及复利计算。第10–11行创建 `DollarAmount` 对象 `d1` 和 `d2`，并分别将其初始化为 `12345` 美分（即$123.45）和 `1576` 美分（即$15.76）。第13–14行通过调用每个对象的 `toString` 成员函数获取对象的 `string` 表示，从而显示 `DollarAmount` 对象的值。接下来，第15行调用 `d1` 的 `add` 成员函数，传入 `d2` 作为参数。该语句将两个对象的值相加，并将结果存储到对象 `d1` 中。最后，第16行显示 `d1` 修改后的值。第18–21行和第23–26行演示了 `DollarAmount` 的 `subtract` 成员函数。第20行从 `d1` 中减去 `d2`，再次修改了 `d1`。第25行从 `d2` 中减去 `d1`，以演示计算结果为负的 `DollarAmount`。输出的前三行显示了这些加法和减法运算的结果。

```cpp
// Fig. 5.7: Interest.cpp
// Compound-interest calculations with class DollarAmount and integers.
#include <iostream>
#include <iomanip>
#include <string>
#include "DollarAmount.h"
using namespace std;

int main() {
   DollarAmount d1{12345}; // $123.45
   DollarAmount d2{1576};  // $15.76

   cout << "After adding d2 (" << d2.toString() << ") into d1 ("
      << d1.toString() << "), d1 = ";
   d1.add(d2); // modifies object d1
   cout << d1.toString() << "\n";

   cout << "After subtracting d2 (" << d2.toString() << ") from d1 ("
      << d1.toString() << "), d1 = ";
   d1.subtract(d2); // modifies object d1
   cout << d1.toString() << "\n";

   cout << "After subtracting d1 (" << d1.toString() << ") from d2 ("
      << d2.toString() << "), d2 = ";
   d2.subtract(d1); // modifies object d2
   cout << d2.toString() << "\n\n";

   cout << "Enter integer interest rate and divisor. For example:\n"
      << "for      2%, enter:    2 100\n"
      << "for    2.3%, enter:   23 1000\n"
      << "for   2.37%, enter:  237 10000\n"
      << "for  2.375%, enter: 2375 100000\n";
   int rate; // whole-number interest rate
   int divisor; // divisor for rate
   cin >> rate >> divisor;

   DollarAmount balance{100000}; // initial principal amount in pennies
   cout << "\nInitial balance: " << balance.toString() << endl;

   // display headers
   cout << "Year" << setw(20) << "Amount on deposit" << endl;

   // calculate amount on deposit for each of ten years
   for (unsigned int year{1}; year <= 10; year++) {
      // increase balance by rate % (i.e., rate / divisor)
      balance.addInterest(rate, divisor);

      // display the year and the amount
      cout << setw(4) << year << setw(20) << balance.toString() << endl;
   }
}
```

```
After adding d2 (15.76) into d1 (123.45), d1 = 139.21
After subtracting d2 (15.76) from d1 (139.21), d1 = 123.45
After subtracting d1 (123.45) from d2 (15.76), d2 = -107.69

Enter integer interest rate and divisor. For example:
for       2%, enter:     2 100
for    2.3%, enter:    23 1000
for   2.37%, enter:   237 10000
for   2.375%, enter:  2375 100000
> 5 100

Initial balance: 1000.00
```

| 年份 | 存款金额 |
|---:|---:|
| 1 | 1050.00 |
| 2 | 1102.50 |
| 3 | 1157.63 |
| 4 | 1215.51 |
| 5 | 1276.29 |
| 6 | 1340.10 |
| 7 | 1407.11 |
| 8 | 1477.47 |
| 9 | 1551.34 |
| 10 | 1628.91 |

```
After adding d2 (15.76) into d1 (123.45), d1 = 139.21
After subtracting d2 (15.76) from d1 (139.21), d1 = 123.45
After subtracting d1 (123.45) from d2 (15.76), d2 = -107.69

Enter integer interest rate and divisor. For example:
for     2%, enter:     2 100
for   2.3%, enter:    23 1000
for  2.37%, enter:   237 10000
for 2.375%, enter:  2375 100000
> 525 10000

Initial balance: 1000.00
```

| 年份 | 存款金额 |
|---:|---:|
| 1 | 1052.50 |
| 2 | 1107.76 |
| 3 | 1165.92 |
| 4 | 1227.13 |
| 5 | 1291.55 |
| 6 | 1359.36 |
| 7 | 1430.73 |
| 8 | 1505.84 |
| 9 | 1584.90 |
| 10 | 1668.11 |

图5.7 使用 `DollarAmount` 类和整数进行复利计算。

### 使用 `DollarAmount` 计算复利

`DollarAmount` 类的 `addInterest` 成员函数计算利息金额，并将其添加到调用该函数的 `DollarAmount` 对象中。该函数接收两个参数：

-   一个表示利率的整数
-   一个整数除数（10的幂）

为了确定利息金额，`addInterest` 将 `DollarAmount` 对象的美分数乘以利率的整数表示，然后将结果除以整数除数。例如：

- 要计算5%的利息，请输入整数5和100。在整数运算中，将 `DollarAmount` 乘以5，再将结果除以100，即可计算出该 `DollarAmount` 值的5%。
- 要计算5.25%的利息，请输入整数525和10000。在整数运算中，将 `DollarAmount` 乘以525，再将结果除以10000，即可计算出该 `DollarAmount` 值的5.25%。

第28–35行提示并输入 `rate` 和 `divisor`。第37行创建 `DollarAmount` 对象 `balance`，并将其初始化为 `100000` 美分（即$1,000）——初始本金，我们在第38行显示。第44–50行执行利息计算。第46行调用 `addInterest` 成员函数来执行当前年份的利息计算。然后，第49行显示当前的 `year` 和 `balance` 的 `string` 表示。你可以通过查看输出中第 `1` 年的新余额来确认是否正确输入了利率。例如，计算5%利率时，第一年的年末余额将是1050.00；计算5.25%利率时，第一年的余额将是1052.50。
