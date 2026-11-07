
- b. 函数调用语句、形参和实参。
- c. 值参数和引用参数。
- d. 局部变量和全局变量。
- e. 命名常量。

```cpp
#include <iostream>                               //Line 1

using namespace std;                              //Line 2

const double RATE = 15.50;                        //Line 3
const char STAR = '*';                            //Line 4

double temp;                                      //Line 5

void func(int, int, double&, char&);              //Line 6

int main()                                        //Line 7
{                                                 //Line 8
    int s = 50;                                   //Line 9
    int t = 6;                                    //Line 10
    double d;                                     //Line 11
    char ch = STAR;                               //Line 12

    func(s, t, d, ch);                            //Line 13
    cout << "d = " << d << ", ch = " << ch << endl; //Line 14
    func(75, 8, d, ch);                           //Line 15
    cout << "d = " << d << ", ch = " << ch << endl; //Line 16

    return 0;                                     //Line 17
}                                                 //Line 18

void func(int speed, int time,                    //Line 19
          double& distance, char& c)              //Line 20
{                                                 //Line 21
    double num;                                   //Line 22

    distance = speed * time;                      //Line 23
    num = static_cast<int>(c);                    //Line 24
    c = static_cast<char>(num + 1);               //Line 25
}                                                 //Line 26
```

这个程序的输出是什么？

- 21.
  - a. 解释实参和形参之间的区别。
    (4, 6, 7, 10)
  - b. 解释值参数和引用参数之间的区别。
  - c. 解释局部变量和全局变量之间的区别。

- 22. 以下程序的输出是什么？(6)

```cpp
#include <iostream>
using namespace std;

void func1();
void func2();

int main()
{
    int num;

    cout << "Enter 1 or 2: ";
    cin >> num;
    cout << endl;

    cout << "Take ";

    if (num == 1)
        func1();
    else if (num == 2)
        func2();
    else
        cout << "Invalid input. You must enter a 1 or 2" << endl;

    return 0;
}

void func1()
{
    cout << "Programming I." << endl;
}

void func2()
{
    cout << "Programming II." << endl;
}
```

- a. 如果输入为 1，输出是什么？
- b. 如果输入为 2，输出是什么？
- c. 如果输入为 3，输出是什么？
- d. 如果输入为 -1，输出是什么？

- 23. 编写一个 void 函数的定义，该函数接收一个整数作为输入，如果该数是偶数，则输出该数的两倍；否则输出该数的五倍。(6, 7, 8)

- 24. 编写一个 void 函数的定义，该函数接收三个十进制数作为输入。该函数返回这三个数的和与平均值。如果平均值大于或等于 70，则返回 "Pass"；否则返回 "Fail"。(6, 7, 8)

- 25. 编写一个 void 函数的定义，该函数具有三个引用参数，类型分别为 int、double 和 string。该函数将 int 和 double 变量的值设置为 0，并将 string 变量的值设置为空字符串。(6, 7, 8)

- 26. 编写一个 void 函数的定义，该函数接收两个整数值，例如 n 和 m。该函数返回 n 和 m 之间（含 n 和 m）所有数的和与平均值。(6, 7, 8)

- 27. 以下程序的输出是什么？(6, 7, 8)

```cpp
#include <iostream>
using namespace std;

void compute(int x, int& y, int& z);

int main()
{
    int one = 7;
    int two = 5;
    int three = 6;

    compute(one, two, three);
    cout << one << ", " << two << ", " << three << endl;

    compute(two, one, three);
    cout << one << ", " << two << ", " << three << endl;

    compute(three, two, one);
    cout << one << ", " << two << ", " << three << endl;

    compute(two, three, one);
    cout << one << ", " << two << ", " << three << endl;

    return 0;
}

void compute(int x, int& y, int& z)
{
    int w = x + y - z;

    y = w % 2;
    x = y + w;
    z = x * y;
}
```

- 28. 以下程序的输出是什么？(6, 7, 8)

```cpp
#include <iostream>
using namespace std;

int temp;

void sunny(int&, int);
void cloudy(int, int&);

int main()
{
    int num1 = 6;
    int num2 = 10;
    temp = 20;

    cout << num1 << " " << num2 << " " << temp << endl;

    sunny(num1, num2);
    cout << num1 << " " << num2 << " " << temp << endl;

    cloudy(num1, num2);
    cout << num1 << " " << num2 << " " << temp << endl;
    return 0;
}

void sunny(int& a, int b)
{
    int w;
    temp = (a + b) / 2;
    w = a / temp;
    b = a + w;
    a = temp - b;
}

void cloudy(int u, int& v)
{
    temp = 2 * u + v;
    v = u;
    u = v - temp;
}
```

- 29. 在以下程序中，给标记的语句编号，以显示它们将执行的顺序（逻辑执行顺序）。另外，如果输入为 10，输出是什么？(6, 7, 8)

```cpp
#include <iostream>

using namespace std;

int secret(int, int);

void func(int x, int& y);

int main()
{
    int num1, num2;

    num1 = 6;
    cout << "Enter a positive integer: ";
    cin >> num2;
    cout << endl;
    cout << secret(num1, num2) << endl;
    num2 = num2 - num1;
    cout << num1 << " " << num2 << endl;
    func(num2, num1);
    cout << num1 << " " << num2 << endl;

    return 0;
}

int secret(int a, int b)
{
    int d;

    d = a + b;
    b = a * d;

    return b;
}

void func(int x, int& y)
{
    int val1, val2;

    val1 = x + y;
    val2 = x * y;
    y = val1 + val2;
    cout << val1 << " " << val2 << endl;
}
```

- 30. 考虑以下程序。(6, 7, 8)

```cpp
#include <iostream>
#include <cmath>
#include <iomanip>

using namespace std;

void trackVar(double& x, double y);

int main()
{
    double one, two;

    cout << fixed << showpoint << setprecision(2);

    cout << "Enter two numbers: ";
    cin >> one >> two;
    cout << endl;

    trackVar(one, two);
    cout << "one = " << one << ", two = " << two << endl;
    trackVar(two, one);
    cout << "one = " << one << ", two = " << two << endl;

    return 0;
}

void trackVar(double& x, double y)
{
    double z;

    z = floor(x) + ceil(y);
    x = x + z;
    y = y - z;

    cout << "z = " << z << ", ";
}
```

- a. 如果输入为 3 5，输出是什么？
- b. 如果输入为 4 11，输出是什么？
- c. 如果输入为 10 10，输出是什么？

- 31. 练习 30 中的函数 trackVar 输出 z 的值。修改该函数的定义，使其不打印 z 的值，而是将其值送回调用环境，并由调用环境打印 z 的值。(6, 7, 8)

- 32. 在练习 30 中，确定每个标识符的作用域。(9)

- 33. 以下代码段的输出是什么？(9)

```cpp
int num1 = 3;
int num2 = 5;

cout << num1 << " " << num2 << endl;

if (num1 + num2 > 7)
{
    int num2 = 12;
    int num3;

    num3 = num2 - num1;
    num1 = num2 * num3;
    num2 = num3 / num1;
    cout << num1 << " " << num2 << endl;
}
cout << num1 << " " << num2 << endl;
```

- 34. 考虑以下程序。它的确切输出是什么？像例 6-14 那样，显示每行执行后变量的值。(6, 7, 8)

```cpp
#include <iostream>                                      //Line 1
using namespace std;                                      //Line 2

void funOne(int& a);                                      //Line 3

int main()                                                //Line 4
{                                                         //Line 5
    int num1, num2;                                       //Line 6

    num1 = 10;                                            //Line 7

    num2 = 20;                                            //Line 8

    cout << "Line 9: In main: num1 = " << num1
         << ", num2 = " << num2 << endl;                //Line 9

    funOne(num1);                                         //Line 10
    cout << "Line 11: In main after funOne: num1 = "
         << num1 << ", num2 = " << num2 << endl;         //Line 11

    return 0;                                             //Line 12
}                                                         //Line 13

void funOne(int& a)                                       //Line 14
{                                                         //Line 15
    int x = 12;                                           //Line 16
    int z;                                                //Line 17

    z = a + x;                                             //Line 18

    cout << "Line 19: In funOne: a = " << a
         << ", x = " << x
         << ", and z = " << z << endl;                   //Line 19

    x = x + 5;                                             //Line 20

    cout << "Line 21: In funOne: a = " << a
         << ", x = " << x
         << ", and z = " << z << endl;                   //Line 21

    a = a + 8;                                             //Line 22

    cout << "Line 23: In funOne: a = " << a
         << ", x = " << x
         << ", and z = " << z << endl;                   //Line 23
}                                                         //Line 24
```

- 35. 以下程序的输出是什么？(11)

```cpp
#include <iostream>
using namespace std;

void trackStaticVar(int& x);
```
