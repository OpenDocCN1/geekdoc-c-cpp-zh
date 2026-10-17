
# 显示 12 全局具名常量（部分2，共2部分）

## 对话示例

Enter a radius to use for both a circle
and a sphere (in inches): 2

Radius = 2 inches

Area of circle = 12.5664 square inches
Volume of sphere = 33.5103 cubic inches

## 值传递：形参数是局部变量

由于形参数对于所有函数定义都是可见的（此处注：显示 13中的程序是豌豆地实验程序）。

Radius = 2 inches

Area of circle = 12.5664 square inches
Volume of sphere = 33.5103 cubic inches

# 显示 13 作为局部变量的形参数（部分1，共2部分）

```cpp
// 计费程序。

#include <iostream>

using namespace std;

const double RATE = 150.00; // 每小时美元。

double fee(int hours_worked, int minutes_worked);

// 返回 hours_worked 小时 minutes_worked 分的法律费用。

int main() {

    int hours, minutes;

double bill;
```

# 显示 13 作为局部变量的形参数（部分2，共2部分）

```cpp
    cout << "Welcome to the offices of\n"
      << "Dewey, Cheatham, and Howe.\n"
      << "The law office with a heart.\n"
      << "Enter the hours and minutes\n"
      << "of your consultation:\n";
    cin >> hours >> minutes;

    bill = fee(hours, minutes);

    cout.set(ios::fixed);

    cout.set(ios::showpoint);

    cout.precision(2);

    cout << "For " << hours << " hours and " << minutes
         << " minutes, your bill is $" << bill << endl;

    return 0;

}

double fee(int hours_worked, int minutes_worked)

{

    int quarter_hours;

    minutes_worked = hours_worked * 60 + minutes_worked;

    quarter_hours = minutes_worked/15;

    return (quarter_hours * RATE);

}
```

> `minutes` 的值不会由于调用 `fee` 而改变。

> `minutes_worked` 是一个初始化为 `minutes` 的局部变量。

## 对话示例

Welcome to the offices of
Dewey, Cheatham, and Howe.
The law office with a heart.
Enter the hours and minutes of your consultation:
2 45
For 2 hours and 45 minutes, your bill is $1650.00

注意函数定义中的形参数 `minutes_worked`。它被用作变量使用并且其值在函数定义内的如下行被改变：

```
minutes_worked = hours_worked * 60 + minutes_worked;
```

与 Dewey、Cheatham 和 Howe 律师事务所不按不足一小时的时间收费。如果他们工作 1 小时 14 分钟，他们只收取 4 个小时的费用，所以你将支付 600 美。这就是“传入形参数”的精确含义。形参数与你在函数体内部声明的变量一样都是局部变量。然而，你不应该为形参数添加一个变量形参数声明。

# 过程抽象与返回值的函数

这是对形式参数的声明。在函数声明中列出形式参数 `minutes_worked` 也充当了变量声明。以下是定义 `fee` 函数的错误方式，因为它声明了两次 `minutes_worked`：

```cpp
double fee(int hours_worked, int minutes_worked) {
    int quarter_hours;
    int minutes_worked;
}
```

![](img/e625ad4e2abbedaa387b8aa67d62ec3a_227_0.png)

# 块作用域

局部变量的作用域是指程序中可以直接访问该变量的部分，有时被称为局部作用域。同样，在程序开头声明的标识符（即所有函数体的作用域）有时被称为具有全局作用域。尽管它们有所不同，但局部和全局标识符实际上都是块作用域的示例。块（block）是用花括号括起来某些 C++ 代码，但全局块”除外，全局块是一个隐含的最外层块，包含了从定义点开始到该块结束的所有代码。块通常是嵌套的。例如，`main` 函数的花括号定义了一个块，而 `main` 内部的循环定义了一个嵌套块。

显示 14 中的程序并没有计算任何有趣的内容，但展示了不同块中声明的标识符的作用域。在这个示例中，常量 `GLOBAL_CONST` 具有全局作用域，函数 `function1` 和 `main` 也是，因为它们是在所有函数体之外声明的。这允许我们从 `main` 和 `function1` 访问 `GLOBAL_CONST`。

`main` 函数声明了局部变量 `x` 和 `d`。它们的作用域延伸到 `main` 块的结束。同样，函数 `function1` 有一个参数 `d` 和局部变量 `y`，它们的作用域延伸到 `function1` 的结束。这两个变量都无法从其作用域外部直接访问。局部变量和参数的作用域实际上使用了相同的块作用域规则，但在这种情况下，块指的是声明变量所属的函数。

显示 14 中的循环说明了嵌套块的作用域。变量在循环内部声明，然后作用域仅延伸到循环块的结束。尝试在作用域之外的地方引用它，即使我们仍在 `main` 内部（例如第 17 行），也会导致编译错误。

你可以将变量理解为在作用域开始时创建，在作用域结束时销毁。例如，每调用一次 `function1`，显示 14 中的局部变量 `y` 就会创建并初始化为 `GLOBAL_CONST`。如果第 23 行的代码更改存储在 `y` 中的值，那么这些更改将在函数退出且 `y` 超出范围时丢失，因为变量 `y` 被销毁了。重复调用 `function1` 不会记得之前的 `y`，而是创建一个新的 `y`。

# 显示 14 局部、全局和块作用域

## 复习块作用域

```cpp
#include <iostream>

using namespace std;

const double GLOBAL_CONST = 1.0;

int function1(int param);

int main() {
    int x;
    double d = GLOBAL_CONST;
    for (int i = 0; i < 10; i++) {
        x = function1(i);
    }
    return 0;
}
```

局部作用域和全局作用域是块作用域的示例。
变量只能在其作用域内被直接访问。

- `main` 的局部作用域：变量 `x` 的作用域是第 20-25 行，变量 `d` 的作用域是第 11-18 行
- 全局作用域：常量 `GLOBAL_CONST` 的作用域是第 4-25 行，函数 `function1` 的作用域是第 6-25 行
- 块作用域：变量 `i` 的作用域是第 13-16 行
- `function1` 的局部作用域：变量 `param` 的作用域是第 20-25 行，变量 `y` 的作用域是第 22-25 行

C++ 还定义了函数作用域和类作用域，后者指的是函数原型中参数的作用域。最后，C++ 支持函数作用域，用于 `goto` 语句。标签是 C 语言的遗留，通常被避免，因为它们会导致逻辑难以追踪，而相同的任务可以通过易于理解的循环完成。

# 复习命名空间

因此，我们所有的程序都以以下两行开头：

```cpp
#include <iostream>

using namespace std;
```

# 过程抽象与返回值的函数

然而，文件的开头并不总是 `using namespace std;` 的最佳位置。事实上，我们可能在不同的函数定义中使用不同的命名空间，使用比仅仅 `std` 更多的命名空间。如果你将指令 `using namespace std;` 放在函数定义开始的花括号 `{` 内部，该指令仅适用于该函数。这允许你在不同的函数定义中使用两个命名空间，即使这两个函数定义在同一个文件中，即使它们有不同的含义。

在函数定义内部放置指令等同于在函数定义内部声明变量，该变量对于函数是局部的。换句话说，如果你在函数定义内部放置指令，该指令对于函数是局部的。在使用任何命名空间之前，良好的做法是将指令放在它们应该所在的地方。显示 15 中的程序行为将与显示 12 完全相同。在这种情况下，差异仅在于风格，但当你开始使用命名空间时，这种差异将影响你的程序的执行。

# 显示 15 使用命名空间（部分 1/2）

```cpp
// 计算圆的面积和球的体积。两个计算使用相同的半径。

#include <iostream>

#include <cmath>

const double PI = 3.14159;

double area(double radius);

// 返回指定半径的圆的面积。

double volume(double radius);

// 返回指定半径的球的体积。
```

（续）

# 显示 15 使用命名空间（部分 2/2）

```cpp
int main() {
    using namespace std;
    double radius_of_both, area_of_circle, volume_sphere;
    cout << "输入圆和球的半径（英寸）: ";
    cin >> radius_of_both;
    area_of_circle = area(radius_of_both);
    volume_sphere = volume(radius_of_both);
    cout << "半径 = " << radius_of_both << " 英寸" << endl;
    cout << "圆面积 = " << area_of_circle << " 平方英寸" << endl;
    cout << "球的体积 = " << volume_sphere << " 立方英寸" << endl;
    return 0;
}

double area(double radius) {
    return (PI * pow(radius, 2));
}

double volume(double radius) {
    return ((4.0/3.0) * PI * pow(radius, 3));
}
```

该程序的示例对话与显示 12 中的程序相同。

## 自测练习

20. 如果你在函数定义中使用变量，你应该在哪里声明该变量？在函数定义中？在程序的 main 部分？任何方便的地方？

![](img/e625ad4e2abbedaa387b8aa67d62ec3a_230_0.png)

21. 假设名为 `Function1` 的函数在其定义中声明了变量 `sam`，名为 `Function2` 的函数在其定义中也声明了名为 `sam` 的变量。程序会编译吗（假设一切正确）？如果编译通过，它可以运行吗（假设一切正确）？如果运行，运行时会生成错误信息吗（假设一切正确）？如果运行且没有错误，会给出正确输出吗（假设一切正确）？

22. 下述函数应该以英尺和英寸表示长度作为参数，并返回相应英尺和英寸的总英寸数。例如，`total_inches(1,2)` 应该返回 14，因为 1 英尺 2 英寸等于 14 英寸。该函数执行得正确吗？如果不正确，为什么？

```cpp
double total_inches(int feet, int inches) {
    inches = 12 * feet + inches;
    return inches;
}
```

23. 为名为 `read_filter` 的函数编写声明和定义，该函数没有参数并返回 `double` 类型的值。`read_filter` 提示用户输入一个 `double` 类型的值并将其读入局部变量。如果该值大于等于零，函数返回提供的值；如果读取的值为负，则返回零。

# 编程示例 阶乘函数

显示 16 包含了常用数学函数——阶乘函数的声明和定义。在数学文本中，阶乘通常写为 `n!`，定义为从 1 到 n 所有整数的乘积。在传统的数学符号中，你可以这样定义 `n!`：

```
n! = 1 * 2 * 3 x ... x n
```

在函数定义中，我们使用 `while` 循环执行乘法。注意，乘法的顺序与你预期的相反。程序先乘以 `n`，然后是 `n-1`，然后是 `n-2`，以此此类推。

# 过程抽象与返回值的函数

## 显示 16 阶乘函数

函数声明

```cpp
int factorial(int n);
//返回 n 的阶乘。
//参数 n 应该是非负数。
```

函数定义

```cpp
int factorial(int n)
{
    int product = 1;
    while (n > 0)
    {
```
