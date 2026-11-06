
```cpp
int a = 5;

cout << (double) a << endl;        //outputs: 5.0
cout << (double) 34 << endl;       //outputs: 34.0
cout << (double)-34 << endl;       //outputs: -34.0
cout << a / 2 << endl;             //outputs: 2
cout << (double) a / 2 << endl;    //outputs: 2.5
return 0;
}
```

> **注意：** 在计算机科学中，类型转换是将一种数据类型的变量转换为另一种数据类型的方法。请注意，`(double)` 不是函数。它只是 C++ 中将整数转换为实数的一种方式。

> **注意：** 在 C++ 中，两个整数相除的结果总是整数。因此，在表达式 `a / 2` 中，由于变量 `a` 和数字 `2` 都是整数，结果总是整数。如最后一条语句所示，如果你希望得到实数类型的结果，需要在除法的至少一个操作数前加上 `(double)` 转换运算符。

此外，语句

```cpp
cout << (double) a / 2 << endl;
```

等价于

```cpp
cout << a / (double) 2 << endl;
```

也等价于

```cpp
cout << (double) a / (double) 2 << endl;
```

当然也等价于

```cpp
cout << a / 2.0 << endl;
```

它们都输出值 2.5。

## Pi

```cpp
M_PI
```

它返回 π 的值。它定义在 cmath 库中。

### 示例

```cpp
project_11_2e

#include <iostream>
#include <cmath>
using namespace std;
int main(){
  cout << M_PI << endl;    //outputs: 3.14159
  cout.precision(20);      //Set the maximum number of digits to display
  cout << M_PI << endl;    //outputs: 3.141592653589793116
  return 0;
}
```

> **注意：** 请注意，`M_PI` 是一个常量，而不是函数。这就是为什么不使用括号。
> 
> **注意：** 语句 `cout.precision(20)` 设置语句 `cout` 显示的最大位数。

## 乘方

```cpp
pow( number, exp )
```

它返回 `number` 的 `exp` 次幂的结果。它定义在 `cmath` 库中。

### 示例

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int main() {
  double a, b, c;

  a = 2;
  b = 3;
  cout << pow(a, b) << endl;      //outputs: 8.0

  c = pow(3, 2);
  cout << c << endl;              //outputs: 9.0
  return 0;
}
```

> **注意：** 函数 `pow()` 也可用于计算一个数的平方根。数学中已知 `√x = x^(1/2)`。因此，你可以写 `y = pow(x, 1/2)` 来计算 `x` 的平方根，甚至可以写 `y = pow(x, 1/3)` 来计算 `x` 的立方根，依此类推！

## 随机数

```cpp
rand()
```

它返回一个范围在 0 到 RAND_MAX 之间的伪随机整数，其中 RAND_MAX 是一个至少为 32767 的常量。函数 `rand()` 定义在 `cstdlib` 库中。

### 示例

```cpp
#include <iostream>
#include <cstdlib>
using namespace std;
```

```cpp
cout << sqrt(2) << endl;       //outputs: 1.41421
cout.precision(15);
cout << sqrt(2) << endl;       //outputs: 1.4142135623731
return 0;
}
```

> **记住！** 语句 `cout.precision(15)` 设置语句 `cout` 显示的**最大位数**。

## 正切

```cpp
tan(number)
```

它返回 *数字* 的正切值。*数字* 的值必须以弧度表示。函数 `tan()` 定义在 `cmath` 库中。

### 示例

```cpp
// project_11_2m
#include <iostream>
#include <cmath>
using namespace std;
int main() {
  double a;

  a = tan(10);
  cout << a << endl;       //outputs: 0.648361
  return 0;
}
```

## 练习 11.2-1 *计算两点之间的距离*

编写一个 C++ 程序，提示用户输入两个点的坐标 *(x, y)*，然后计算它们之间的直线距离。所需公式为

\[d = \sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}\]

### 解答

在本练习中，你需要使用两个函数：`pow()` 函数，它返回一个数的乘方结果；以及 `sqrt()` 函数，它返回一个数的平方根。

为简化问题，分别计算 \((x_1 - x_2)^2\) 和 \((y_1 - y_2)^2\) 这两项，并将结果赋给两个临时变量。

C++ 程序如下所示。

```cpp
// project_11_2_1a
#include <iostream>
#include <cmath>
using namespace std;

int main() {
    double d, x1, x2, x_temp, y1, y2, y_temp;

    cout << "Enter coordinates for point A: ";
    cin >> x1;
    cin >> y1;

    cout << "Enter coordinates for point B: ";
    cin >> x2;
    cin >> y2;

    x_temp = pow(x1 - x2, 2);
    y_temp = pow(y1 - y2, 2);

    d = sqrt(x_temp + y_temp);

    cout << "Distance between points: " << d;
    return 0;
}
```

现在来看另一种方法。你应该意识到，实际上可以将一个函数嵌套在另一个函数中。这样做时，嵌套函数的结果被用作外层函数的参数。这是大多数程序员喜欢遵循的编写风格，因为它可以节省大量代码行。当然，如果嵌套太多函数，就没有人能理解你的代码。最多嵌套四层是完全可以接受的。使用嵌套函数的 C++ 程序如下所示。

### project_11_2_1b

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int main() {
    double d, x1, x2, y1, y2;

    cout << "Enter coordinates for point A: ";
    cin >> x1;
    cin >> y1;

    cout << "Enter coordinates for point B: ";
    cin >> x2;
    cin >> y2;

    d = sqrt(pow(x1 - x2, 2) + pow(y1 - y2, 2));

    cout << "Distance between points: " << d;
    return 0;
}
```

## **练习 11.2-2** *汽车行驶了多远？*

*一辆汽车从静止开始，沿直线水平道路以恒定加速度行驶一段给定距离。编写一个 C++ 程序，提示用户输入加速度和汽车行驶的距离，然后计算行驶时间。所需公式为*

$S = u_0 + \frac{1}{2}at^2$

其中

- **S** 是汽车行驶的距离，单位为米 (m)
- **u₀** 是汽车的初速度，单位为米每秒 (m/sec)
- **t** 是汽车行驶的时间，单位为秒 (sec)
- **a** 是加速度，单位为米每二次方秒 (m/sec²)

### **解答**

由于汽车从静止开始，初速度 u₀ 为零。因此，公式变为

$S = \frac{1}{2}at^2$

现在，如果解出时间，最终公式变为

$t = \sqrt{\frac{2S}{a}}$

在 C++ 中，你可以使用 sqrt() 函数，它返回一个数的平方根。

```cpp
// project_11_2_2
#include <iostream>
#include <cmath>
using namespace std;
int main() {
    double S, a, t;

    cout << "Enter acceleration: ";
    cin >> a;
    cout << "Enter distance traveled: ";
    cin >> S;

    t = sqrt(2 * S / a);

    cout << "Your car traveled for " << t << " seconds";
    return 0;
}
```

## 11.3 复习题：判断题

对以下每个陈述选择**正确**或**错误**。

- 1. 一般来说，函数是解决小问题的小型子程序。
- 2. 每个程序都必须使用海伦迭代公式来计算正数的平方根。
- 3. `abs()` 函数返回一个项的绝对位置。
- 4. 语句 `int(3.59)` 返回结果 3.6。
- 5. `M_PI` 常量等于 3.14。
- 6. 语句 `pow(2, 3)` 返回结果 9。
- 7. `rand()` 函数也可以返回负的随机数。
- 8. 语句 `y = rand() % 2` 有 50% 的可能性将值 1 赋给变量 `y`。
- 9. 语句 `round(3.59)` 返回结果 4。
- 10. 要计算 90 度的正弦，你必须写 `y = sin (M_PI / 2)`。
- 11. 语句 `y = sqrt(-2)` 是有效的。
- 12. 以下代码片段满足确定性属性。

    ```cpp
    double a, b, x;

    cin >> a;
    cin >> b;
    x = a * sqrt(b);
    cout << x << endl;
    ```

## 11.4 复习题：选择题

为以下每个陈述选择正确答案。

- 1. 以下哪一项计算变量 `a` 的 2 次幂结果？
  - a. `y = a * a;`
  - b. `y = pow(a, 2);`
  - c. `y = a * a / a * a;`
  - d. 以上所有
- 2. 当执行语句 `y = abs(+5.2)` 时，变量 `y` 的值是什么？
  - a. -5.2
  - b. -5
  - c. 0.2
  - d. 5.2
  - e. 5

