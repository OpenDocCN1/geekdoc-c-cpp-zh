
**图 6.18 使用默认实参。**

```cpp
// Fig. 6.18: fig06_18.cpp
// Using default arguments.
#include <iostream>
using namespace std;

// function prototype that specifies default arguments
unsigned int boxVolume(unsigned int length = 1, unsigned int width = 1,
   unsigned int height = 1);

int main() {
   // no arguments--use default values for all dimensions
   cout << "The default box volume is: " << boxVolume();

   // specify length; default width and height
   cout << "\n\nThe volume of a box with length 10,\n"
      << "width 1 and height 1 is: " << boxVolume(10);

   // specify length and width; default height
   cout << "\n\nThe volume of a box with length 10,\n"
      << "width 5 and height 1 is: " << boxVolume(10, 5);

   // specify all arguments
   cout << "\n\nThe volume of a box with length 10,\n"
      << "width 5 and height 2 is: " << boxVolume(10, 5, 2)
      << endl;
}

// function boxVolume calculates the volume of a box
unsigned int boxVolume(unsigned int length, unsigned int width,
   unsigned int height) {
   return length * width * height;
}
```

```text
The default box volume is: 1

The volume of a box with length 10,
width 1 and height 1 is: 10

The volume of a box with length 10,
width 5 and height 1 is: 50

The volume of a box with length 10,
width 5 and height 2 is: 100
```

对 `boxVolume` 的第一次调用（第 12 行）不指定实参，因此使用所有三个默认值 1。第二次调用（第 16 行）只传递一个 `length` 实参，因此 `width` 和 `height` 参数使用默认值 1。第三次调用（第 20 行）只为 `length` 和 `width` 传递实参，因此 `height` 参数使用默认值 1。最后一次调用（第 24 行）为 `length`、`width` 和 `height` 都传递了实参，因此不使用任何默认值。显式传递给函数的任何实参都从左到右赋给函数的形参。因此，当 `boxVolume` 接收一个实参时，函数将该实参的值赋给其 `length` 形参（即形参列表中最左边的形参）。当 `boxVolume` 接收两个实参时，函数按顺序将这些实参的值赋给其 `length` 和 `width` 形参。最后，当 `boxVolume` 接收全部三个实参时，函数分别将这些实参的值赋给其 `length`、`width` 和 `height` 形参。

### 关于默认实参的注意事项

默认实参*必须*位于函数形参列表的最右端（末尾）。当调用一个具有两个或更多默认实参的函数时，如果某个实参*不是*最右边的实参，那么该实参右侧的所有实参也*必须*省略。默认实参必须在函数名的*首次*出现处指定——通常是在函数原型中。如果函数定义同时充当原型，因而省略了函数原型，则应在函数头中指定默认实参。默认值可以是任何表达式，包括常量、全局变量或函数调用。默认实参也可以用于 `inline` 函数。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_782_0.png)

**良好编程实践 6.4**

*使用默认实参可以简化函数调用的编写。然而，有些程序员认为显式指定所有实参更清晰。*

## 6.15 一元作用域解析运算符

C++ 提供**一元作用域解析运算符（`::`）**，用于在作用域内存在同名局部变量时访问全局变量。⁵ 一元作用域解析运算符不能用于访问外层块中同名的*局部*变量。如果全局变量的名字与作用域内的局部变量名字不同，则可以直接访问全局变量，而无需使用一元作用域解析运算符。

⁵ C++ 标准也将作用域解析运算符（`::`）称为作用域运算符。

**图 6.19** 演示了在局部变量和全局变量同名（第 6 行和第 9 行）时使用一元作用域解析运算符的情况。为了强调变量 `number` 的局部版本和全局版本是不同的，程序将一个变量声明为 `int`，另一个声明为 `double`。

```cpp
// Fig. 6.19: fig06_19.cpp
// Unary scope resolution operator.
#include <iostream>
using namespace std;

int number{7}; // global variable named number

int main() {
    double number{10.5}; // local variable named number

    // display values of local and global variables
    cout << "Local double value of number = " << number
         << "\nGlobal int value of number = " << ::number << endl;
}
```

```text
Local double value of number = 10.5
Global int value of number = 7
```

**图 6.19 一元作用域解析运算符。**

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_784_0.png)

**良好编程实践 6.5**

始终使用一元作用域解析运算符（`::`）来引用全局变量（即使与局部变量名没有冲突），可以清楚地表明你打算访问的是全局变量而不是局部变量。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_785_0.png)

**软件工程观察 6.10**

始终使用一元作用域解析运算符（`::`）来引用全局变量，可以降低与非全局变量名称冲突的风险，从而使程序更易于修改。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_785_1.png)

**错误预防提示 6.10**

始终使用一元作用域解析运算符（`::`）来引用全局变量，可以消除因非全局变量隐藏全局变量而可能发生的逻辑错误。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_785_2.png)

**错误预防提示 6.11**

避免在程序中对不同用途使用相同名称的变量。尽管在各种情况下这是允许的，但它可能导致错误。

## 6.16 函数重载

C++ 允许定义多个同名函数，只要它们具有不同的签名。这称为**函数重载**。C++ 编译器通过检查调用中实参的数量、类型和顺序来选择调用正确的函数。函数重载用于创建多个名称*相同*的函数，这些函数执行类似的任务，但针对*不同*的数据类型。例如，数学库中的许多函数针对不同的数值类型进行了重载——C++ 标准要求 **6.3 节**中讨论的数学库函数提供 `float`、`double` 和 `long double` 重载版本。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_787_0.png)

**良好编程实践 6.6**

> *重载执行密切相关任务的函数可以使程序更易读、更易理解。*

### 重载的 `square` 函数

**图 6.20** 使用重载的 `square` 函数来计算一个 `int` 的平方（第 7–10 行）和一个 `double` 的平方（第 13–16 行）。第 19 行通过传递字面值 `7` 调用 `square` 函数的 `int` 版本。C++ 将整数字面值视为 `int` 类型。类似地，第 21 行通过传递字面值 `7.5` 调用 `square` 函数的 `double` 版本，C++ 将其视为 `double` 类型。在每种情况下，编译器都根据实参的类型选择要调用的正确函数。输出窗口的最后两行证实了在每种情况下都调用了正确的函数。

```cpp
// Fig. 6.20: fig06_20.cpp
// Overloaded square functions.
#include <iostream>
using namespace std;

// function square for int values
int square(int x) {
   cout << "square of integer " << x << " is ";
   return x * x;
}

// function square for double values
double square(double y) {
   cout << "square of double " << y << " is ";
   return y * y;
}

int main() {
   cout << square(7);   // calls int version
   cout << endl;
   cout << square(7.5); // calls double version
   cout << endl;
}
```

```text
square of integer 7 is 49
square of double 7.5 is 56.25
```

**图 6.20 重载的 `square` 函数**

