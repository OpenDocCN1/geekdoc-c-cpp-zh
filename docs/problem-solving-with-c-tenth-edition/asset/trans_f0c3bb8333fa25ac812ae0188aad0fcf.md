

# 显示 4.12 全局命名常量（第 1 部分，共 2 部分）

```
//Computes the area of a circle and the volume of a sphere.
//Uses the same radius for both calculations.
#include <iostream>
#include <cmath>
using namespace std;

const double PI = 3.14159;

double area (double radius);
//Returns the area of a circle with the specified radius.

double volume(double radius);
//Returns the volume of a sphere with the specified radius.

int main()
{
    double radiusOfBoth, areaOfCircle, volumeOfSphere;

    cout << "Enter a radius to use for both a circle\n"
         << "and a sphere (in inches): ";
    cin >> radiusOfBoth;

    areaOfCircle = area(radiusOfBoth);
    volumeOfSphere = volume(radiusOfBoth);

    cout << "Radius = " << radiusOfBoth << " inches\n"
         << "Area of circle = " << areaOfCircle
         << " square inches\n"
         << "Volume of sphere = " << volumeOfSphere
         << " cubic inches\n";

    return 0;
}

double area(double radius)
{
    return (PI * pow(radius, 2));
}

double volume(double radius)
{
    return ((4.0/3.0) * PI * pow(radius, 3));
}
```

# 显示 4.12 全局命名常量（第 2 部分，共 2 部分）

## 示例对话

```
Enter a radius to use for both a circle
and a sphere (in inches): 2
Radius = 2 inches
Area of circle = 12.5664 square inches
Volume of sphere = 33.5103 cubic inches
```

以及具有该半径的球体的体积。编写该程序的程序员查阅了计算这些量的公式，并找到如下公式：

```
area = π x (radius)²
volume = (4/3) x π x (radius)³
```

这两个公式都包含常量 π，它约等于 3.14159。符号 π 是希腊字母，读作“pi”。在之前的程序中，我们使用以下声明来生成一个名为 PI 的命名常量，以便在将这些公式转换为 C++ 代码时使用：

```
const double PI = 3.14159;
```

在显示 4.12 的程序中，我们使用了相同的声明，但将其放在文件开头附近，这样它就定义了一个全局命名常量，可在所有函数体中使用。

编译器在全局命名常量声明的位置方面给了你很大的自由度，但为了便于阅读，你应该将所有 `#include` 指令放在一起，将所有全局命名常量声明放在另一组，并将所有函数声明放在一起。我们将遵循标准做法，将所有全局命名常量声明放在 `#include` 指令之后、函数声明之前。

将所有命名常量声明放在程序开头有助于提高可读性，即使该命名常量只被一个函数使用。如果命名常量在程序的未来版本中可能需要更改，那么将其放在程序开头会更容易找到。例如，将销售税率常量声明放在会计程序的开头，可以在税率上调时轻松修改程序。

也可以不使用 `const` 修饰符，将普通变量声明为全局变量，这些变量对文件中的所有函数定义都是可见的。其声明方式与全局命名常量相同，只是变量声明中不使用 `const` 修饰符。然而，还有

![](img/88b1f375f11336dbd9dac8b1675d0698_257_0.png)

# 显示 4.13 形式参数用作局部变量（第 2 部分，共 2 部分）

```
16    cout << "Welcome to the offices of\n"
17        << "Dewey, Cheatham, and Howe.\n"
18        << "The law office with a heart.\n"
19        << "Enter the hours and minutes"
20        << " of your consultation:\n";
21    cin >> hours >> minutes;
22
23    bill = fee(hours, minutes);
24
25    cout.setf(ios::fixed);
26    cout.setf(ios::showpoint);
27    cout.precision(2);
28    cout << "For " << hours << " hours and " << minutes
29        << " minutes, your bill is $" << bill << endl;
30
31    return 0;
32 }
33
34 double fee(int hoursWorked, int minutesWorked)
35 {
36     int quarterHours;
37
38     minutesWorked = hoursWorked * 60 + minutesWorked;
39     quarterHours = minutesWorked/15;
40     return (quarterHours * RATE);
41 }
```

`minutes` 的值不会因调用 `fee` 而改变。

`minutesWorked` 是一个局部变量，初始化为 `minutes` 的值。

## 示例对话

```
Welcome to the offices of
Dewey, Cheatham, and Howe.
The law office with a heart.
Enter the hours and minutes of your consultation:
2 45
For 2 hours and 45 minutes, your bill is $1650.00
```

请注意函数 `fee` 定义中的形式参数 `minutesWorked`。它被用作一个变量，其值会被函数定义中的下面这行代码改变：

```
minutesWorked = hoursWorked * 60 + minutesWorked;
```

形式参数就像你在函数体内声明的变量一样，是局部变量。但是，你不应该为形式参数添加变量声明。在函数声明中列出形式参数 `minutesWorked` 也充当变量声明。

不要为形式参数添加声明

下面是以错误方式开始函数 `fee` 的定义，因为它将 `minutesWorked` 声明了两次：

```
double fee(int hoursWorked, int minutesWorked)
{
    int quarterHours;
    int minutesWorked;
    ...
}
```

切勿这样做！

# 块作用域

局部变量的作用域是指程序中能够直接访问该变量的部分，有时也称为局部作用域。类似地，在程序开头、所有函数体外声明的全局标识符有时被称为具有全局作用域。尽管存在差异，局部标识符和全局标识符实际上都是第 3 章所述的块作用域的实例。块是一些用花括号括起来的 C++ 代码，但“全局块”除外，它是一个隐含的最外层块，包含所有代码。作用域规则规定，在其块内声明的标识符对于该块是局部的，并且只能从其定义点到其块末尾访问。块通常是嵌套的。例如，`main` 函数的花括号定义了一个块，而 `main` 内部的 `for` 循环则定义了一个嵌套块。

显示 4.14 中概述的程序不会计算任何有趣的内容，但说明了在不同块中声明的标识符的作用域。在该示例中，常量 `GLOBAL_CONST` 具有全局作用域，函数 `function1` 和 `main` 本身也具有全局作用域，因为它们是在所有函数体外声明的。这使我们能够从 `main` 和 `function1` 中访问 `GLOBAL_CONST`。

`main` 函数声明了局部于 `main` 的变量 `x` 和 `d`，它们的作用域扩展到 `main` 块的末尾。类似地，函数 `function1` 有一个参数 `param` 和一个局部变量 `y`，它们的作用域扩展到 `function1` 的末尾。这两个变量都不能从其作用域之外直接访问。局部变量和参数的作用域实际上使用相同的块作用域规则，但在这种情况下，块指的是声明变量或参数的函数。

显示 4.14 中的 `for` 循环说明了嵌套块的作用域。变量 `i` 在 `for` 循环内声明，因此其作用域仅限于循环块的末尾。在其作用域之外的任何地方引用 `i`（即使我们仍在 `main` 内部，例如在第 17 行）都会导致编译器错误。

你可以将变量视为在其作用域开始时被创建，在其作用域结束时被销毁。例如，显示 4.14 中的局部变量 `y` 在每次调用 `function1` 时被创建并初始化为 `GLOBAL_CONST`。如果第 23 行的代码改变了存储在 `y` 中的值，那么当函数退出且 `y` 超出作用域时，这些更改将丢失，因为变量 `y` 被销毁了。重复调用 `function1` 不会恢复 `y` 之前的值，而是会创建一个新的 `y`。

除了块作用域之外，还有命名空间作用域和类作用域。类作用域将在第 10 章讨论，命名空间作用域将在第 12 章讨论。C++ 还定义了函数原型作用域，它指的是函数原型中定义的参数所在行的作用域。最后，C++ 支持函数作用域，它用于标签。标签是 C 语言的遗留物，用于 `goto` 语句。它们的用法通常被避免，因为这可能导致难以理解的逻辑，而同样的任务可以通过循环以可理解的方式完成。

# 再论命名空间

到目前为止，我们所有的程序都由以下两行开头：

```
#include <iostream>
using namespace std;
```

# 显示 4.14 局部、全局和块作用域

## 块作用域再探

```
1   #include <iostream>
2   using namespace std;
3
4   const double GLOBAL_CONST = 1.0;
5
6   int function1(int param);
7
8   int main()
9   {
10      int x;
11      double d = GLOBAL_CONST;
12
13      for (int i = 0; i < 10; i++)
14      {
15          x = function1(i);
16      }
17      return 0;
18  }
19
20  int function1(int param)
21  {
22      double y = GLOBAL_CONST;
23      ...
24      return 0;
25  }
```

局部作用域和全局作用域都是块作用域的示例。变量只能在其作用域内被直接访问。

块作用域：变量 `i` 的作用域为第 13-16 行

`main` 的局部作用域：变量 `x` 的作用域为第 10-18 行，变量 `d` 的作用域为第 11-18 行

全局作用域：常量 `GLOBAL_CONST` 的作用域为第 4-25 行，函数 `function1` 的作用域为第 6-25 行

`function1` 的局部作用域：变量 `param` 的作用域为第 20-25 行，变量 `y` 的作用域为第 22-25 行

