
## 程序 5.10 打印能被 7 整除的整数（续）

```cpp
using namespace std;

int main()
{
    // Declaration including initialization
    int lower = 1;
    int higher = 300;
    int divisor = 7;
    int col = 1;
    // Processing loop
    for (int i = lower; i < higher; i++)
    {
        if (i % divisor == 0)
        {
            cout << setw(4) << i;
            col++;
            if (col > 10)
            {
                cout << endl;
                col = 1;
            }
        }
    }
    return 0;
}
```

```text
Run:
  7   14   21   28   35   42   49   56   63   70
 77   84   91   98  105  112  119  126  133  140
147  154  161  168  175  182  189  196  203  210
217  224  231  238  245  252  259  266  273  280
287  294
```

## 示例 5.15

假设我们想要在给定某月的天数和该月第一天是星期几（0 到 6 分别表示星期日到星期六）的情况下打印该月的月历。程序 5.11 给出了一个解决方案。

## 程序 5.11 打印某月的日历

```cpp
/**************************************************************
 * Prints a month's calendar when we are given the number of days *
 * and the first day of the month.                              *
 **************************************************************/
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    // Declaration including initialization
    int startDay;
    int daysInMonth;
    int col = 1;
    // Validation of days in a Month
    do
    {
        cout << "Enter the number of days in the month (28, 29, 30, or 31): ";
        cin >> daysInMonth;
    } while (daysInMonth < 28 || daysInMonth > 31);
    // Validation of start day
    do
    {
        cout << "Enter start day (0 to 6): ";
        cin >> startDay;
    } while (startDay < 0 || startDay > 6);
    // Print titles
    cout << endl;
    cout << "Sun Mon Tue Wed Thu Fri Sat" << endl;
    cout << "---------------------------" << endl;
    // Print spaces before the startday
    for (int space = 0; space < startDay; space++)
    {
        cout << "  ";
        col++;
    }
    // Print the calendar
    for (int day = 1; day <= daysInMonth; day++)
    {
        cout << setw(3) << day << " ";
        col++;
        if (col > 7)
        {
            cout << endl;
            col = 1;
        }
    }
    return 0; // End main
}
```

```text
Run:
Enter the number of days in the month (28, 29, 30, or 31): 31
Enter start day (0 to 6): 3

Sun Mon Tue Wed Thu Fri Sat
---------------------------
                  1   2   3   4
  5   6   7   8   9  10  11
 12  13  14  15  16  17  18
 19  20  21  22  23  24  25
 26  27  28  29  30  31
```

## 5.4 *do-while* 语句

我们要讨论的最后一种重复语句是 *do-while 语句*，其中逻辑表达式在每次迭代结束时而不是开始时进行测试。因此，*do-while* 循环是一种 *后测试循环*。由于每次迭代中的逻辑表达式都是在循环体执行之后才进行测试，所以 *do-while* 语句中的循环体至少会执行一次（图 5.12）。

*do-while* 语句由五个部分组成：保留字 *do*、作为循环体的语句（通常是括在花括号中的复合语句）、保留字 *while*、括号中的逻辑表达式以及一个分号。注意，*do-while* 语句末尾必须有一个分号。

> **在 *do-while* 语句末尾必须有一个分号。**

### 5.4.1 事件控制循环

*do-while* 语句被设计用作事件控制循环。然而，*do-while* 循环的后测试特性需要采用不同的措施来控制循环。

### 至少一次迭代

当问题要求循环体至少执行一次时，*do-while* 循环是推荐的解决方案。

![](img/d68f6199646ca63591a6d8419e0ed4ba_198_0.png)

**图 5.12** do-while 语句的流程图和语法

当问题要求循环体至少执行一次时，我们使用 *do-while* 循环。

## 示例 5.16

我们想要编写一个程序，提取并打印任意非负整数的最左边一位数字。换句话说，如果输入的整数是 247，则应打印数字 2；如果整数是 7562，则应打印数字 7。程序 5.12 包含该问题的解决方案。

在第一次运行中，该数字只有一位。循环的第一次迭代提取出这一位数字，*num* 的值变为 0，这意味着循环终止。

## 程序 5.12 提取整数的最左边一位数字

```cpp
/*****************************************************************
 * Demonstrate the use of the do-while loop to extract the       *
 * left-most digit of an integer.                                *
 *****************************************************************/
#include <iostream>
using namespace std;

int main()
{
    // Declaration
    int num;
    short leftDigit;
    // Input
    cout << "Enter a non-negative integer: ";
    cin >> num;
    // Loop
    do
    {
        leftDigit = num % 10;
        num = num / 10;
    } while (num > 0);
    // Output
    cout << "The leftmost digit is: " << leftDigit << endl;
    return 0;
}
```

```text
Run:
Enter a non-negative integer: 5
The leftmost digit is: 5

Run:
Enter a non-negative integer: 4567
The leftmost digit is: 4
```

在第二次运行中，该数字有四位。这里第一次迭代提取最右边的数字（7），但第二次迭代会丢弃这个数字，并用新的最右边数字（6）替换它，因为进入第二次迭代时，num 的值是 456。一个四位数字会经历四次迭代。这个问题表明，我们确实至少需要一次迭代，因为输入的数字至少有一位（即使该数字是 0）。

### 数据验证

另一个需要至少一次迭代的常见示例是**数据验证**。当用户输入必须符合一组标准的数据时，程序中应包含数据验证。例如，当我们在航空公司预订系统中输入航班信息时，有些数据是必填的，有些是可选的。数据验证可确保我们已按正确格式输入所有必填数据。

## 示例 5.17

数据输入通常要求数据处于预定义范围内。例如，当我们将数字分数转换为等级时，考试分数通常位于 0 到 100 的范围内。如果用户输入了超出该范围的数字，程序需要重复请求，直到用户输入正确范围内的数字。程序 5.13 演示了这种数据验证。注意使用 *逻辑或* 和 *不等* 表达式来定义不可接受的范围。

在第一次运行中，用户输入了有效范围内的分数。循环体只执行一次，该分数被接受。在第二次运行中，用户两次输入了超出范围的分数。循环体重复执行三次；前两次迭代中输入的分数被丢弃，第三次迭代中输入的分数被接受。该程序表明，*do-while* 循环是适用于数据验证的设计。

## 程序 5.13 使用 *do-while* 循环进行验证

```cpp
/**************************************************************
 * Demonstrate the use of the do-while loop to validate data    *
 **************************************************************/
#include <iostream>
using namespace std;

int main ()
{
    // Declaration
    int score;
    char grade;
    // Input validation loop
    do
    {
        cout << "Enter a score between 0 and 100: ";
        cin >> score;
    } while (score < 0 || score > 100);
    // Decision
    switch (score / 10)
    {
        case 10: grade = 'A';
            break;
        case 9: grade = 'A';
            break;
        case 8: grade = 'B';
            break;
        case 7: grade = 'C';
            break;
        case 6: grade = 'D';
            break;
        default: grade = 'F';
    }
    // Output
    cout << "The grade is " << grade << endl;
    return 0;
}
```

```text
Run:
Enter a score between 0 and 100: 83
The grade is B

Run:
Enter a score between 0 and 100: 111
Enter a score between 0 and 100: 97
The grade is A
```

### 5.4.2 *do-while* 循环分析

我们在前一节分析了 *while* 循环，发现 *while* 循环是一种预测试循环，其中测试次数比迭代次数多一次。我们说 *for* 循环是 *while* 循环的一种变体，这意味着它遵循 *while* 循环的规范。分析 *do-while* 循环并将其与 *while* 循环进行比较是有用的。为此，我们像展开 *while* 循环那样展开一个 *do-while* 循环（图 5.13）。

> 在 *do-while* 循环中，如果循环体执行了 *n* 次，
> 则条件会被测试 *n* 次。

