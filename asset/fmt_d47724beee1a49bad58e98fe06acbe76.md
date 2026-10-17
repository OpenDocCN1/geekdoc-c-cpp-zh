
以下哪些语句是有效的？如果无效无效，请解释原因。(4)

- a. `volume = box(length, width, height);`
- b. `volume = box(length, 3.8, height);`
- c. `cout << box(num1, num3, num2) << endl;`
- d. `cout << box(length, width, 7.0) << endl;`
- e. `volume = box(num1, width, height);`
- f. `cout << box(6.2 , height) << endl;`
- g. `volume = box(length + width, height);`
- h. `volume = box(num1, num2 + num3);`

8. 考虑以下函数：(4)

```cpp
int hidden(int num1, int num2)
{
    if (num1 > 20)
        num1 = num2 / 10;
    else if (num2 > 20)
        num2 = num1 / 20;
    else
        return num1;
    return num1 * num2;
}
```

```cpp
int compute(int one, int two)
{
    int secret = one;
    for (int i = one + 1; i <= two; i++)
        secret = secret + i;
    return secret;
}
```

每个每个程序的输出是什么？

- a. `cout << hidden(15, 10) << endl;`
- b. `cout << compute(3, 9) << endl;`
- c. `cout << hidden(30, 20) << " " << compute(10, 20) << endl;`
- d. `x = 2; y = 8; cout << compute(y, x) << endl;`

9. 考虑以下原型：(3, 4)

```cpp
double first(double, double);
int second(char, double, double);
string third(string, int, double);
char grade(double, double);
```

回答以下问题：

- a. `first` 有几个参数？返回值类型是什么？
- b. `second` 有几个参数？返回值类型是什么？
- c. `third` 有几个参数？返回值类型是什么？
- d. `grade` 有几个参数？返回值类型是什么？
- e. 调用 `third` 需要几个实际参数？参数的顺序应该是怎样的？
- f. 写一个 C++ 语句，使用参数 `2.5` 和 `7.8` 调用 `first` 并打印结果。
- g. 写一个 C++ 语句，使用参数 `8.5` 和 `9.5` 调用 `grade` 并打印结果。
- h. 写一个 C++ 语句，打印 `third` 的返回值。

10. 为什么程序中需要函数原型？(5)

11. 定义一个函数，接收一个 `char` 输入，如果字符大于 0 则返回 `true`，否则返回 `false`。(4)

12. 考虑以下函数：(1, 4)

```cpp
double mystery(int x, double y, char ch) {
    if (isupper(ch))
        return(sqrt(x)) + y;
    else
        return(pow(y, 3)) + x;
}
```

以下语句的输出是什么？（假设输出保留两位。）

- a. `cout << mystery(16, 2.0, 'A') << endl;`
- b. `cout << mystery(5, 3.0, '*') << endl;`
- c. `cout << mystery(-7, 2.5, 'T') << endl;`

13. 考虑以下函数：(4)

```cpp
int secret(int m, int n) {
    int temp = n;
    for (int i = 1; i < abs(m); i++) {
        temp = temp + n;
    }
    if (m < 0)
        temp = -temp;
    return temp;
}
```

- a. 以下语句的输出是什么？
  i. `cout << secret(18, 4) << endl;`
  ii. `cout << secret(-10, 20) << endl;`
- b. `secret` 函数的作用是什么？

14. 定义一个函数，接收三个数字。如果前两个数字的积的地 `floor` 等于第三个数字，则返回 `true`。（假设三个数字都是 `double` 类型。）

15. 考虑以下 C++ 程序：(1, 4)

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int main() {
  int temp = 0;
  for (int counter = 1; counter <= 100; counter++) {
    if (pow(floor(sqrt(counter)) / 1.0), 2.0) == counter)
      temp = temp + counter;
  }
  cout << temp << endl;
  return 0;
}
```

- a. 这个程序的输出是什么？
- b. 这个程序是了什么？

16. 以下程序的输出是什么？(4)

```cpp
#include <iostream>
using namespace std;
int mystery(int x, int y, int z);
int main() {
  cout << mystery(4, 18, 12) << endl;
  cout << mystery(6, -3, 45) << endl;
  cout << mystery(-5, 12, -7) << endl;
  cout << mystery(1, 0, 0) << endl;
  cout << mystery(10, 10, 10) << endl;
  return 0;
}
```

```cpp
int mystery(int x, int y, int z)
{
    if (x <= y && x <= z && x != 0)
        return (y + z) / x;
    else if (y <= x && y <= z && y != 0)
        return (z + x) / y;
    else if (z <= x && z <= y && z != 0)
        return (x + y) / z;
    else
        return x + y + z;
}
```

- b. 函数调用语句、形式参数和实际参数。
- c. 值参数和引用参数。
- d. 局部变量和全局变量。
- e. 命名常量。

```cpp
#include <iostream> //Line 1
using namespace std; //Line 2
const double RATE = 15.50; //Line 3
const char STAR = '*'; //Line 4
double temp; //Line 5
void func(int, int, double&, char&); //Line 6
int main() { //Line 7
    int s = 50; //Line 8
    int t = 6; //Line 9
    double d; //Line 10
    char ch = STAR; //Line 11
    func(s, t, d, ch); //Line 12
    cout << "d = " << d << ", ch = " << ch << endl; //Line 13
    func(75, 8, d, ch); //Line 14
    cout << "d = " << d << ", ch = " << ch << endl; //Line 15
    return 0; //Line 17
} //Line 18
void func(int speed, int time, double& distance, char& c) { //Line 19
    double num; //Line 20
    distance = speed * time; //Line 22
    num = static_cast<int>(distance); //Line 23
    c = static_cast<char>(num + 1); //Line 24
} //Line 26
```

该程序的输出是什么？

- 21. a. 解释实际参数和形式参数之间的区别。（4, 6, 7, 10)
- b. 解释值参数和引用参数的区别。
- c. 解释局部变量和全局变量的区别。

## 第 6 章：用户定义函数

22. 下一个程序的输出是什么？

```cpp
#include <iostream>
using namespace std;
void func1();
void func2();
int main() {
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
void func1() {
    cout << "Programming I." << endl;
}
void func2() {
    cout << "Programming II." << endl;
}
```

- a. 如果输入是 1，输出是什么？
- b. 如果输入是 2，输出是什么？
- c. 如果输入是 3，输出是什么？
- d. 如果输入是 -1，输出是什么？

- 23. 编写一个 `void` 函数的定义，该函数接受一个整数作为输入，如果是偶数，则输出该数字的两倍；否则输出该数字五倍。（6, 7, 8)
- 24. 编写一个 `void` 函数的定义，该函数接受小数作为输入。该函数返回三个数的和和平均值。如果平均值大于或等于 70，则返回 "Pass"；否则返回 "Fail"。（6, 7, 8)

编写一个具有三个类型为 `int`、`double` 和 `string` 的引用参数的 `void` 函数定义。该函数将 `int` 和 `double` 变量的值设置为 0，并将 `string` 变量的值设置为空字符串。（6, 7, 8)

编写一个 `void` 函数的定义，该函数接受两个整数值，返回所有数字 `n` 和 `m`（包含边界）的和和平均值。（6, 7, 8)

下一个程序的输出是什么？（6, 7, 8)

```cpp
#include <iostream>
using namespace std;
void compute(int x, int& y, int& z);
int main() {
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
void compute(int x, int& y, int& z) {
    int w = x + y - z;
    y = w % 2;
    x = y + w;
    z = x * y;
}
```

下一个程序的输出是什么？（6, 7, 8)

```cpp
#include <iostream>
using namespace std;
int temp;
void sunny(int&, int);
void cloudy(int, int&);
```

```cpp
int main() {
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
void sunny(int& a, int b) {
    int w;
    temp = (a + b) / 2;
    w = a / temp;
    b = a + w;
    a = temp;
}
void cloudy(int u, int& v) {
    temp = 2 * u + v;
    v = u;
    u = temp;
}
```

29. 在下面的程序中，标记语句以显示它们执行的顺序（逻辑顺序）。如果输入是 10，输出是什么？（6, 7, 8)

```cpp
#include <iostream>
using namespace std;
int secret(int, int&);
void func(int x, int& y);
int main() {
    int num1, num2;
    num1 = 6;
    cout << "Enter a positive integer: ";
    cin >> num2;
    cout << endl;
    cout << secret(num2, num1) << endl;
    func(num1, num2);
    cout << num1 << " " << num2 << endl;
    return 0;
}
int secret(int a, int& b) {
    int d;
    d = a + b;
    b = d - a;
    return d;
}
void func(int x, int& y) {
    int vall, val2;
    vall = x + y;
    val2 = x * y;
    cout << vall << " " << val2 << endl;
}
```

30. 考虑下面的程序。（6, 7, 8)

```cpp
#include <iostream>
#include <cmath>
#include <iomanip>
using namespace std;
void trackVar(double& x, double y);
int main() {
    double one, two;
    cout << fixed << setprecision(2);
    cout << "Enter two numbers: ";
    cin >> one >> two;
    cout << endl;
    trackVar(one, two);
    cout << "one = " << one << " two = " << two << endl;
    return 0;
}
void trackVar(double& x, double y) {
    double z;
    z = floor(x) + ceil(y);
    x = z - y;
    y = z / x;
}
```

- a. 如果输入是 3，输出是什么？
- b. 如果输入是 5，输出是什么？
- c. 如果输入是 10，输出是什么？

- 31. 修改该函数，使其返回 `z` 的值而不是打印它发送到调用环境。
- 32. 在第 30 题中标识符的作用域。（6, 7, 8)
- 33. 下一个代码段的输出是什么？（9)

```cpp
int num1 = 3;
int num2 = 5;
cout << num1 << " " << num2 << endl;
if (num1 < 7) {
    num2 = 12;
    int num3;
    num3 = num2 - num1;
```
