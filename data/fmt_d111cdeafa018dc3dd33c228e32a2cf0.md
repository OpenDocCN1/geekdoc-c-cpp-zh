
`cout << rand() << endl; // 显示 0 到 RAND_MAX 之间的随机整数`

`cout << rand() << endl; // 显示 0 到 RAND_MAX 之间的随机整数`

`cout << rand() << endl; // 显示 0 到 RAND_MAX 之间的随机整数`

`return 0;`

```
```

`time()` 函数定义在 `ctime` 库中。它在 C++ 中无法直接访问，你需要包含 `ctime` 库。如果你想要一个 `minimum` 到 `maximum` 之间的伪随机整数，可以使用以下模式：

`minimum + rand() % (maximum - minimum + 1)`

| project_11_2m |
| `#include <iostream>`
`#include <ctime>`
`#include <cstdlib>`
`using namespace std;`
`int main() {`
`  srand(time(NULL));`
`  cout << 2 + rand() % (10 - 2 + 1) << endl; // 显示 2 到 10 之间的随机整数`
`  cout << 20 + rand() % 6 << endl; // 显示 20 到 25 之间的随机整数`
`  return 0;`
`} |`

## 四舍五入

- `round(number)`

此函数返回 `number` 最接近的整数。

## 示例

| project_11_2n |
| `#include <iostream>`
`#include <cmath>`
`using namespace std;`
`int main() {`
`  double a = 5.9;`
`  cout << round(a) << endl; // 显示: 6`
`  cout << round(5.4) << endl; // 显示: 5`
`  return 0;`
`} |`

> `round()` 函数定义在 `cmath` 库中。它在 C++ 中无法直接访问，你需要包含 `cmath` 库。如果你需要 `number` 到指定精度的四舍五入后的值，可以使用以下公式：

```
round(number * pow(10, precision)) / pow(10, precision)
```

## 示例

| project_11_20 |

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int main() {
    double a, y;
    a = 5.312;
    y = round(a * pow(10, 2)) / pow(10, 2);
    cout << y << endl; // 输出为: 5.31
    a = 5.315;
    y = round(a * pow(10, 2)) / pow(10, 2);
    cout << y << endl; // 输出为: 5.32
    cout << round(2.3447 * pow(10, 3)) / pow(10, 3) << endl; // 输出为: 2.345
    cout << round(2.3447 * 1000) / 1000 << endl; // 输出为: 2.345
    return 0;
}
```

## 平方根

`sqrt(number)`

该函数返回 `number` 的平方根。

## 示例

![](img/6e4b8e11c2f26304087157218fda632f_176_0.png)

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int main() {
    double x, y;
    cout << sqrt(9) << endl; // 输出为: 3
    cout << sqrt(2) << endl; // 输出为: 1.4142
    cout.precision(17);
    cout << sqrt(2) << endl; // 输出为: 1.4142135623730951
    x = sqrt(8); // 赋值 2.828421247461903
    y = round(sqrt(8));
    cout << y << endl; // 输出为: 3
    return 0;
}
```

> 函数 `sqrt()` 定义在库 `cmath` 中。在 C++ 中无法直接访问它，因此你需要包含 `cmath` 库。

`cout.precision(17)` 将语句 `cout` 显示的最大数字位数设置为 17。

注意函数 `sqrt()` 是如何嵌套在函数 `round()` 之中的。内部（嵌套）函数（或多个函数）的结果被用外部函数的参数。这是大多数程序员倾向于遵循的编写风格，因为有助于节省大量的代码行。当然，如果你需要嵌套很多函数，将没有人能读懂你的代码。嵌套最多四层是完全可以的。

## 练习 11.2-1 计算两点之间的距离

编写一个 C++ 程序，提示用户输入两个点的坐标 `(x,y)`，然后计算它们之间的直线距离。所需的公式为：

`d = \sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}`

### 方案解答

在本次练习中，你需要使用函数 `sqrt()`，它返回一个数字的平方根。

为了简化操作，项 `(x_1 - x_2)^2` 和 `(y_1 - y_2)^2` 是分别计算的，并将结果赋值给两个临时变量。这里展示了该 C++ 程序。

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int main() {
    double d, x1, x2, x_temp, y1, y2, y_temp;
    cout << "输入点 A 的坐标:" << endl;
    cin >> x1 >> y1;
    cout << "输入点 B 的坐标:" << endl;
    cin >> x2 >> y2;
    x_temp = pow(x1 - x2, 2);
    y_temp = pow(y1 - y2, 2);
    d = sqrt(x_temp + y_temp);
    cout << "两点间的距离: " << d << endl;
    return 0;
}
```

现在让我们来看另一种方法。

你应该意识到，在函数调用内部执行操作实际上是可能的。这样做，操作的结果将用用作函数的参数。

这里展示了该 C++ 程序。

![](img/6e4b8e11c2f26304087157218fda632f_178_0.png)

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int main() {
    double x1, x2, y1, y2;
    cout << "输入点 A 的坐标:" << endl;
    cin >> x1 >> y1;
    cout << "输入点 B 的坐标:" << endl;
    cin >> x2 >> y2;
    double d = sqrt(pow(x1 - x2, 2) + pow(y1 - y2, 2));
    cout << "两点间的距离: " << d << endl;
    return 0;
}
```

## 练习 11.2-2 汽车行驶了多远？

汽车从静止开始，以恒定加速度沿水平道路行驶一段距离。编写一个 C++ 程序，提示用户输入加速度和行驶距离，并计算行驶时间。所需的公式为 `$S = u_0 + \frac{1}{2}at^2$`

其中：

- `S` 是距离，单位为米 `(m)`
- `u_0` 是初速度，单位为每秒 `(m/s)`
- `a` 是加速度，单位为每秒每秒 `(m/s²)`
- `t` 是时间，单位为秒 `(s)`

### 方案解答

由于汽车从静止开始，因此 `u_0 = 0`。公式简化为 `$S = \frac{1}{2}at^2$`。

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int main() {
    double S, a, t;
    cout << "输入加速度:" << endl;
    cin >> a;
    cout << "输入距离:" << endl;
    cin >> S;
    t = sqrt(2 * S / a);
    cout << "行驶时间: " << t << " 秒" << endl;
    return 0;
}
```

## 11.3 复习判断题

判断以下陈述的对错：

1. `sqrt()` 函数返回负数的平方根。
2. C++ 必须使用迭代 算法。
3. `abs()` 函数返回绝对值。
4. `M_PI` 常数等于 3。
5. `pow(2)` 的结果是 9。
6. `rand()` 函数不能返回负数。
7. `round(3.5)` 赋值给变量 `y`。
8. `sqrt(3.5)` 的结果是 4。
9. 为了计算 90 度的正弦，必须写 `sin(M_PI/2)`。
10. `y = sqrt(-2)` 是有效的。
11. 下列代码片段满足定义：

```cpp
double a, b, x;
cin >> a >> b;
x = sqrt(b);
```

## 11.4 复习选择题

为每个陈述选择一个正确答案：

1. 下列哪项计算变量的平方？
   a. `y = a * a;`
   b. `y = pow(a, 2);`
   c. `y = a / a;`
   d. 以上均对

2. 执行语句 `y = abs(+5.2)` 后，`y` 的值为：
   a. `-5.2`
   b. `5`
   c. `0.2`
   d. `5.2`
3. 下列哪项在 C++ 中计算 180 度的正弦？
   a. `sin(180)`
   b. `sin(M_PI)`
   c. 以上均对
   d. 以上均非

4. 执行语句 `y = (int)(5.0 / 2.0)` 后，`y` 的值为：
   a. `2.5`
   b. `3`
   c. `2`
   d. `0.5`
5. 执行语句 `y = pow(sqrt(4), 2)` 后，`y` 的值为：
   a. `4`
   b. `2`
   c. `8`
   d. `16`
6. 执行语句 `y = round(5.2) / 2.0` 后，`y` 的值为：
   a. `2`
   b. `2.5`
   c. `2.6`
   d. 以上都不是

## 15.5 复习练习

完成以下练习：

1. 创建追踪表以确定 C++ 程序在每次执行步骤中的变量值。两次执行的输入值为：(i) `9`，和 (ii) `4`。

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int main() {
    double a, b, c;
    cin >> a;
    a += 6 / sqrt(a) * 2 + 20.4;
    b = (int)round(a) % 4;
    c = (int)b << 3;
    cout << a << " , " << b << " , " << c << endl;
    return 0;
}
```

2. 创建追踪表以确定 C++ 程序在每次执行步骤中的变量值。两次执行的输入值为：(i)`-2`，和 (ii)`-3`

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int main() {
    int a, b, c;
    cin >> a;
    b = abs(a) % 4 + pow(a, 4);
    c = b % 5;
    cout << b << " , " << c << endl;
    return 0;
}
```

# 第 12 章
复杂的数学表达式

## 12.1 编写复杂的数学表达式

在第 7.2 节中，你学习了所有的算术运算符，但对于如何使用它们以及如何编写复杂的数学表达式并不了解。在本章中，你将学习将数学表达式转换为 C++ 语句有多简单。

- 算术运算符遵循与数学中相同的优先级规则，这意味着先执行乘除法，再执行加减法。此外，当乘除法同时出现在同一个表达式中时，由于两者的优先级相同，这些操作从左到右执行。

## 练习 12.1-1 在 C++ 中表示数学表达式

以下哪些 C++ 语句正确表示了以下数学表达式？

```
x = \frac{1}{10 + z}
```

- i. `x = 1 * 27 / 10 + z;`
- ii. `x = 1 · 27 / (10 + z);`
- iii. `x = 27 / 10 + z;`
- iv. `x = 27 / (10 + z);`
- v. `x = (1 / 10 + z) * 27;`
- vi. `x = 1 / ((10 + z) * 27);`
- vii. `x = 1 / (10 + z) * 27;`
- viii. `X = 1 / (10 + z) / 27;`

### 答案

- 错误。由于乘法和除法在加法之前执行，这等同于 `$x = \frac{1\cdot z}{10} + z$`。
- 错误。使用了星号表示乘法。
- 错误。由于除法在加法之前执行，等同于 `$X = \frac{27}{10} + Z$`。
- iv. **正确**。这等同于 `$X = \frac{27}{10+z}$`。
- v. **错误**。在括号内部，除法在加法之前执行。这等同于 `$x = \left(\frac{1}{10} + z\right) 27$`。
- vi. **错误**。括号优先执行，这等同于 `$x = \frac{1}{(10+z)27}$`。
- vii. **正确**。除法在乘法之前执行（从左到右）。先计算 `\frac{1}{10+z}`，然后将结果乘以 27。
- viii. **错误**。这等同于 `$X = \frac{1}{10+z}27$`。

## 练习 12.1-2 在 C++ 中编写数学表达式

编写一个 C++ 程序来计算数学表达式 `y = 10x - \frac{10-z}{4}`

### 答案

首先，你必须区分数据输入和输出结果。显然，输出结果赋值给 `y`，用户必须输入 `x` 和 `z` 的值。该练习的解法所示。

```cpp
#include <iostream>
using namespace std;
int main() {
    double x, y, z;
    cout << "Enter value for x: ";
    cin >> x;
    cout << "Enter value for z: ";
    cin >> z;
```
```cpp
y = 10 * x - (10 - z) / 4;
    cout << "The result is: " << y << endl;
    return 0;
}
```

## 练习 12.1-3 在 C++ 中编写复杂的数学表达式

编写一个 C++ 程序来计算数学表达式

```
y = \frac{3x^2 + 5x + 2}{7w} - \frac{3+x}{7}
```

### 答案

哎！现在表达式变得更复杂了！事实上，它复杂得多！所以，让我们来看一种不同的方法。核心思想是将复杂的表达式拆分为更小、更简单的表达式，并将子结果赋值给临时变量。最后，你可以用这些临时变量构建原始表达式。

```cpp
#include <iostream>
using namespace std;
int main() {
    double denominator, numerator, temp1, temp2, temp3, w, x, z;
    cout << "Enter value for x: ";
    cin >> x;
    cout << "Enter value for w: ";
    cin >> w;
    cout << "Enter value for z: ";
    cin >> z;
    temp1 = 3 * x * x + 2;
    temp2 = 7 * w;
    numerator = temp1 / temp2;
    temp3 = 3 + x;
    denominator = temp3 / 7;
    y = numerator - denominator;
    cout << "The result is: " << y << endl;
    return 0;
}
```
