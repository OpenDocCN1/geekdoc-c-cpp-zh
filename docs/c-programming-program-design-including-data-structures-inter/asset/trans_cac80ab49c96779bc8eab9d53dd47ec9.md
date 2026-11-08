

```cpp
while (num != -999)
{
    cout << num % 25 << " ";
    cin >> num;
}

cout << endl;

return 0;
}
```

13. 以下程序旨在输入两个数并输出它们的和。它会询问用户是否想运行该程序。如果回答是 Y 或 y，则提示用户输入两个数。将数字相加并显示结果后，它会再次询问用户是否想继续添加更多数字。然而，该程序未能做到这一点。请改正程序，使其正常工作。

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

14. 以下程序段的输出是什么？

```cpp
int count = 0;

while (count++ < 10)
    cout << "This loop can repeat statements." << endl;
```

15. 以下程序段的输出是什么？

```cpp
int count = 5;

while (--count > 0)
    cout << count << " ";
cout << endl;
```

16. 以下程序段的输出是什么？

```cpp
int count = 5;

while (count-- > 0)
    cout << count << " ";
cout << endl;
```

17. 以下程序段的输出是什么？

```cpp
int count = 1;
while (count++ <= 5)
    cout << count * (count - 2) << " ";

cout << endl;
```

18. 在以下每种情况下，你将使用哪种类型的循环，例如计数器控制和哨兵控制？

- a. 对以下级数求和：1 + (2 / 1) + (3 / 2) + (4 / 3) + (5 / 4) + ... + (10 / 9)

- b. 对以下数字求和，最后一个数字除外：17, 32, 62, 48, 58, −1

- c. 一个文件包含一名员工的工资。更新该员工的工资。

19. 考虑以下 for 循环：

```cpp
int j, s;

s = 0;
for (j = 1; j <= 10; j++)
    s = s + j * (j - 1);
```

在这个 for 循环中，指出循环控制变量、初始化语句、循环条件、更新语句以及更新 s 值的语句。

20. 以下程序段的输出是什么？

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

21. 以下程序段的输出是什么？

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

22. 假设以下代码已正确插入程序中：

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
  (i) 11          (ii) 4          (iii) 26          (iv) 以上都不是

- b. 如果在 for 循环语句的右括号后插入一个分号，s 的最终值是什么？
  (i) 0          (ii) 1          (iii) 2          (iv) 5          (v) 以上都不是

- c. 如果在 for 循环控制表达式中将 5 替换为 0，s 的最终值是什么？
  (i) 0          (ii) 1          (iii) 2          (iv) 以上都不是

23. 指出以下每条语句产生的输出（如果有）：

- a.
  ```cpp
  for (i = 1; i <= 1; i++)
      cout << "*";
  cout << endl;
  ```

- b.
  ```cpp
  for (i = 2; i >= 1; i++)
      cout << "*";
  cout << endl;
  ```

- c.
  ```cpp
  for (i = 1; i <= 1; i--)
      cout << "*";
  cout << endl;
  ```

- d.
  ```cpp
  for (i = 12; i >= 9; i--)
      cout << "*";
  cout << endl;
  ```

- e.
  ```cpp
  for (i = 0; i <= 5; i++)
      cout << "*";
  cout << endl;
  ```

- f.
  ```cpp
  for (i = 1; i <= 5; i++)
  {
      cout << "*";
      i = i + 1;
  }
  cout << endl;
  ```

24. 编写一个 for 语句，将 1 到 100 之间所有 3 的倍数相加。

25. 以下代码的输出是什么？变量 x 和 y 之间是否存在关系？如果存在，请说明该关系。输出是什么？

```cpp
int x = 19683;
int i;
int y = 0;

for (i = x; i >= 1; i = i / 3)
    y++;
cout << "x = " << x << ", y = " << y << endl;
```

26. 假设输入为 5 3 8。以下代码的输出是什么？假设所有变量都已正确声明。

```cpp
cin >> a >> b >> c;
for (j = 1; j < a; j++)
{
    d = b + c;
    b = c;
    c = d;
    cout << c << " ";
}
cout << endl;
```

27. 以下 C++ 程序段的输出是什么？假设所有变量都已正确声明。

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

28. 假设输入为 3 5 7 -6 10。以下代码的输出是什么？

```cpp
int temp = 0;
int num;
int count;
```

- a.
  ```cpp
  x = 5;  y = 50;
  do
      x = x + 10;
  while (x < y);
  cout << x << " " << y << endl;
  ```

- b.
  ```cpp
  x = 5;  y = 80;
  do
      x = x * 2;
  while (x < y);
  cout << x << " " << y << endl;
  ```

- c.
  ```cpp
  x = 5;  y = 20;
  do
      x = x + 2;
  while (x >= y);
  cout << x << " " << y << endl;
  ```

- d.
  ```cpp
  x = 5;  y = 35;
  while (x < y)
      x = x + 10;
  cout << x << " " << y << endl;
  ```

- e.
  ```cpp
  x = 5;  y = 30;
  while (x <= y)
      x = x * 2;
  cout << x << " " << y << endl;
  ```

- f.
  ```cpp
  x = 5;  y = 30;
  while (x > y)
      x = x + 2;
  cout << x << " " << y << endl;
  ```

33. 编写一个输入语句验证循环，提示用户输入一个小于 20 或大于 75 的数。

34. 将以下代码改写为 for 循环：

```cpp
int i = 0, value = 0;

while (i <= 20)
{
    if (i % 2 == 0 && i <= 10)
        value = value + i * i;
    else if (i % 2 == 0 && i > 10)
        value = value + i;
    else
        value = value - i;
    i = i + 1;
}

cout << "value = " << value << endl;
```

这个循环的输出是什么？

35. 将练习 34 中的 while 循环改写为 do...while 循环。

36. 以下程序中的 do...while 循环本应读取一些数字，直到到达哨兵值（在本例中为 -1）。它本应将除哨兵值以外的所有数字相加。如果数据如下所示：

12    5    30    48    -1

该程序未能正确地将这些数字相加。请改正程序，使其能正确相加。

```cpp
#include <iostream>

using namespace std;
int main()
{
    int total = 0,
        count = 0,
        number;
    do
    {
        cin >> number;
        total = total + number;
        count++;
    }
    while (number != -1);

    cout << "The number of data read is " << count << endl;
    cout << "The sum of the numbers entered is " << total
         << endl;

    return 0;
}
```

37. 使用与练习 36 相同的数据，以下循环同样失败。请改正它。

```cpp
cin >> number;
while (number != -1)
    total = total + number;
    cin >> number;
cout << endl;
cout << total << endl;
```

38. 使用与练习 36 相同的数据，以下循环同样失败。请改正它。

```cpp
cin >> number;
while (number != -1)
{
    cin >> number;
    total = total + number;
}
cout << endl;
cout << total << endl;
```

39. 给定以下程序段：

```cpp
for (number = 1; number <= 10; number++)
    cout << setw(3) << number;
```

编写一个 while 循环和一个 do...while 循环，使其具有相同的输出。

