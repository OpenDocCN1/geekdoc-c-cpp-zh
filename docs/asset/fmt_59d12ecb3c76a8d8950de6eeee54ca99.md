
```cpp
#include <iostream>

int main() {

    int num, sum, dig;

    sum = dig = 0;

    std::cout << "Enter number: ";

    std::cin >> num;

    if(num == 0)

        dig = 1;

    else

    {

        if(num < 0)

            num = -num;

        while (num != 0) {

            sum += num % 10;
            num /= 10; // Remove the last digit.
        }

    }
    std::cout << dig << " digits and their sum is " << sum << '\n';
    return 0;

}
```

## C.6.16
编写一个程序，连续读取 `[0, 255]` 之间的整数并以二进制形式显示。例如，如果用户输入 `32`，程序应该显示 `0100000`。如果用户输入的数字超出 `[0, 255]` 范围，程序应该显示输入的总次数。它还应该显示最小和最大的数字，以及 `[0, 50]` 之间输入数字的平均值。仅使用 `while` 循环。

```cpp
#include <iostream>

using std::cout;
using std::cin;

int main() {
    int i, num, times, cnt, min, sum;
    times = cnt = sum = 0;
    min = 255;
    max = -1;
    while(1) {
        cout << "\nEnter number: ";
        cin >> num;
        if(num < 0 || num > 255)
            break;
        i = 7;
        while (i >= 0) { // Check each bit.
            if((num >> i) & 1)
                cout << '1';
            else
                cout << '0';
            i--;
        }
        cout << "\n";
        i = 0;
        while (i < num) {
            cout << "\n";
            i++;
        }
        times++;
        if(num >= 0 && num <= 50) {
            sum += num;
            cnt++;
        }
        if (max < num)
            max = num;
        if (min > num)
            min = num;
    }
    cout << "Total number of times entered is: " << times << '\n';
    cout << "Min:" << min << " Max:" << max << '\n';
    if(cnt)
        cout << "Avg: " << (float)sum/cnt << '\n';
    else
        cout << "No integer in [0, 50] was entered\n";
    return 0;
}
```

## C.6.17
级 `1/1 - 1/3 + 1/5 - 1/7 ...` 的和收敛于 `pi/4`。编写一个程序，找出需要加多少项，直到结果以 `0.001` 的精度收敛到 `pi/4`。考虑 `pi` 等于 `3.14`。使用 `fabs()` 函数来检查收敛性。

```cpp
#include <iostream>
#include <cmath>

int main() {
    int i, terms;
    double a, val, final, sum;
    const double pi = 3.14, accuracy = 0.001;
    terms = sum = 0;
    a = 1;
    i = 1;
    final = pi/4;
    while (1) {
        terms++;
        sum += a/i;
        if (fabs(sum-final) < accuracy)
            break;
        a = -a;
        i += 2;
    }
    std::cout << "Sum: " << sum << " Terms: " << terms << '\n';
    return 0;
}
```

## C.18
编写一个程序，连续读取月份数字（`1=1`月，`12=12`月）、每月的第一（`1=周一`，`7=周日`），并显示该月的日历。如果输入的月份是二月，程序应提示用户输入该月的天数，即 `28` 或 `29`。如果给月份超出 `[1, 12]` 范围，程序应终止。

```cpp
#include <iostream>
using std::cout;
using std::cin;

int main() {
    int i, mon, mon_days, day, rows;
    while(1) {
        cout << "\nter month: ";
        cin >> mon;
        if(mon < 1 || mon > 12) {
            break;
        }
        if(mon == 2) {
            cout << "Enter Feb days: ";
            cin >> mon_days;
        }
        else if(mon==4 || mon == 6 || mon == 9 || mon == 11) {
            mon_days = 30;
        }
        else {
            mon_days = 31;
        }
        cout << "Enter start day (1=Mon,7=Sun): \tTue\tWed\tThu\tFri\tSat\tSun\n";
        cin >> day;
        for(i = 1; i < day; i++) /* 添加一些空格直到月份的第一天
        of the month to格式化输出. */
        cout << '\t';
        rows = 0;
        for(i = 1; i <= mon_days; i++) {
            cout << i << '\t';
            if(i == 8-day+(rows*7)) {
                cout << '\n';
                rows++;
            }
        }
    }
    return 0;
}
```

# do-while 语句

与 `for` 和 `while` 语句（在执行体*之前*测试表达式）不同，`do-while` 语句在每次执行执行体*之后*测试表达式。因此，`do-while` 循环至少执行一次。它的形式如下：

```cpp
do
{
    /* 至少执行一次的语句块，
    只要 exp 的值为真，就会重复执行。 */
} while (exp);
```

首先执行循环体，然后求值 `exp`。如果为假，循环终止。如果为真，则再次执行循环体并测试 `exp`。这个过程一直重复，直到 `exp` 变为假。

例如，以下程序使用 `do-while` 语句显示从 `1` 到 `10` 的整数：

```cpp
#include <iostream> // Example 6.11
int main() {
    int i = 1;
    do {
        std::cout << i << '\n';
        i++;
    } while (i <= 10);
    return 0;
}
```

虽然单个语句周围的括号可以省略，但我总是使用它们，否则读者可能会误认为，将 `while` 部分视为一个独立的 `while` 语句。例如：

```cpp
do
    std::cout << i << '\n';
while(+i <= 10);
```

# 6 循环 127

```cpp
do {
    cout << "Enter number: ";
    cin >> num;
} while (num <= 0);
while (last != num);
return 0;
```

## C.6.21
编写一个程序，供老师使用以测试学生是否掌握了乘法口表。程序应该在 `[1, 10]` 范围内生成两个随机值（例如 `a` 和 `b`），并显示 `axb =`（较小的数字排在前面）。程序应提示学生输入结果，并显示一条信息性消息以指示答案是否正确。如果学生输入 `-1`，程序应该显示正确答案的总数并退出。

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
using std::cout;
using std::cin;

int main() {
    int i, j, num, fails, wins;
    fails = wins = 0;
    srand(time(NULL));
    do {
        i = rand()%10+1; /* rand() 返回一个随机正整数，运算符将其限制在 [0, 9] 内。我们加 1 将其限制在 [1, 10] 内。 */
        j = rand()%10+1;
        if (i < j) {
            cout << '\n' << i << ' x ' << j << ' = ';
        } else {
            cout << '\n' << j << ' x ' << i << ' = ';
        }
        cin >> num;
        if (num != -1) {
            if (num == i*j) {
                cout << "Correct\n";
                wins++;
            } else {
                cout << "Wrong. The answer is " << i*j << '\n';
                fails++;
            }
        }
    } while (num != -1);
    cout << "Fails: " << fails << " Wins: " << wins << '\n';
    return 0;
}
```

# C++ 绪

## C.22
编写一个程序根据泰勒级数计算 `sin(x)`：`sin(x) = x - x^3/3! + x^5/5! - x^7/7! ...`。程序应以度读取 `x`，将其转换为弧度，并计算结果，直到连续项之间的绝对差小于 `0.0001`。不要计算阶乘或进行幂运算。具体来说，计算新项时应使用前一项并将其乘以一个适当的数字。例如，计算 `x5/5!` 时使用前一项 `x3/3!` 并乘以 `x*x/4`。将 `pi` 视为 `3.14`，使用 `fabs()` 函数求差，并使用 `sin()` 函数比较结果。

```cpp
#include <iostream>
#include <cmath>

int main() {
    int i, a;
    double x, sum, prev_term, cur_term;
    const double pi = 3.14, accuracy = 0.0001;
    std::cout << "Enter x in degrees: ";
    std::cin >> x;
    x = pi*x/180; // 将度转换为弧度。
    sum = x;
    a = 1;
    cur_term = x;
    i = 2;
    do {
        a = -a;
        prev_term = cur_term;
        cur_term = prev_term * x*x/(i*(i+1));
        sum += cur_term * a;
        i += 2;
    } while (fabs(cur_term-prev_term) >= accuracy);
    std::cout << "Sum: " << sum << " Sin: " << sin(x) << '\n';
    return 0;
}
```

# goto 语句

`goto` 语句用于将控制转移到同一函数内的另一个语句，前提是该语句有一个标签。其语法如下：

```cpp
goto label;
```

当执行 `goto` 语句时，程序将控制转移到标签后的语句。标签被命名为变量，并且在使用 `goto` 语句的函数中必须是唯一的。它的名字后面必须跟一个冒号 `：` 标签的作用范围是整个函数。例如，在以下程序中，如果用户输入 `-1`，`goto` 语句将执行转移到 `START` 标签并重复循环。

```cpp
#include <iostream> // 示例 6.12
int main() {
    int i, num;
START:
for(i = 0; i < 5; i++)
{
    std::cout << "Enter number: ";
    std::cin >> num;
    if(num == -1) goto START; /* 我们可以写 i=-1; 并得到相同的结果；这只是如何使用 goto 的一个示例。 */
    return 0;
}
```

通常，最好避免使用 `goto`，因为它会导致程序的执行从一个点跳转到另一个点，使得代码难以阅读、维护和修改。但在某些情况下 `goto` 有用，例如：

```cpp
if(error_1)
    goto ERROR;
if(error_2)
    goto ERROR;
ERROR:
```

另一个例子，`goto` 可以帮助从嵌套循环中退出，跳转到这里：

```cpp
for(i = 0; i < 10; i++)
    for(j = 0; j < 20; j++)
    {
        if(condition)
            goto NEXT;
    }
NEXT:
```

在本章结束前，我想指出 `goto` 在某些情况下是有用的，尽管许多程序员反对它的使用。

## 未完成练习

**U.6.1** 编写一个计算 `1` 到 `99` 之和的程序。

**U.6.2** 编写一个计算 `1` 到 `n` 之和的程序，由用户提供 `n`。

**U.6.3** 程序的输出是什么？

```cpp
#include <iostream>
int main() {
    for (int i = 1; i <= 25; i++) {
        cout << "One\n";
    }
    return 0;
}
```

**U.6.4** 编写一个程序读取国家的人口及其增长率（百分比）。然后程序应读取年份并显示人口。

**U.6.5** 编写一个程序连续读取温度并显示等于、小于或大于 `40°F` 的温度。如果用户输入 `100`，则停止。

**U.6.6** 编写一个程序读取最多 `100` 个整数。如果输入大于上一个数字，则停止，并显示输入了多少个数字。

**U.6.7** 编写一个程序依次读取三个整数（例如 `a, b, c`），而不是一次性读取。程序应强制用户按降序输入（即 `a > b > c`）。

**U.6.8** 编写一个程序读取球的初始高度，并显示经过多少次跳后高度小于初始高度的 `1/4`。程序应提示用户输入减少率（%）。例如，输入值 `0.1` 每次落地弹起比上次少 `10%`。

**U.6.9** 编写一个程序连续读取整数，直到用户输入 `0`。然后程序应显示最大的正数和最小的负数。如果用户只输入正数或负数，程序应显示一条信息性消息。

**U.6.10** 编写一个程序强制读取十个正数。如果输入负数，程序应提示用户输入另一个。程序在退出前显示输入了多少个负数。使用一个 `for` 循环。

**U.6.11** 编写一个程序读取十个整数，并显示用户输入了多少唯一值。例如，如果用户输入 `-5, 10, 17, -31, -30, -29, 75, 76, 9, -4`，程序应显示 `3`，对：`{-31, -30}`, `{-30, -29}` 和 `{75, 76}`。

**12** 级数应该加上多少项：

```
S_1 = 4 + 10 + 16 + 22 + ...
S_2 = 1 + 8 + 15 + 22 + ...
```
