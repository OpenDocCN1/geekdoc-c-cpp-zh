
```cpp
// demonstrate squareByReference

cout << "z = " << z << " before squareByReference" << endl;

squareByReference(z);

cout << "z = " << z << " after squareByReference" << endl;

// squareByValue multiplies the number by itself, stores the
// result in number and returns the new value of number
int squareByValue(int number) {
    return number * number; // caller's argument not modified
}

// squareByReference multiplies numberRef by itself and stores the result
// in the value which numberRef refers in function main
void squareByReference(int *numberRef) {
    *numberRef *= *numberRef; // caller's argument modified
}
```

`x = 2` `squareByValue`
Value returned by `squareByValue`: `4`
`x = 2` `squareByValue`

`z = 4` before `squareByReference`
`z = 16` after `squareByReference`

图 6.17 | 按值传递和按引用传递参数。（2 部分中的 2 部分。）

# 函数内部作为别名的引用

引用也可以作为函数内部其他变量的别名（尽管它们通常如图 6.17 所示作为引用使用）。例如，以下代码：

```cpp
int count; // declare integer variable count
int &cRef=count; // create an alias for count
++cRef; // increment count (using its alias cRef)
```

通过其别名 `cRef` 增加变量 `count` 的值。引用变量必须在声明时初始化，不能重新赋值给其他变量。从这个意义上说，引用是常量。对别名（即引用）执行的所有操作实际上都是在原始变量上执行的。别名仅仅是原始变量的另一个名称。除非是对常量的引用（下文将讨论），否则引用初始化器必须是一个左值（例如，变量名），而不能是常量或右值表达式（例如，计算结果）。

# const 引用

要指定不允许修改相应的参数，请在参数声明的类型名之前放置 `const` 修饰符。

## 6.14 默认参数

例如，考虑类 `setName`（图 3.2）。为了在该早期示例中简单，我们在 `setName` 成员函数中使用按值传递，其定义头如下：

```cpp
void setName(std::string accountName)
```

当调用此成员函数时，它接收了字符串参数的副本。string 对象可能很大，因此这种拷贝操作会降低应用程序的性能。

出于这个原因，string 对象（以及普通对象）应该按引用传递。遵循最小权限原则，类的 `setName` 成员函数不需要修改其参数，我们可以声明参数为：

```cpp
const std::string& accountName
```

从左到右，`accountName` 参数是对字符串常量的引用。我们获得了按引用传递字符串的性能，但 `setName` 将该参数视为常量，它不能修改调用者中的值——就像按值传递一样。调用 `setName` 的代码仍将像我们在图 3.1 中的那样传递字符串参数。

![](img/d9ae0ed4c13d4f57e9ae2c92e9fdf0b7_285_0.png)

- **性能技巧 6.4**：对于传递大对象，使用 `const` 引用参数来模拟按值传递的外观安全性，并避免拷贝大对象的开销。

同样，类的 `setName` 成员函数定义头为：

```cpp
std::string getName() const
```

这表示字符串是按值返回的。将其改为：

```cpp
const std::string& getName() const
```

表示字符串应该按引用返回（消除了拷贝字符串的开销），并且调用者不能修改返回的字符串。

# 返回局部变量的引用

函数可以返回局部变量的引用，但这是危险的。返回局部变量时——除非变量被声明为 `static`——该引用指向一个在函数终止时被丢弃的变量。访问此类变量会导致未定义行为。指向未定义变量的引用被称为悬空引用（dangling references）。

![](img/d9ae0ed4c13d4f57e9ae2c92e9fdf0b7_285_1.png)

- **常见编程错误 6.8**：在被调用函数中返回局部变量是一个逻辑错误，编译器通常会对此发出警告。编译警告指示了潜在的问题，因此软件工程团队要求在不出现警告的情况下编译代码。

## 6.14 默认参数

程序对于某个特定参数使用相同的参数值反复调用函数是常见现象。在这些情况下，你可以指定该参数有一个默认参数，即要传递给该参数的默认值。当程序在函数调用中省略了具有默认参数的参数的参数时，编译器会写出该函数调用并插入该参数的默认值。

# 带有默认参数的 boxVolume 函数

图 6.18 展示了使用默认参数计算箱体体积的函数。

```cpp
//// Fig. 6.18: fig06_18.cpp
// Using default arguments.
#include <iostream>
using namespace std;
int boxVolume(int length = 1, int width = 1, int height = 1) {
    return length * width * height;
}
int main() {
    cout << "Volume: " << boxVolume(2, 3, 4) << endl;
    cout << "Volume: " << boxVolume(2, 3) << endl;
    cout << "Volume: " << boxVolume(2) << endl;
    return 0;
}
```

![](img/d9ae0ed4c13d4f57e9ae2c92e9fdf0b7_286_0.png)

图 6.18 | 使用默认参数。

## 第 6 章 函数与递归简介

```cpp
5
6 int number{7}; // 名为 number 的全局变量
int main() {
    double number{10.5}; // 名为 number 的局部变量
    // 显示局部和全局变量的值
    cout << "Local value of number = " << number
    << "\nGlobal int value of number = " << ::number << endl;
}
```

Local value of number = 10.5
Global int value of number = 7

**图 6.19** | 作用域解析运算符。（2 部分，共 2 部分。）

- **良好的编程实践 6.5**
使用作用域解析运算符 (`::`) 来引用全局变量（即使与局部变量名没有冲突）可以清楚地表示你的意图是访问全局变量而非局部变量。

- **软件工程观察 6.10**
使用作用域解析运算符 (`::`) 来引用全局变量可以由于减少与非全局变量发生名称冲突的风险，从而使程序更易维护。

- **错误预防技巧 6.10**
使用作用域解析运算符 (`::`) 来引用全局变量可以消除当非全局变量隐藏全局变量时可能发生的逻辑错误。

- **错误预防技巧 6.11**
在程序中避免为不同目的使用同名的变量。虽然这在各种情况下是被允许的，但会导致错误。

## 6.16 函数重载

C++ 允许定义多个同名的函数，只要它们的签名（signatures）不同。其中一个特性是函数重载。C++ 编译器通过检查调用中的名称、类型和参数顺序来选择要调用的适当函数。函数重载用于创建多个同名但执行相似任务且处理不同数据类型的函数。例如，数学库中的许多函数都针对不同的数值类型进行了重载——C++ 标准要求第 6.3 节讨论的数学库函数提供 `float` 和 `double` 重载版本。

- **良好的编程实践 6.6**
重载执行密切相关任务的函数可以使程序更可读、易理解。

## 重载的 square 函数

图 6.20 使用重载的 `square` 函数来计算 `int` 的平方（第 7–10 行）和 `double` 的平方（第 13–16 行）。第 19 行通过传递字面量 7 调用了 `int` 版本的 `square` 函数。C++ 将整数字面量视为 `int` 类型。同样，第 21 行通过传递字面量 7.5 调用了 `double` 版本的 `square` 函数，它是 `double` 类型。在每情况下，编译器都根据参数的类型选择正确的调用函数。输出窗口的最后两行确认了每个情况下都调用了正确的函数。

```cpp
// Fig.6.20: fig06-20.cpp
// 重载的 square 函数。
#include <iostream>
using namespace std;
// 用于 int 值的 square 函数
int square(int x) {
    cout << "square of integer " << x << " is ";
    return x * x;
}
// 用于 double 值的 square 函数
double square(double y) {
    cout << "square of double " << y << " is ";
    return y * y;
}
int main() {
    cout << square(7); // 调用 int 版本
    cout << endl;
    cout << square(7.5); // 调用 double 版本
    cout << endl;
}
```

| square of integer 7 is 49 |
| square of double 7.5 is 56.25 |

**图 6.20** 重载的 `square` 函数。

### 编译器如何区分重载函数

重载函数通过它们的*签名*（signatures）来区分。签名是函数名称及其参数类型（按顺序）的组合。编译器用其参数的类型对每个函数标识符进行编码（有时称为*名称修饰*（name mangling）或*名称装饰*（name decoration）），以确保*类型安全*。类型安全链接确保重载函数符合参数的类型。图 6.21 是用 GNU C++ 编译的。我们没有显示程序的执行输出（就像我们通常做的那样），而是展示了 GNU C++ 在汇编语言中产生的修饰名称。

对于 GNU C++，修饰名称（main 除外）以两个下划线 (`_`) 开头，随后是字母 Z，然后是函数名。Z 之后的数字指定了函数名称的字符数。例如，函数 `square`

```cpp
// Fig. 6.1: fig06_21.cpp
// 名称修饰以实现类型安全链接
// 用于 int 值的 square 函数
int square(int x) {
    return x * x;
}
// 用于 double 值的 square 函数
double square(double y) {
    return y * y;
}
// 接收类型参数的函数
int, void nothing1(int a, float b, char c, int&d) { }
// char, int, float& 和 double
// 接收类型参数的函数
int nothing2(char a, int b, float& c, double& d) {
    return 0;
}
int main() {
```

![](img/d9ae0ed4c13d4f57e9ae2c92e9fdf0b7_290_0.png)

其名称有 6 个字符，因此它的修饰名称是 `__Z`。

- 对于接收 `int` 的 `square`（第 5 行），`i` 代表 `int`。
- 对于接收 `double` 的 `square`（第 10 行），`d` 代表 `double`。
- 对于接收 `int`, `float`, `char`, `int&` 参数的 `nothing1`（第 16 行），`i` 代表 `int`，`f` 代表 `float`，`c` 代表 `char`
- 对于接收 `char`, `int`, `float&`, `double&` 参数的 `nothing2`（第 20 行），`c` 代表 `char`，`i` 代表 `int`，`f` 代表 `float&`，`d` 代表 `double`。

编译器通过参数列表区分重载函数。返回类型可以不同，但如果不同，它们必须具有不同的参数列表。函数修饰是特定编译器的。例如，Visual C++ 为 `square` 函数产生了 `__ZsquareAH` 为

## 6.17 函数模板

第 5 行。GNU C++ 不进行修饰；然而，编译器会。例如，Visual C++ 使用 `_main`。

### 良好的编程实践 6.9

创建参数列表相同的函数函数

编译器仅使用参数列表来区分重载函数。此类函数需要相同数量的参数。在重载带有默认参数的函数时要小心，因为可能会导致歧义。

### 错误预防技巧 6.10

带有默认参数的函数可能与另一个函数以相同方式调用，这会导致错误。例如，程序包含一个不带参数的函数和一个包含所有默认参数的同名函数，当尝试不带参数使用该函数时会导致错误。编译器无法确定选择哪个版本。

### 重载运算符

在第 10 章中，我们将讨论重载运算符如何操作用户定义类型。事实上，到目前为止我们一直在使用重载运算符，包括流插入运算符 `<<` 和流提取运算符 `>>`，对所有基本类型都进行了重载。我们将在第 10 章详细说明重载 `<< >>` 以处理用户定义类型。

重载函数通常用于对不同类型执行不同程序逻辑的相似操作。如果程序逻辑和操作对于每个数据类型都是相同的，可以使用函数模板更紧凑、方便地执行重载。你编写单个函数模板。根据调用该函数时提供的参数类型，C++ 会自动生成模板特化来处理每个类型。因此，单个函数模板本质上定义了一族重载函数。

### maximum 函数模板

图 622 定义了一个 `maximum` 函数模板（第 13–18 行），用于确定三个值的最大值。所有模板定义都以 `template` 关键字开头，后面跟着圆角括号内的模板参数列表。模板参数列表中的每个参数之前都有 `typename` 或 `class` 关键字（它们在此处是同义词）。类型参数是基本类型或用户定义类型的占位符。这些占位符（在此例中为 `T`）用于指定参数的类型（第 4 行）、指定函数的返回类型（第 4 行）以及在函数体内部声明变量（第 5 行）。函数模板的定义类似于任何其他函数，但使用类型参数作为占位符。

## 第26 章 函数与递归简介

```cpp
// Fig. 6.22: maximum.h
// 函数模板 maximum 头文件。
template <typename T> // 或 template<class T>
T maximum(T value1, T value2, T value3) {
    T maximumValue=value1; // 假设 value1 是最大的
    // 确定 value2 是否大于 maximumValue
    if (value2 > maximumValue) {
        maximumValue = value2;
    }
    // 确定 value3 是否大于 maximumValue
    if (value3 > maximumValue) {
        maximumValue = value3;
    }
    return maximumValue;
}
```

**图 6.22** 函数模板 `maximum` 头文件。

该函数模板声明了一个单类型参数 `T`（第 3 行），作为函数 `maximum` 用要测试的数据类型的占位符。对于特定的模板定义，类型参数的名称在模板参数列表中必须是唯一的。当编译器在源代码中检测到 `maximum` 调用时，`maximum` 调用中参数的类型将替换整个模板定义中的 `T`，然后 C++ 会创建一个完整的函数，用于确定指定类型三个值的最大值——这三个值具有相同的类型，因此我们在示例中使用了一个类型参数。新创建的函数模板是代码生成的手段。（我们在第 15 章中使用需要多个类型参数的 C++ 标准库模板。）

### 使用函数模板 maximum

图 6.23 使用 `maximum` 函数模板分别确定三个 `int` 值、三个 `double` 值和三个 `char` 值的最大值（第 15、24 和 33 行）。由于每次调用都使用不同类型的参数，编译器会为每个调用创建一个独立的函数定义：一个期望三个 `int` 值，一个期望三个 `double` 值，另一个期望三个 `char` 值。

```cpp
// Fig. 6.23: maximum06_23.cpp
// 函数模板 maximum 测试程序。
#include <iostream>
#include "maximum.h" // 函数模板 maximum 的定义
using namespace std;
int main() {
    // 使用 int 值演示 maximum
    cout << "Input three integers: ";
    int int1, int2, int3;
    cin >> int1 >> int2 >> int3;
}
```
