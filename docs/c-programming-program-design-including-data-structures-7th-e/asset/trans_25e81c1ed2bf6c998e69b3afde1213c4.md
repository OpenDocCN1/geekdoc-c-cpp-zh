

```
'R' > 'T' is false
'+' < '*' is false
'A' <= 'a' is true
```

注意，比较不同数据类型的值可能会产生不可预测的结果。例如，以下表达式比较一个整数和一个字符：

```
8 < '5'
```

在这个表达式中，在特定机器上，8 会与 '5' 的排序序列（即 53）进行比较。也就是说，8 与 53 进行比较，这使得这个特定表达式的求值结果为 true。

表达式 4 < 6 和 'R' > 'T' 是逻辑（布尔）表达式。当 C++ 对逻辑表达式求值时，如果该逻辑表达式的求值结果为 true，则返回整数值 1；否则返回整数值 0。在 C++ 中，任何非零值都被视为 true。

> **注意** 第 2 章介绍了数据类型 `bool`。回想一下，数据类型 `bool` 有两个值：`true` 和 `false`。在 C++ 中，`true` 和 `false` 是保留字。标识符 `true` 被设置为 1，标识符 `false` 被设置为 0。为了可读性，每当使用逻辑表达式时，这里将使用标识符 `true` 和 `false` 作为逻辑表达式的值。

既然我们知道了关系运算符如何工作，就可以开始学习如何在 C++ 程序中实现决策。尽管逻辑值只有两个，即 `true` 和 `false`，但它们极其有用，因为它们使程序能够纳入会改变处理流程的决策。本章剩余部分讨论将决策纳入程序的方法。在 C++ 中，有两种选择或分支控制结构：`if` 语句和 `switch` 结构。本节讨论如何使用 `if` 和 `if...else` 语句创建单向选择、双向选择和多路选择。`switch` 结构将在本章后面讨论。

## 单向选择

如果客户的支票账户余额低于所需最低余额，银行希望向其发送通知。也就是说，如果账户余额低于所需最低余额，就应向客户发送通知；否则，不执行任何操作。同样，如果保险单持有人不吸烟，保险公司希望对该保单保费应用 10% 的折扣。这两种情况

### 示例 4-3

```cpp
//Program to compute and output the penalty on an unpaid
//credit card balance. The program assumes that the interest
//rate on the unpaid balance is 1.5% per month.

#include <iostream>                         //Line 1
#include <iomanip>                          //Line 2

using namespace std;                        //Line 3

const double INTEREST_RATE = 0.015;         //Line 4

int main ()                                  //Line 5
{
    double creditCardBalance;               //Line 6
    double payment;                         //Line 7
    double penalty = 0.0;                   //Line 8

    cout << fixed << showpoint << setprecision(2);       //Line 11

    cout << "Line 12: Enter credit card balance: ";     //Line 12
    cin >> creditCardBalance;                            //Line 13
    cout << endl;                                        //Line 14

    cout << "Line 15: Enter the payment: ";             //Line 15
    cin >> payment;                                      //Line 16
    cout << endl;                                        //Line 17

    balance = creditCardBalance - payment;               //Line 18

    if (balance > 0)                                     //Line 19
        penalty = balance * INTEREST_RATE;               //Line 20

    cout << "Line 21: The balance is: $" << balance      //Line 21
         << endl;
    cout << "Line 22: The penalty to be added to your "   //Line 22
         << "next month bill is: $" << penalty << endl;

    return 0;                                            //Line 23
}                                                       //Line 24
```

**示例运行：** 在此示例运行中，用户输入以阴影表示。

```
Line 12: Enter credit card balance: 2500.00

Line 15: Enter the payment: 275.00

Line 21: The balance is: $2225.00
Line 22: The penalty to be added to your next month bill is: $33.38
```

第 7 行到第 10 行的语句声明了程序中使用的变量。第 12 行的语句提示用户输入信用卡账单金额。第 13 行的语句将金额输入到变量 `creditCardBalance` 中。第 15 行的语句提示用户输入付款金额。第 16 行的语句将付款金额输入到变量 payment 中。第 18 行的语句计算未付余额。第 19 行的 `if` 语句判断未付余额是否为正。如果未付余额为正，第 20 行的语句计算罚金。第 21 行和第 22 行的语句输出结果。该程序假设未付余额的年利率为 18%（即每月 1.5%）。如你所见，未付余额的利息会迅速累积，不仅会损害你的信用评级，还会使你陷入财务困境。

### 示例 4-4

考虑以下语句：

```cpp
if score >= 60      //syntax error
    grade = 'F';
```

这条语句展示了一个不正确的 `if` 语句版本。逻辑表达式两侧缺少圆括号，这是一个语法错误。

在 `if` 语句中，在表达式之后的圆括号后（即在语句之前）放置分号是一个语义错误。如果分号紧跟在右圆括号之后，`if` 语句将对空语句进行操作。

### 示例 4-5

考虑以下 C++ 语句：

```cpp
if (score >= 60);      //Line 1
    grade = 'F';       //Line 2
```

因为表达式末尾有一个分号（见第 1 行），所以第 1 行的 `if` 语句终止。这个 `if` 语句的动作是空操作，第 2 行的语句不属于第 1 行的 `if` 语句。因此，无论 `if` 语句的求值结果如何，第 2 行的语句都会执行。

## 双向选择

在许多编程情形中，你必须在两个备选方案之间做出选择。例如，如果兼职员工加班工作，工资单使用加班工资公式计算；否则，工资单使用常规公式计算。这是一个双向选择的例子。为了在两个备选方案之间做出选择——也就是实现双向选择——C++ 提供了 `if...else` 语句。双向选择使用以下语法：

### 示例 4-7

以下程序确定员工的周工资。如果工作小时数超过 40，则工资包含加班费。

```cpp
//Program: Weekly wages

#include <iostream>                                      //Line 1
#include <iomanip>                                       //Line 2

using namespace std;                                     //Line 3

int main()                                                //Line 4
{                                                         //Line 5
    double wages, rate, hours;                            //Line 6

    cout << fixed << showpoint << setprecision(2);        //Line 7
    cout << "Line 8: Enter working hours and rate: ";     //Line 8
    cin >> hours >> rate;                                  //Line 9

    if (hours > 40.0)                                      //Line 10
        wages = 40.0 * rate +                              //Line 11
                1.5 * rate * (hours - 40.0);               //Line 12
    else                                                  //Line 12
        wages = hours * rate;                              //Line 13

    cout << endl;                                          //Line 14
    cout << "Line 15: The wages are $" << wages << endl;  //Line 15

    return 0;                                              //Line 16
}                                                         //Line 17
```

**示例运行：** 在此示例运行中，用户输入以阴影表示。

Line 8: Enter working hours and rate: 50.00 12.50

Line 15: The wages are $687.50

第 6 行的语句声明了程序中使用的变量。第 7 行的语句将浮点数的输出设置为固定小数格式，带小数点、尾随零和两位小数。第 8 行的语句提示用户输入工作小时数和工资率。第 9 行的语句将这些值分别输入到变量 hours 和 rate 中。第 10 行的语句检查变量 hours 的值是否大于 40.0。如果 hours 大于 40.0，则由第 11 行的语句计算工资，其中包含加班费。否则，由第 13 行的语句计算工资。第 15 行的语句输出工资。

在双向选择语句中，在表达式之后、语句1之前放置分号会产生语法错误。如果 `if` 语句以分号结束，

