
## 程序输出（示例输入已加粗显示）

```
Enter two numbers and I will divide the first
number by the second number: **12 0**
Sorry, I cannot divide by zero.
```

在程序的运行示例中，调用了 `divide` 函数，将 12 传递给 `arg1` 参数，并将 0 传递给 `arg2` 参数。在 `divide` 函数内部，第 29 行的 `if` 语句执行。因为 `arg2` 等于 0.0，所以第 31 行和 32 行的代码执行。当第 32 行的 `return` 语句执行时，`divide` 函数立即结束。这意味着第 34 行的 `cout` 语句不会执行。程序从 `main` 函数中的第 17 行继续运行。

## 从函数返回值

**概念：函数可以将一个值传回调用该函数的程序部分。**

你已经看到数据可以通过参数变量传递给函数。数据也可以从函数返回，回到调用它的语句。返回值的函数通常被称为*有返回值函数（value-returning functions）*。

你已经见过的 `pow` 函数就是返回值函数的一个例子。这里有一个示例：

```cpp
double x;

x = pow(4.0, 2.0);
```

这段代码的第二行调用了 `pow` 函数，将 4.0 和 2.0 作为参数传递进去。该函数计算 4.0 的 2.0 次幂的值并返回该值。该值（ 16.0）通过 `=` 运算符赋值给变量 `x`。

虽然可以向函数传递多个参数，但它只能返回一个值。将函数想象为具有多个接收数据的通信通道（参数），但只有一个发送数据的通道（返回值）。这在图 6-9 中所示。

**图 6-9** 函数返回一个值

![](img/191adf3284699566e6a7b1008ce9bdb5_363_0.png)

> **注意：** 理论上可以从函数返回多个值，但必须将它们“打包”在一起。

## 图 6-11 函数的参数和返回值

```
total = sum(value1, value2);
```

![](img/191adf3284699566e6a7b1008ce9bdb5_366_0.png)

当你调用一个返回值的函数时，你通常希望对它返回的值进行某些有意义的操作。程序 6-12 显示了将函数的返回值赋值给变量。这是使用返回值的常用方法，但你也可以对它们进行许多其他操作。例如，以下代码显示了一个调用 `sum` 函数的数学表达式：

```cpp
int x = 10, y = 15;

double average;

average = sum(x, y) / 2.0;
```

在最后一条语句中，调用了 `sum` 函数并将 `x` 和 `y` 作为其参数。函数的返回值 25 被除以 2.0。结果 12.5 被赋值给 `average`。这是另一个例子：

```cpp
int x = 10, y = 15;

cout << "The sum is " << sum(x, y) << endl;
```

这段代码将 `sum` 函数的返回值传递给 `cout` 以进行显示。屏幕将显示消息“The sum is 25”。

记住，一个返回值的函数返回的是一个特定类型的值。你可以在任何可以使用同类型普通值的地方使用函数的返回值。这意味着，在任何可以使用 `int` 值的地方，都可以使用返回 `int` 值的函数调用。同样，在任何可以使用 `double` 值的地方，都可以使用返回 `double` 值的函数调用。所有数据类型都是如此的。

让我们来看另一个例子。程序 6-13 计算圆的面积，除了 `main` 函数外，它还有两个函数。其中一个函数是 `square`，它返回传递给它的任何数字的平方。该程序还有一个名为 `getRadius` 的函数，提示用户输入半径。用户输入的值由该函数返回。

### 程序 6-13

```cpp
// 此程序演示了返回值的函数。square 函数在数学语句中被调用。
#include <iostream>
#include <iomanip>
using namespace std;

// 函数原型
double getRadius();
double square(double);

int main() {
    const double PI = 3.14159; // 圆周率常量
    double radius; // 用于存储圆的半径
    double area; // 用于存储圆的面积

    // 设置数值输出格式。
    cout << fixed << show(2);

    // 获取圆的半径。
    cout << "This program calculates the area of a circle.\n";
    radius = getRadius();

    // 计算圆的面积。
    area = PI * square(radius);

    // 显示面积。
    cout << "The area is " << area << endl;
    return 0;
}

/*********************
// getRadius 的定义。
// 此函数要求用户输入圆的
// 半径，并将该数字作为 double 返回。
/*********************
double getRadius() {
    double rad;
    cout << "Enter the radius of the circle: ";
    cin >> rad;
    return rad;
}

/*********************
// square 函数的定义。
// 此函数接受一个 double 参数，并将
// 该参数的平方作为 double 返回。
/*********************
double square(double number) {
    return number * number;
}
```

## 以粗体显示示例输入的程序输出

```
此程序计算圆的面积。
Enter the radius of the circle: **10**
The area is **314.2**
```

首先，查看第 39 行到 46 行定义的 `getRadius` 函数。该函数的目的是提示用户输入圆的半径。在第 41 行，该函数定义了一个局部变量 `rad`。第 43 行和 44 行提示用户输入圆的半径，该半径存储在 `rad` 变量中。在第 45 行，返回 `rad` 的值。在 `main` 函数的第 23 行中调用了 `getRadius` 函数。从函数返回的值赋值给 `radius` 变量。

接下来，查看在第 54 行到 57 行定义的 `square` 函数。当调用该函数时，会向它传递一个 `double` 参数。函数将该参数存储在 `number` 参数中。第 56 行的 `return` 语句返回表达式 `number * number` 的值，即参数 `number` 的平方。在 `main` 函数的第 26 行中调用了 `square` 函数，并将 `radius` 的值作为参数传递。该函数将返回 `radius` 变量的平方，该值将用于数学表达式。

假设用户输入 10 作为半径，且此值作为参数传递给 `square` 函数，则 `square` 函数将返回值 100。图 6-12 展示了值 100 是如何传回第 26 行的数学表达式的。值 100 将用于该数学表达式。

## 图 6-12 square 函数

![](img/191adf3284699566e6a7b1008ce9bdb5_368_0.png)

函数可以返回任何类型的值。程序 6-12 显示了返回值的函数。`getRadius` 和 `square` 函数返回 `double`。

## 聚光灯：使用函数

你的朋友经营着餐饮公司。他的食谱是以杯（cups）衡量的。当他去商店时，他们只按盎司（ounce）出售。他要求你写一个将杯转换为盎司的程序。

你设计了以下算法：
- 显示说明程序功能的屏幕。
- 获取杯数。
- 将杯转换为盎司并显示结果。

图 6-13 显示了程序如何分解为函数。

### 图 6-13 程序的层次图

![](img/191adf3284699566e6a7b1008ce9bdb5_368_1.png)

如层次图所示，`main` 函数将调用其他函数。以下是这些函数的摘要：
- `showIntro`: 此函数显示说明屏幕。
- `getCups`: 此函数提示用户输入杯数，并将该值作为 double 返回。
- `cupsToOunces`: 此函数接受杯数作为参数，并将等量的盎司数作为 double 返回。

### 程序 6-14

```cpp
// 此程序将杯转换为盎司。

#include <iostream>
#include <iomanip>

using namespace std;

// 函数原型
void showIntro();
double getCups();
double cupsToOunces(double);

int main() {
    // 杯和盎司的变量。
    double cups, ounces;

    // 设置数值输出格式。
    cout << fixed << setprecision(1);

    // 显示介绍。
    showIntro();

    // 获取杯数。
    cups = getCups();

    // 将杯转换为盎司。
    ounces = cupsToOunces(cups);

    // 显示盎司数。
    cout << cups << " cups equals " << ounces << " ounces.\n";

    return 0;
}

/*********************
// showIntro 函数显示一个介绍屏幕。
*********************
void showIntro() {
    cout << "This program converts measurements\n"
         << "in cups to fluid ounces. For your in\n"
         << "reference the formula is:\n"
         << "1 cup = 8 fluid ounces\n\n";
}

/*********************
// getCups 函数提示用户输入杯数，
// 并将该值作为 double 返回。
*********************
double getCups() {
    double numCps;
    cout << "Enter the number of cups: ";
    cin >> numCps;
    return numCps;
}

/*********************
// cupsToOunces 函数接受杯数作为参数，
// 并将等量的盎司数作为 double 返回。
*********************
double cupsToOunces(double numCps) {
    return numCps * 8.0;
}
```

### 程序输出（示例输入已加粗显示）

```
此程序将杯的测量转换为液体盎司。供你参考的公式如下：
  1 杯 = 8 盎司
Enter the number of cups: **2** [回车]
2.0 杯等于 16.0 盎司。
```

## 返回布尔值

> **概念：** 函数可以返回 true 或 false 值。

通常，需要一个函数来测试参数并返回一个 true 或 false 值，以指示条件是否存在。这样的函数将返回一个 bool 值。例如，以下函数接受一个 int 参数，如果该参数在 1 到 100 之间，则返回 true，否则返回 false：

```cpp
bool isValid(int number) {
    bool status;

    if (number >= 1 && number <= 100)
        status = true;
    else
        status = false;

    return status;
}
```

以下代码显示了一个使用函数调用的 if/else 语句：

```cpp
int value = 20;

if (isValid(value))
    cout << "The value is within range.";
else
    cout << "The value is out of range.";
```

这段代码执行时，将显示消息 "The value is within range."。

程序 6-15 显示了另一个示例。该程序有一个名为 `isEven` 的函数，如果其参数是偶数，该函数返回 true。否则，函数返回 false。

### 程序 6-15

```cpp
// 此程序使用一个返回 true 或 false 的函数。

#include <iostream>

using namespace std;

// 函数原型
bool isEven(int);

int main() {
    int val;

    // 从用户处获取数字。
    cout << "Enter an integer and I will tell you ";
    cout << "if it is even or odd: ";
    cin >> val;

    // 指明它是偶数还是奇数。
    if (isEven(val))
        cout << val << " is even.";
    else
        cout << val << " is odd.";

    return 0;
}

/************************************************************
// 函数 isEven 的定义。此函数接受一个
// 整数参数并测试它是偶数还是奇数。如果参数
// 是偶数，该函数返回 true；如果参数是
// 奇数，返回 false。返回值为 bool。
************************************************************
bool isEven(int number) {
    bool status;
    if (number % 2 == 0)
        status = true; // 如果没有余数，则数字为偶数。
    else
        status = false; // 否则，数字为奇数。

    return status;
}
```

### 程序输出（示例输入已加粗显示）

```
Enter an integer and I will tell you if it is even or odd: **5** [回车]
5 is odd.
```

`isEven` 函数在第 18 行的以下语句中调用：
`if (isEven(val))`

当 if 语句执行时，`isEven` 被调用并传入 val。如果 val 是偶数，`isEven` 返回 true；否则，返回 false。

## 检查点

- 6.11 一个函数可以有多少个返回值？
- 6.12 为一个名为 `distance` 的函数编写头。该函数应返回一个 double 并有两个 double 参数：rate 和 time。
- 6.13 为一个名为 `days` 的函数编写头。该函数应返回 int 并有三个 int 参数：years, months 和 weeks。
- 6.14 为一个名为 `getKey` 的函数编写头。该函数应返回一个 char 且不使用参数。
- 6.15 为一个名为 `lightYears` 的函数编写头。该函数应返回 long 并有一个 long 参数：miles。

## 局部变量与全局变量

> **概念：** 局部变量定义在函数内部，在函数外部不可访问。全局变量定义在所有函数之外，在其作用范围内的所有函数都可以访问。

### 局部变量

定义在函数内部的变量是该函数的局部变量。它们对其他函数隐藏，其他函数通常无法访问它们。程序 6-16 显示，因为定义在函数中的变量是隐藏的，其他函数可以具有相同名称的不同变量。

### 程序 6-16

```cpp
// 此程序显示定义在函数中的变量
// 对其他函数隐藏的。

#include <iostream>

using namespace std;

void anotherFunction(); // 函数原型

int main() {
```
