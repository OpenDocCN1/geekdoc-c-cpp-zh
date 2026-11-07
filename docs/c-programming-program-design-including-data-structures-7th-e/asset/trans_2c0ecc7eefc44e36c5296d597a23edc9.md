
## 习题

习题末尾括号中的数字指的是本章开头列出的学习目标。

1. 判断以下陈述的真假。

- a. 循环是一种控制结构，它使某些语句反复执行。(1)
- b. 在计数器控制的 `while` 循环中，不必初始化循环控制变量。(2)
- c. `while` 循环的循环体可能完全不执行。(2)
- d. 在无限 `while` 循环中，`while` 表达式（判断表达式）最初为假，但在第一次迭代之后始终为真。(2)
- e. 下面的 `while` 循环：

```cpp
j = 0;
while (j <= 10)
    j++;
```

如果 `j > 10` 则终止。(2, 3)

- f. 哨兵控制的 `while` 循环是一种事件控制的 `while` 循环，其终止取决于一个特殊值。(2, 3)
- g. 要从长度未指定的文件中读取数据，EOF 控制的循环是一个不错的选择。(3)
- h. 当 `while` 循环终止时，控制首先回到 `while` 语句之前的语句，然后转到紧跟在 `while` 循环之后的语句。(2, 3)

2. 以下 C++ 代码的输出是什么？(2, 3)

```cpp
int i = 2;
int temp = 1;
while (i < 10)
{
    temp = temp * (i - 1);
    i = i + 1;
}
cout << "i = " << i << " and temp = " << temp << endl;
```

3. 以下 C++ 代码的输出是什么？(2, 3)

```cpp
int count = 0;
int sum = 0;

while (count <= 8)
{
    sum = sum + static_cast<int>(sqrt(count));
    count++;
}
cout << sum << endl;
```

4. 以下 C++ 代码的输出是什么？(2, 3)

```cpp
int num = 0;
while (num * num <= 6 * num)
{
    num = num + 1;
    cout << num << " ";
}
cout << endl;
```

5. 以下 `while` 循环何时终止？(2, 3)

```cpp
ch = 'D';
while ('A' <= ch && ch <= 'Z')
    ch = static_cast<char>(static_cast<int>(ch) + 1);
```

6. 假设输入为 1 20 35 15 28 66 -1。以下代码的输出是什么？(2, 3)

```cpp
int num;
int sum;
int count;

cin >> count;
cin >> sum;

while (count <= 4)
{
    cin >> num;
    sum = sum + num;
    count++;
}
cout << "Sum = " << sum << endl;
```

7. 假设输入为 3 4 6 7 2 -1。以下代码的输出是什么？(2, 3)

```cpp
int num;
int sum;

cin >> sum;
num = sum;

while (num != -1)
{
    cin >> num;
    sum = sum + 2 * num;
}
cout << "Sum = " << sum << endl;
```

8. 假设输入为 3 4 6 7 2 -1。以下代码的输出是什么？(2, 3)

```cpp
int num;
int sum;

cin >> num;
sum = num;

while (num != -1)
{
    sum = sum + 2 * num;
    cin >> num;
}
cout << "Sum = " << sum << endl;
```

9. 假设输入为 10 -6 12 -5 -4 0。以下代码的输出是什么？(2, 3)

```cpp
int num;
int sum = 0;

cin >> num;

while (num != 0)
{
    if (num > 0)
        sum = sum + num;
    else
        sum = sum - num;
    cin >> num;
}
cout << "Sum = " << sum << endl;
```

10. 改正以下代码，使其读取并求出 20 个数的和：(2, 3)

```cpp
int count = 0;
int sum = 0;

cin >> num;
while (count <= 20);
{
    cin >> num;
    count++;
    sum = sum + count;
}
```

11. 考虑以下程序：(2, 3)

```cpp
#include <iostream>

using namespace std;

int main()
{
    int num1, num2;
    int temp = 0;

    cout << "Enter two integers: ";
    cin >> num1 >> num2;
    cout << endl;

    while (num1 % 3 != num2 % 5)
    {
        temp = num1 + num2;
        num1 = num2;
        num2 = temp;
        cout << temp << " ";
    }
    cout << endl;

    return 0;
}
```

- a. 如果输入为 10 17，输出是什么？
- b. 如果输入为 -4 11，输出是什么？
- c. 如果输入为 2 29，输出是什么？
- d. 如果输入为 7 43，输出是什么？

12. 假设输入为：

58   23   46   75   98   150   12   176   145   -999

以下程序的输出是什么？(2, 3)

```cpp
#include <iostream>

using namespace std;

int main()
{
    int num;
    int count = 0;
    cin >> num;

    while (num != -999)
    {
        count++;
        cout << num % count << " ";
        cin >> num;
    }

    cout << endl;

    return 0;
}
```

13. 以下程序旨在输入两个数并输出它们的和。它询问用户是否想运行该程序。如果回答是 Y 或 y，则提示用户输入两个数。在将数字相加并显示结果后，它再次询问用户是否想继续添加更多数字。然而，该程序未能做到这一点。改正程序，使其正常工作。(2, 3)

```cpp
#include <iostream>
#include <iomanip>

using namespace std;

int main()
{
    char response;
    double num1;
    double num2;

    cout << "This program adds two numbers." << endl;
    cout << "Would you like to run the program: (Y/y) ";
    cin >> response;
    cout << endl;

    cout << fixed << showpoint << setprecision(2);

    while (response == 'Y' && response == 'y')
    {
        cout << "Enter two numbers: ";
        cin >> num1 >> num2;
        cout << endl;

        cout << num1 << " + " << num2 << " = " << (num1 - num2)
             << endl;

        cout << "Would you like to add again: (Y/y) ";
        cin >> response;
        cout << endl;
    }
    return 0;
}
```

14. 以下程序段的输出是什么？(2, 3)

```cpp
int count = 1;

while (count++ <= 5)
    cout << "count: " << count << endl;
```

15. 以下程序段的输出是什么？(2, 3)

```cpp
int count = 5;

while (count > 0)
    cout << count-- << " ";
cout << endl;
```

16. 以下程序段的输出是什么？(2, 3)

```cpp
int count = 5;

while (count-- > 0)
    cout << count << " ";
cout << endl;
```

17. 以下程序段的输出是什么？(2, 3)

```cpp
int count = 1;
while (count++ <= 5)
    cout << count * (count - 2) << " ";

cout << endl;
```

18. 在以下每种情形中，你将使用哪种类型的循环，例如计数器控制或哨兵控制？(3)

- a. 求以下级数之和：1 + (2 / 1) + (3 / 2) + (4 / 3) + (5 / 4) + … + (10 / 9)
- b. 求以下数字之和，但不包括最后一个数：17, 32, 62, 48, 58, -1
- c. 一个文件包含一名员工的工资。更新该员工的工资。

19. 考虑以下 for 循环：(4)

```cpp
int j, s;

s = 0;
for (j = 1; j <= 10; j++)
    s = s + j * (j - 1);
```

在这个 for 循环中，指出循环控制变量、初始化语句、循环条件、更新语句，以及更新 s 值的语句。

20. 以下程序段的输出是什么？(4)

```cpp
int num = 1;
int i;

for (i = 0; i < 5; i++)
{
    num = num * (5 - i);
    cout << num << " ";
}
cout << endl;
```

21. 以下程序段的输出是什么？(4)

```cpp
int num = 0;
int count;
int y = 0;

for (count = 1; count <= 5; ++count)
{
    num = 3 * (count - 1) + (y - count);
    cout << num << " ";
}
cout << count << " " << endl;
```

22. 假设以下代码已正确插入程序中。(4)

```cpp
int s = 0;
int i;

for (i = 0; i < 5; i++)
{
    s = 2 * s + i;
    cout << s << " ";
}
cout << endl;
```

- a. s 的最终值是什么？
  - (i) 11
  - (ii) 14
  - (iii) 26
  - (iv) 以上都不是
- b. 如果在 for 循环语句的右括号后插入一个分号，s 的最终值是什么？
  - (i) 0
  - (ii) 1
  - (iii) 2
  - (iv) 5
  - (v) 以上都不是
- c. 如果将 for 循环控制表达式中的 5 替换为 0，s 的最终值是什么？
  - (i) 0
  - (ii) 1
  - (iii) 2
  - (iv) 以上都不是

23. 指出以下各语句会产生什么输出（如果有的话）：(4)

- a.

```cpp
for (i = 1; i <= 1; i++)
    cout << "* ";
cout << endl;
```

- b.

```cpp
for (i = 2; i >= 1; i++)
    cout << "* ";
cout << endl;
```

