
3. 以下 C++ 代码的输出是什么？(2, 3)

```cpp
int count = 0;
int sum = 0;
while (count <= 5)
{
    sum = sum + count * (count - 1);
    count++;
}
cout << sum << endl;
```

4. 以下 C++ 代码的输出是什么？(2, 3)

```cpp
int num = 1;
while (num * num <= 50)
{
    cout << num << " ";
    num = num + 2;
}

cout << endl;
```

5. 以下 while 循环何时终止？(2, 3)

```cpp
char ch = 'D';
while ('A' <= ch && ch <= 'Z')
    ch = static_cast<char>(static_cast<int>(ch) + 1);
```

6. 假设输入为 0 0 8 12 50 7 13 -1。以下代码的输出是什么？(2, 3)

```cpp
int num, sum, count;
cin >> sum;
cin >> count;
cin >> num;

while (count <= 4)
{
    sum = sum + num;
    count++;
    cin >> num;
}
cout << "Sum = " << sum << endl;
```

7. 假设输入为 0 5 6 4 9 8 -1。以下代码的输出是什么？(2, 3)

```cpp
int num = 0;
int sum;
cin >> sum;

while (num != -1)
{
    cin >> num;
}
sum = sum + 2 * static_cast<int>(sqrt(num));
cout << "Sum = " << sum << endl;
```

8. 假设输入为 0 5 6 4 9 8 -1。以下代码的输出是什么？(2, 3)

```cpp
int num;
int sum;

cin >> num;
sum = num;

while (num != -1)
{
    sum = sum + num * (num - 1);
    cin >> num;
}
cout << "Sum = " << sum << endl;
```

9. 假设输入为 20 -16 -5 15 6 0。以下代码的输出是什么？(2, 3)

```cpp
int num;
int temp = 0;

cin >> num;

while (num != 0)
{
    if (num % 2 == 0)
        temp = temp + num;
    else
        temp = temp - num;
    cin >> num;
}
cout << "temp = " << temp << endl;
```

10. 改正以下代码，使其读取并求出 20 个数的和。(2, 3)

```cpp
int count = 0;
int sum = 0;

while (count <= 20);
{
    sum = sum + count;
    count++;
    cin >> num;
}
```

11. 考虑以下程序。(2, 3)

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

    while ((num1 + num2) % 2 != (num1 + num2) % 3)
    {
        temp = num1 + num2;
        num1 = num2;
        num2 = temp;
        cout << temp << " ";
    }
    cout << " *" << endl;

    return 0;
}
```

- a. 如果输入为 `10 10`，输出是什么？
- b. 如果输入为 `4 11`，输出是什么？
- c. 如果输入为 `12 29`，输出是什么？
- d. 如果输入为 `10 17`，输出是什么？

12. 假设输入为：

`32 53 -10 45 -56 -87 132 165 -999`

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
        cout << num % (count + 1) << " ";
        cin >> num;
        count++;
    }

    cout << endl;

    return 0;
}
```

13. 以下程序旨在输入两个数并输出它们的和。它会询问用户是否愿意运行该程序。如果答案为 Y 或 y，则提示用户输入两个数。在将数字相加并显示结果后，它会再次询问用户是否愿意继续添加更多数字。然而，该程序未能做到这一点。请改正程序，使其正常工作。(2, 3)

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
int count = 0;

while (++count < 5)
    cout << count + 1 << " ";
cout << endl;
```

15. 以下程序段的输出是什么？(2, 3)

```cpp
int count = 0;

while (count++ < 5)
    cout << count + 1 << " ";
cout << endl;
```

16. 以下程序段的输出是什么？(2, 3)

```cpp
int count = 5;

while (--count > 0)
    cout << 2 * count << " ";
cout << endl;
```

17. 以下程序段的输出是什么？(2, 3)

```cpp
int count = 0;
while (count++ <= 5)
    cout << (count - 1) * (count - 2) << " ";

cout << endl;
```

18. 在下列每种情况下，你将使用哪种类型的循环，例如计数器控制循环或哨兵控制循环？(3)

- a. 求以下级数之和：1 + (2 / 1) + (3 / 2) + (4 / 3) + (5 / 4) + ... + (10 / 9)
- b. 求以下数字之和，但不包括最后一个数字：17, 32, 62, 48, 58, -1
- c. 一个文件包含员工工资。更新员工工资。

19. 考虑以下 *for* 循环。(4)

```cpp
int j, s;

s = 0;
for (j = 1; j <= 10; j++)
    s = s + j * (j - 1);
```

在这个 *for* 循环中，指出循环控制变量、初始化语句、循环条件、更新语句，以及更新 s 值的语句。

- c.
  ```cpp
  for (i = 1; i <= 1; i--)
      cout << "**";
  cout << endl;
  ```

- d.
  ```cpp
  for (i = 12; i >= 9; i--)
      cout << "**";
  cout << endl;
  ```

- e.
  ```cpp
  for (i = 0; i <= 5; i++)
      cout << "**";
  cout << endl;
  ```

- f.
  ```cpp
  for (i = 1; i <= 5; i++)
  {
      cout << "**";
      i = i + 1;
  }
  cout << endl;
  ```

24. 编写一个 `for` 语句，求 1 到 1000 之间所有能被 3 或 5 整除的数之和。(4)

25. 以下代码的输出是什么？变量 x 和 y 之间有关系吗？如果有，请说明该关系？输出是什么？(4)

```cpp
int x = 19683;
int i;
int y = 0;

for (i = x; i >= 1; i = i / 3)
    y++;
cout << "x = " << x << ", y = " << y << endl;
```

26. 以下代码的输出是什么？(4)

```cpp
for (int k = 2; k <= 10000; k = k * k)
    cout << k << " ";
cout << endl;
```

27. 以下 C++ 程序段的输出是什么？假设所有变量都已正确声明。(4)

```cpp
for (j = 0; j < 8; j++)
{
    cout << j * 25 << " - ";

    if (j != 7)
        cout << (j + 1) * 25 - 1 << endl;
    else
        cout << (j + 1) * 25 << endl;
}
```

28. 假设输入为 6 -2 4 9 -5 8。以下代码的输出是什么？(4)

```cpp
int num, count, temp = 1;

cin >> num;

for (count = 1; count <= 4; count++)
{
    temp = temp + temp * (num + count);
    cin >> num;
}
cout << "temp = " << temp << endl;
```

29. 以下哪些仅适用于 while 循环？哪些仅适用于 do...while 循环？哪些两者都适用？(2, 5)

- a. 它被视为条件循环。
- b. 循环体至少执行一次。
- c. 控制循环的逻辑表达式在进入循环之前求值。
- d. 循环体可能完全不执行。

30. 以下程序包含会阻止其编译和/或运行的错误。请改正所有此类错误。(4)

```cpp
#include <stream>

#using namespace sdt;

const int LIMIT = 35;

int main();
{
    long long num1, num2;
    double first, second;

    cout >> "Enter two integers less than 100: "
    cin << num1 >> num2;
    cout >> endl;

    for (count = 1; count < Limit; count+)
    {
        first = (num1 * num2) / 2.0;
        if (num1 / num2 == 0)
            second = (num1 - num2) % 2.0;
        else
            second = num1 + num;
        num1 = num1 + num2;
        num2 := num2 * (count - LIMIT)
    }
}
```
