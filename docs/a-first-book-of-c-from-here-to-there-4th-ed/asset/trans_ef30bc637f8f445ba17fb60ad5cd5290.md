

## 程序 4.5

```
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    double monthlySales, income;

    cout << "Enter the value of monthly sales: ";
    cin >> monthlySales;
    if (monthlySales >= 50000.00)
        income = 375.00 + .16 * monthlySales;
    else if (monthlySales >= 40000.00)
        income = 350.00 + .14 * monthlySales;
    else if (monthlySales >= 30000.00)
        income = 325.00 + .12 * monthlySales;
    else if (monthlySales >= 20000.00)
        income = 300.00 + .09 * monthlySales;
    else if (monthlySales >= 10000.00)
        income = 250.00 + .05 * monthlySales;
    else
        income = 200.00 + .03 * monthlySales;

    cout << setiosflags(ios::showpoint)
         << setiosflags(ios::fixed)
         << setprecision(2)
         << "The income is $" << income << endl;

    return 0;
}
```

程序 4.5 的一个示例运行如下：

```
Enter the value of monthly sales: 36243.89
The income is $4674.27
```

## 练习 4.3

- 1. （练习）锐角小于 90 度，钝角大于 90 度，直角等于 90 度。利用此信息，编写一个 C++ 程序，接受以度为单位的角度，并显示对应输入度的角度类型。

利用此信息，编写、编译并运行一个 C++ 程序，以用户输入接受雷诺数并显示一条消息，指示流动是层流、湍流还是过渡的。

### 6. （程序）系统关键部件的公差根据以下时间表确定：

| 规格状态 | 公差 |
|---|---|
| 航天探索 | 小于 0.1% |
| 军用级 | 大于或等于 0.1% 且小于 1% |
| 商用级 | 大于或等于 1% 且小于 10% |
| 玩具级 | 大于或等于 10% |

利用此信息，编写、编译并运行一个 C++ 程序，接受部件的公差读数并确定应分配给它的规格。

### 7. （程序）a. 编写、编译并运行一个程序，接受两个实数和一个选择代码作为用户输入。如果输入的选择代码为 1，则程序应将两个先前输入的数字相加并显示结果；如果选择代码为 2，则应将数字相乘；如果选择代码为 3，则应将第一个数字除以第二个数字。

b. 确定在练习 7a 中编写的程序在输入的数字为 3 和 0 且选择代码为 3 时会做什么。

c. 修改练习 7a 中编写的程序，使其不允许除以 0，并在尝试此除法时显示一条消息。

### 8. （程序）从原点开始的线段所在象限由该线段与正 x 轴的夹角决定，如下所示：

| 从正 x 轴的角度 | 象限 |
|---|---|
| 在 0 到 90 度之间 | I |
| 在 90 到 180 度之间 | II |
| 在 180 到 270 度之间 | III |
| 在 270 到 360 度之间 | IV |

a. 利用此信息，编写、编译并运行一个 C++ 程序，以用户输入接受线的角度并确定并显示输入数据的正确象限。 （注意：如果角度恰好为 0、90、180 或 270 度，则相应的线不在任何象限内，而是位于坐标轴上。）

b. 修改为练习 8a 编写的程序，以显示一条消息，将 0 度的角度标识为正 x 轴，将 90 度的角度标识为正 y 轴，将 180 度的角度标识为负 x 轴，将 270 度的角度标识为负 y 轴。

### 9. （程序）编写、编译并运行一个 C++ 程序，接受一个数字后跟一个空格然后是一个字母。如果数字后面的字母是 f，则程序应将输入的数字视为华氏温度，将其转换为等效摄氏温度并显示合适的消息。如果字母是 c，则程序应将输入的数字视为摄氏温度，将其转换为等效华氏温度并显示合适的消息。如果字母既不是 f 也不是 c，则程序应显示一条消息，指出输入的数据不正确然后终止。使用程序中的 if-else 链并使用以下转换公式：摄氏 = (5.0 / 9.0) × (华氏 - 32.0) 华氏 = (9.0 / 5.0) × 摄氏 + 32.0

### 10. （程序）许多州根据汽车的车型年份和重量，使用类似于以下的时间表来确定年度汽车注册费：

| 车型年份 | 重量 | 重量等级 | 注册费 |
|---|---|---|---|
| 1990 年或更早 | 少于 2700 磅 | 1 | 26.50 |
|  | 2700 到 3800 磅 | 2 | 35.50 |
|  | 超过 3800 磅 | 3 | 56.50 |
| 1991 年至 1999 年 | 少于 2700 磅 | 4 | 35.00 |
|  | 2700 到 3800 磅 | 5 | 45.50 |
|  | 超过 3800 磅 | 6 | 62.50 |
| 2000 年或以后 | 少于 3500 磅 | 7 | 49.50 |
|  | 3500 磅或更多 | 8 | 62.50 |

利用此信息，编写、编译并运行一个 C++ 程序，接受汽车的年份和重量并确定并显示其重量等级和注册费。

### 11. （调试）使用程序 4.5 中的佣金时间表，以下程序计算月收入：

```
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    double monthlySales, income;

    cout << "Enter the value of monthly sales: ";
    cin >> monthlySales;
    if (monthlySales >= 50000.00)
        income = 375.00 + .16 * monthlySales;
    if (monthlySales >= 40000.00 && monthlySales < 50000.00)
        income = 350.00 + .14 * monthlySales;
    if (monthlySales >= 30000.00 && monthlySales < 40000.00)
        income = 325.00 + .12 * monthlySales;
```

```
if (monthlySales >= 20000.00 && monthlySales < 30000.00)
    income = 300.00 + .09 * monthlySales;
if (monthlySales >= 10000.00 && monthlySales < 20000.00)
    income = 250.00 + .05 * monthlySales;
if (monthlySales < 10000.00)
    income = 200.00 + .03 * monthlySales;
```

```
cout << setiosflags(ios::showpoint)
    << setiosflags(ios::fixed)
    << setprecision(2)
    << "\n\nThe income is $" << income << endl;
```

```
return 0;
}
```

- a. 此程序是否会产生与程序 4.5 相同的输出？
- b. 哪个程序更好？为什么？

### 12. （调试）以下程序被编写为产生与程序 4.5 相同的结果：

```
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    double monthlySales, income;

    cout << "Enter the value of monthly sales: ";
    cin >> monthlySales;
```

```
if (monthlySales < 10000.00)
    income = 200.00 + .03 * monthlySales;
else if (monthlySales >= 10000.00)
    income = 250.00 + .05 * monthlySales;
else if (monthlySales >= 20000.00)
    income = 300.00 + .09 * monthlySales;
else if (monthlySales >= 30000.00)
    income = 325.00 + .12 * monthlySales;
else if (monthlySales >= 40000.00)
    income = 350.00 + .14 * monthlySales;
else if (monthlySales >= 50000.00)
    income = 375.00 + .16 * monthlySales;
```

```
cout << setiosflags(ios::showpoint)
    << setiosflags(ios::fixed)
    << setprecision(2)
    << "The income is $" << income << endl;

return 0;
}
```

- a. 这个程序做什么？
- b. 对于哪些月销售额值，这个程序会计算正确的收入？

## 4.4 switch 语句

if-else 链用于编程应用中，必须从许多可能的选择中选择一组指令。switch 语句是 if-else 链的替代方案，用于比较整数表达式与特定值的情况。它具有以下一般形式：

```
switch (integer_expression)
{   // 复合语句的开始
    case value_1:  // 以冒号结尾
        statement1;
        statement2;
        .
        .
        break;
    case value_2:  // 以冒号结尾
        statementm;
        statementn;
        .
        .
        break;
    .
    .
    case value_n:  // 以冒号结尾
        statementw;
        statementx;
        .
        .
        break;
    default:  // 以冒号结尾
        statementaa;
        statementbb;
        .
        .
}   // switch 和复合语句的结束
```

