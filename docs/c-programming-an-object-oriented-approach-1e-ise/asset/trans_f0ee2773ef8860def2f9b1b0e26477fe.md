

## 程序 4.16 一个人的税负（续）

```cpp
48    cout << "Income: " << income << endl;
49    cout << "Tax due: " << tax;
50    return 0;
51 }
```

运行：

```text
Enter income in dollars: 8500
Income: 8500
Tax due: 425
```

运行：

```text
Enter income in dollars: 14500
Income: 14500
Tax due: 950
```

运行：

```text
Enter income in dollars: -5
Error! Invalid income!
```

运行：

```text
Enter income in dollars: 123000
Income: 123000
Tax due: 16600
```

第三次运行中的收入（-5）无效；除此之外，每次运行中的收入都属于某个税率档次。在第一次运行中，纳税人处于第 1 档，需要缴纳其收入的 5% 作为税款（425）。在第二次运行中，纳税人处于第 2 档。她需要为第 1 档（前 10000 美元）缴纳 500 美元，并为第 2 档（剩余的 4500 美元）缴纳 450 美元，依此类推。请验证每个结果是否正确。

## 4.5.3 日期编号

假设我们为一年中的每一天分配一个日期编号。例如，1 月 1 日是第 1 天，12 月 31 日是第 365 天。我们希望根据月份和当月的日期，找出某一天在一年中的编号。

### 理解问题

要解决这个问题，我们需要知道月份和该月的日期。我们需要月份，是因为必须计算所有前面月份经过的天数。

### 制定算法

该算法需要完成两个任务：加上所有过去月份的天数，以及加上当前月份中的日期编号。第一个任务通过一个 *switch* 语句完成，每个月对应一个 case。第二个任务在 *switch* 语句之后完成。采用贯穿方式（不使用 *break* 语句）的 *switch* 语句非常适合这个问题，因为我们需要累计前面月份经过的天数。为了让 *switch* 语句正常工作，我们从一年中的最后一个月开始，依次处理到第一个月。例如，如果当前是第 7 个月，我们进入 case 7，但会加上第 6 个月到第 1 个月的天数。执行完 *switch* 语句后，再加上当前月份中的日期数。

### 编写代码

程序 4.17 遵循上述算法。请注意，我们忽略了闰年的情况；在闰年中，2 月包含 29 天。闰年的情况留作练习。我们还忽略了输入错误，这些内容将在后续章节中讨论。

**程序 4.17** 日期编号

```cpp
/********************************************************
 * Finding the number of days passed from the beginning of the
 * year including the current day
 ********************************************************/
#include <iostream>
using namespace std;

int main ( )
{
    // Declaration
    int month;
    int day;
    int totalDays = 0;
    // Input current month and current day of the month
    cout << "Enter month: ";
    cin >> month;
    cout << "Enter day of month: ";
    cin >> day;
    // Number of days in months
    int m01 = 31;
    int m02 = 28;
    int m03 = 31;
    int m04 = 30;
    int m05 = 31;
    int m06 = 30;
    int m07 = 31;
    int m08 = 31;
    int m09 = 30;
    int m10 = 31;
    int m11 = 30;
    // Switch statement finds the total days using fall-through
    switch (month)
    {
        case 12 : totalDays += m11;
        case 11 : totalDays += m10;
        case 10 : totalDays += m09;
        case 9  : totalDays += m08;
        case 8  : totalDays += m07;
```

（续）

## 程序 4.17 日期编号（续）

```cpp
39    case 7 : totalDays += m06;
40    case 6 : totalDays += m05;
41    case 5 : totalDays += m04;
42    case 4 : totalDays += m03;
43    case 3 : totalDays += m02;
44    case 2 : totalDays += m01;
45    case 1 : totalDays += 0;
46  }
47  // Adding the day of the month to the previous total days
48  totalDays += day;
49  // Printing the result
50  cout << "Day number: " << totalDays;
51  return 0;
52}
```

运行：

```text
Enter month: 1
Enter day of month: 23
Day number: 23
```

运行：

```text
Enter month: 4
Enter day of month: 12
Day number: 102
```

运行：

```text
Enter month: 11
Enter day of month: 24
Day number: 328
```

运行：

```text
Enter month: 12
Enter day of month: 31
Day number: 365
```

## 关键术语

- 条件表达式
- 悬空 else
- 德·摩根定律
- *default* 分支
- 相等表达式
- if 语句
- if-else 语句
- 逻辑与表达式
- 逻辑表达式
- 逻辑非表达式
- 逻辑或表达式
- 多路选择
- 单路选择
- 关系表达式
- 短路行为
- switch 语句
- 双路选择

## 总结

为了解决某些问题，我们需要根据对真值条件的测试结果做出决定。这称为*选择*。最常见的决策结构是单路选择，在 C++ 中通过 *if 语句*实现。我们讨论的第二种选择语句是使用 *if-else 语句*的双路选择。

有时，决策问题过于复杂，无法仅使用关系表达式和相等表达式解决。我们可以将关系表达式和相等表达式与逻辑表达式结合起来实现选择。我们讨论了三种逻辑运算符：NOT、AND 和 OR。

C++ 中的另一种多路决策结构是 *switch 语句*，它根据特定值做出决策。

另一种可用于决策的结构称为*条件表达式*。它是 C++ 中唯一的*三元*表达式。它使用两个运算符和三个操作数。

## 习题

**PR-1.** 如果初始值为 x = 4、y = 0，执行以下代码后，x 和 y 的值是多少？

```cpp
if (x != 0)
{
    y = 3;
}
```

**PR-2.** 如果初始值为 x = 4、y = 0 和 z = 2，执行以下代码后，x、y 和 z 的值是多少？

```cpp
if (z == 2)
{
    y = 1;
}
else
{
    x = 3;
}
```

**PR-3.** 如果初始值为 x = 4、y = 0 和 z = 2，执行以下代码后，x、y 和 z 的值是多少？

```cpp
if (x > y || y < z)
{
    x = 10;
}
```

**PR-4.** 如果初始值为 x = *true*、y = *false* 和 z = *true*，执行以下代码后，x、y 和 z 的值是多少？

```cpp
if (x)
{
    if (y)
    {
        z = false;
    }
    else
    {
        y = true;
    }
}
```

**PR-5.** 如果初始值为 x = 4、y = 0 和 z = 2，执行以下代码后，x、y 和 z 的值是多少？

```cpp
if (z == 0 || y != 0)
{
    if (z <= 2)
    {
        z = 4;
    }
}
else
{
    y = 5;
    z = y + x;
}
```

**PR-6.** 如果初始值为 x = 0、y = 0 和 z = 1，执行以下代码后，x、y 和 z 的值是多少？

```cpp
switch (x)
{
    case 0: x = 2;
            y = 3;
    case 1: x = 4;
    default: y = 5;
             x = 1;
}
```

**PR-7.** 如果初始值为 x = 2、y = 1 和 z = 1，执行以下代码后，x、y 和 z 的值是多少？

```cpp
switch (x)
{
    case 0: x = 3;
            y = 2;
    case 1: x = 2;
    default: y = 3;
             x = 4;
}
```

**PR-8.** 使用 switch 语句重写下面的多路选择。

```cpp
if (x == 2)
{
    x++;
}
else if (x == 3)
{
    x--;
}
else
{
    cout << "End!";
}
```

**PR-9.** 使用多路 *if-else* 语句重写下面的 switch 语句。

```cpp
switch (x)
{
    case 1: cout << "One" << endl;
        break;
    case 2: cout << "Two" << endl;
        break;
    default: cout << "Any" << endl;
        break;
}
```

**PR-10.** 使用一个 *switch* 语句重写下面的代码片段。

```cpp
if (ch == 'R' || ch == 'a')
    countA++;
else if (ch == 'E' || ch == 'e')
    countE++;
else if (ch == 'T' || ch == 't')
    countT++;
else
    cout << "Error--Not A, E, or T" << endl;
```

**PR-11.** 编写一个代码片段：如果整型变量 *score* 大于或等于 90，则将值 1 赋给变量 *best*。

**PR-12.** 编写一个代码片段：如果浮点变量 *amount* 大于 5.4，则给整型变量 *num* 加 4。

**PR-13.** 编写一个代码片段：如果变量 *flag* 为 *true*，则打印整型变量 *num* 的值。

**PR-14.** 编写一个代码片段完成以下操作：如果变量 *divisor* 不为零，则用变量 *dividend* 除以 *divisor*，并将结果存储在 *quotient* 中。如果 *divisor* 为零，则将其赋给 *quotient*。然后打印这三个变量。假设变量 *dividend* 和 *divisor* 为整型，*quotient* 为双精度型。

**PR-15.** 编写一个代码片段来检查变量 *flag* 是否为 *true*；如果为 *true*，则读取整型变量 *num1* 和 *num2* 的值。然后计算并打印这两个输入值的和与平均值。如果变量 *flag* 为 *false*，则不执行任何操作。

**PR-16.** 编写一个代码片段来测试整型变量 *num1* 的值。如果该值为 10，则计算 *num1* 的平方。如果该值为 9，则向 *num1* 中读入一个新值。如果该值为 2 或 3，则将 *num1* 乘以 99 并打印结果。使用嵌套的 *if* 语句实现代码，不要使用 *switch* 语句。

