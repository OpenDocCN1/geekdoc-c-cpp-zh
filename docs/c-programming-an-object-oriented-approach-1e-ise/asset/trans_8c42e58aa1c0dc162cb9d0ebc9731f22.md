

## 优先级与结合性

当我们尝试计算包含关系表达式和相等表达式的复杂表达式时，需要注意这两组运算符的优先级和结合性。在复杂表达式中，括号有助于指明求值顺序。以下是一些示例：

```cpp
3 < 4 == 1        // 根据优先级，表达式为 (3 < 4) == 1。结果为 true。
2 < 3 < 0         // 根据结合性，表达式为 (2 < 3) < 0。结果为 false。
3 <= 6 < 5        // 根据结合性，表达式为 (3 <= 6) < 5。结果为 true。
4 == 4 < 2        // 根据优先级，表达式为 4 == (4 < 2) 或 4 == 0。结果为 false。
```

## 易犯错误

我们应避免对浮点值使用相等运算符，因为我们不知道这些值在内存中的存储精度。换句话说，结果取决于系统。

```cpp
x == 2.78123       // 即使 x 的值为 2.78123，结果也可能为 false。
x != 14.67823      // 即使 x 的值接近 14.67823，结果也可能为 true。
```

## 4.1.2 单向选择：if 语句

最常见的决策结构是单向选择，在 C++ 中通过 if 语句实现。图 4.1 展示了单向选择的逻辑以及 C++ 中 if 语句的语法。

在这种类型的语句中，我们使用表达式来测试条件。如果测试结果为 true，程序就执行该语句（或一组语句）；如果结果为 false，则跳过该语句（或一组语句）。请注意，如果要执行多个语句，就需要使用复合语句。

这种选择通常称为单向选择：执行某项任务或不执行该任务。请注意，只有在每次运行程序时，选择表达式的结果都无法预知（取决于所测试的条件），它才有意义。换句话说，关系表达式或相等表达式的结果应取决于程序的输入；否则，决策就没有意义。

请注意，当测试结果为 true 时要执行的语句是一个单独的语句，但这个单独的语句可以是复合语句（即包含在一对大括号中的一组语句）。有些程序员在只需执行一条语句时会省略大括号。我们强烈不建议这样做。即使只需执行一条语句，大括号也能清晰地显示程序的执行流程。

![](img/d68f6199646ca63591a6d8419e0ed4ba_132_0.png)

### 程序 4.1 输出绝对值

```cpp
1  /************************************************************
2   * Using if-statement to print the absolute value of a number        *
3   ************************************************************/
4  #include <iostream>
5  using namespace std;
6
7  int main ()
8  {
9      // Declaration
10     int number;
11     // Getting input
12     cout << "Enter an integer: ";
13     cin >> number;
14     // Finding the absolute value
15     if (number < 0)
16     {
17         number = -number;
18     }
19     // Printing the absolute value
20     cout << "Absolute value of the number you entered is: " << number;
21     return 0;
22 }
```

```text
运行：
Enter an integer: 25
Absolute value of the number you entered is: 25

运行：
Enter an integer: -17
Absolute value of the number you entered is: 17
```

### 示例 4.1

程序 4.1 展示了 if 语句的一种非常简单的用法：求出程序用户输入的整数的绝对值。如果用户输入的是负整数，程序就将它改为大小相同的正整数；否则，程序不做任何操作。程序退出决策部分（第 15 至 18 行）后，会输出所输入整数的绝对值。

请注意，在这个简单示例中，我们不需要使用大括号（第 16 和 18 行），但使用大括号是一种良好的编程习惯。

### 示例 4.2

程序 4.2 同样展示了 if 语句的用法。它用于计算员工每周的税前总收入。如果员工一周工作超过 40 小时，超出部分的加班工资率为基本工资率的 130%。

### 程序 4.2 员工税前总收入

```cpp
/****************************************************************
 * Use of if-statement to find gross payment of an employee      *
 ****************************************************************/
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    // Declaration
    double hours;
    double rate;
    double regularPay;
    double overPay;
    double totalPay;
    // Input
    cout << "Enter hours worked: ";
    cin >> hours;
    cout << "Enter pay rate: ";
    cin >> rate;
    // Calculation that does not depend on decision
    regularPay = hours * rate;
    overPay = 0.0;
    // Calculation that is skipped if hours worked is not more than 40
    if (hours > 40.0)
    {
        overPay = (hours - 40.0) * rate * 0.30;
    } // End if
    // Rest of the calculation
    totalPay = regularPay + overPay;
    // Printing output
    cout << fixed << showpoint;
    cout << "Regular pay = " << setprecision (2) << regularPay << endl;
    cout << "Over time pay = " << setprecision (2) << overPay << endl;
    cout << "Total pay = " << setprecision (2) << totalPay << endl;
    return 0;
}
```

```text
运行：
Enter hours worked: 30
Enter pay rate: 22.00
Regular pay = 660.00
Over time pay = 0.00
Total pay = 660.00
```

### 程序 4.2 员工税前总收入（续）

```text
运行：
Enter hours worked: 45
Enter pay rate: 25.00
Regular pay = 1125.00
Over time pay = 37.50
Total pay = 1162.50
```

在第一次运行中，由于员工工作时间少于 40 小时，程序会忽略第 27 行的语句。加班工资保持初始化时的 0.0。在第二次运行中，由于员工工作时间超过 40 小时，程序会执行第 27 行的语句，计算出 37.50 美元的加班工资，并将其加到 *regularPay* 上，使 *totalPay* 达到 1162.50 美元。

### 一些易犯错误

使用 *if* 语句进行单向选择时，我们必须仔细留意可能出现的问题。这些错误通常不会被编译器发现，因为它们是逻辑错误，而非语法错误。我们编译并运行程序后，才会发现结果不正确。

**误用赋值运算符而非相等运算符** 一种常见错误是使用赋值运算符（=）而非相等运算符（==）。以下是一个示例：

```cpp
if (x = 0)        // This statement is always false.
{
  statement;      // The statement is never executed.
}
```

请注意，在这种情况下，无论 x 的值是什么，条件都始终为 *false*。该表达式会将 x 的值改为 0（这并非我们的本意）。表达式的结果就是 x 的值，即 0。我们已经知道，在需要布尔值的表达式中，0 会被解释为 *false*。这意味着该语句永远不会执行。

类似地，如果使用 (x = 5) 而不是 (x == 5)，结果就始终为 *true*，该语句也始终会执行，如下所示：

```cpp
if (x = 5)        // This condition is always true.
{
  statement;      // The statement is always executed.
}
```

**忘记大括号** 另一个常见错误是在需要执行多个语句时忘记大括号：

```cpp
if (x == 0)
  statement1;     // 如果 x 等于 0，则执行 Statement1。
  statement2;     // Statement2 总是会执行。
```

### 程序 4.3 判断成绩是否及格

```cpp
/************************************************************
 * Use of an if-else statement to find a pass/no-pass grade *
 ************************************************************/
#include <iostream>
using namespace std;

int main()
{
    // Local Declaration
    int score;
    // Input
    cout << "Enter a score between 0 and 100: ";
    cin >> score;
    // Decision
    if (score >= 70)
    {
        cout << "Grade is pass" << endl;
    } // End if
    else
    {
        cout << "Grade is nopass" << endl;
    } // End else
    return 0;
}
```

```text
运行：
Enter a score between 0 and 100: **65**
Grade is nopass

运行：
Enter a score between 0 and 100: **92**
Grade is pass
```

### 示例 4.4

程序 4.4 要求用户输入两个整数，并输出其中较大的一个。

### 程序 4.4 求两个数中的较大值

```cpp
/************************************************************
 * Use of if-else statement to print larger between two numbers *
 * or print the first if numbers are equal                    *
 ************************************************************/
#include <iostream>
```

