
16. 以下程序的输出是什么？

```cpp
#include <iostream>

using namespace std;

int mystery(int x, int y, int z);

int main()
{
    cout << mystery(7, 8, 3) << endl;
    cout << mystery(10, 5, 30) << endl;
    cout << mystery(9, 12, 11) << endl;
    cout << mystery(5, 5, 8) << endl;
    cout << mystery(10, 10, 10) << endl;

    return 0;
}

int mystery(int x, int y, int z)
{
    if (x <= y && x <= z)
        return (y + z - x);
    else if (y <= z && y <= x)
        return (z + x - y);
    else
        return (x + y - z);
}
```

17. 编写一个函数的定义，该函数接受三个十进制数作为输入，并返回第一个数乘以第二个数的第三个数次方。

18. 考虑以下 C++ 函数：

```cpp
int mystery(int num)
{
    int y = 1;

    if (num == 0)
        return 1;
    else if (num < 0)
        return -1;
    else
        for (int count = 1; count < num; count++)
            y = y * (num - count);

    return y;
}
```

以下语句的输出是什么？

- a. `cout << mystery(6) << endl;`
- b. `cout << mystery(0) << endl;`
- c. `cout << mystery(-5) << endl;`
- d. `cout << mystery(10) << endl;`

19.

- a. 你如何在 void 函数中使用 return 语句？
- b. 为什么你想在 void 函数中使用 return 语句？

20. 在下面所示的程序代码中，识别以下项目：

- a. 函数原型、函数头、函数体和函数定义。
- b. 函数调用语句、形式参数和实际参数。
- c. 值参数和引用参数。
- d. 局部变量和全局变量。
- e. 命名常量。

```cpp
#include <iostream>                                      //Line 1

using namespace std;                                     //Line 2

const double NUM = 3.5;                                  //Line 3

int temp;                                                //Line 4

void func(int, double&, char);                           //Line 5

int main()                                               //Line 6
{                                                        //Line 7
    int num;                                             //Line 8
    double one;                                          //Line 9
    char ch;                                             //Line 10

    func(num, one, ch);                                  //Line 11
    cout << num << " " << one << " " << ch << endl;      //Line 12
    func(16, 9, '?');                                    //Line 13
    cout << num << " " << one << " " << ch << endl;      //Line 14

    return 0;                                             //Line 15
}                                                        //Line 16

void func(int first, double& second, char ch)             //Line 17
{                                                        //Line 18
    int num;                                             //Line 19
    double y;                                            //Line 20
    int u;                                               //Line 21

    num = 2 * first;                                     //Line 22
    y = second * first;                                  //Line 23
    u = static_cast<int>(ch);                            //Line 24
    second = num + y * u;                                //Line 25
}                                                        //Line 26
```

21.

- a. 解释实际参数和形式参数之间的区别。
- b. 解释值参数和引用参数之间的区别。
- c. 解释局部变量和全局变量之间的区别。

22. 以下程序的输出是什么？

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

- a. 如果输入是 1，输出是什么？
- b. 如果输入是 2，输出是什么？
- c. 如果输入是 3，输出是什么？
- d. 如果输入是 −1，输出是什么？

23. 编写一个 void 函数的定义，该函数接受一个十进制数作为输入，并输出该十进制数数值的 3 倍。将输出格式化为保留两位小数。

24. 编写一个 void 函数的定义，该函数接受两个十进制数作为输入。如果第一个数不为零，它输出第二个数除以第一个数的结果；否则，它输出一条消息，指示第二个数不能被第一个数除，因为第一个数是 0。

25. 编写一个 void 函数的定义，该函数具有三个引用参数，类型分别为 int、double 和 string。该函数将 int 和 double 变量的值设置为 0，并将 string 变量的值设置为空字符串。

26. 编写一个 void 函数的定义，该函数接受两个 int 类型的参数，比如 sum 和 testScore。该函数通过加上 testScore 的值来更新 sum 的值。sum 的新值会在调用环境中体现。

27. 以下程序的输出是什么：

```cpp
#include <iostream>
using namespace std;

void find(int a, int& b, int& c);

int main()
{
    int one, two, three;

    one = 5;
    two = 10;
    three = 15;

    find(one, two, three);
    cout << one << ", " << two << ", " << three << endl;

    find(two, one, three);
    cout << one << ", " << two << ", " << three << endl;

    find(three, two, one);
    cout << one << ", " << two << ", " << three << endl;

    find(two, three, one);
    cout << one << ", " << two << ", " << three << endl;

    return 0;
}

void find(int a, int& b, int& c)
{
    int temp;

    c = a + b;
    temp = a;
    a = b;
    b = 2 * temp;
}
```

28. 以下程序的输出是什么？

```cpp
#include <iostream>
using namespace std;

int x;

void summer(int&, int);
void fall(int, int&);

int main()
{
    int intNum1 = 2;
    int intNum2 = 5;
    x = 6;

    summer(intNum1, intNum2);
    cout << intNum1 << " " << intNum2 << " " << x << endl;

    fall(intNum1, intNum2);
    cout << intNum1 << " " << intNum2 << " " << x << endl;
    return 0;
}

void summer(int& a, int b)
{
    int intNum1;
    intNum1 = b + 12;
    a = 2 * b + 5;
    b = intNum1 + 4;
}

void fall(int u, int& v)
{
    int intNum2;
    intNum2 = x;
    v = intNum2 * 4;
    x = u - v;
}
```

29. 在以下程序中，给标注的语句编号以显示它们将执行的顺序（执行的逻辑顺序）。另外，如果输入是 10，输出是什么？

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

void func (int x, int& y)
{
    int val1, val2;

    val1 = x + y;
    val2 = x * y;
    y = val1 + val2;
    cout << val1 << " " << val2 << endl;
}
```

30. 考虑以下程序：

```cpp
#include <iostream>
#include <cmath>
#include <iomanip>

using namespace std;

void traceMe(double x, double y);

int main()
{
    double one, two;

    cout << "Enter two numbers: ";
    cin >> one >> two;
    cout << endl;
```

