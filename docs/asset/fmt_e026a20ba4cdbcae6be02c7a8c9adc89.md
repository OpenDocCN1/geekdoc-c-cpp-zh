
```cpp
20:   cout << FirstNumber << " x " << SecondNumber;
21:   cout << " = " << MultiplicationResult << endl;
22:
23:   return 0;
24:}
```

### 输出

此程序将帮助你乘以两个数字
输入第一个数字: 51
输入第二个数字: 24
51 x 24 = 1224

### 分析

此应用程序要求用户输入两个数字，程序将其相并显示结果。为了让应用程序能够用户输入的数字，它需要将它们存储在内存中。第 9 行和第 13 行定义的变量 `FirstNumber` 和 `SecondNumber` 负责临时存储用户输入的整数值。你在第 10 行和第 14 行使用 `std::cin` 接收用户输入。第 21 行的 `std::cout` 用于显示结果。

# 第 3 节：使用变量、声明常量

在列表 3.1 中，`FirstNumber`、`SecondNumber` 和 `MultiplicationResult` 都是相同类型——整数——分三行声明。如果你愿意，可以将这三个变量的声明合并为一行代码如下：

```cpp
int FirstNumber = 0, SecondNumber = 0, MultiplicationResult = 0;
```

因为 C++ 允许同时声明多个变量。然而，在需要时再声明变量通常更好，因为这样代码更易读。

### 什么是变量？

存储在变量中的数据是 RAM 中的数据。当计算机关闭或应用程序终止时，这些将会丢失，除非程序员将数据持久化到硬盘等存储介质上。

### 理解变量的作用域

普通变量在一个定义的范围内是有效的且可以使用的。当位于作用域之外时，编译器将无法识别变量名。在作用域之外，变量是一个编译器一未知的实体。

为了更好地理解变量的作用域，将列表 3.1 中的程序重组为函数 `MultiplyNumbers()`，该函数乘以两个数字并返回结果。

### 列表 3.2 演示变量的作用域

```cpp
1: #include <iostream>
2: using namespace std;
3:
4: void MultiplyNumbers ()
5: {
6:     cout << "Enter the first number: ";
7:     int FirstNumber = 0;
8:     cin >> FirstNumber;
9:
10:
11:    cout << "Enter the second number: ";
12:    int SecondNumber = 0;
13:    cin >> SecondNumber;
14:
15:    // Multiply two numbers, store result in a variable
16:    int MultiplicationResult = FirstNumber * SecondNumber;
17:
18:    // Display result
19:    cout << FirstNumber << " x " << SecondNumber;
20:    cout << " = " << MultiplicationResult << endl;
21: }
22: int main ()
23: {
24:    cout << "This program will help you multiply two numbers" << endl;
25:
26:    // Call the function that does all the work
27:    MultiplyNumbers();
28: }
```

### 列表 3.2 续

```cpp
26: MultiplyNumbers();
27:   // cout << FirstNumber << " x " << SecondNumber;
29:   // cout << " * " << MultiplicationResult << endl;
30:
31:   return 0;
32: )
```

# 输出

此程序将帮助你将两个数字相乘
输入第一个数字：51
输入第二个数字：24
51 x 24 = 1224

# 分析

列表 3.2 执行的操作与列表 3.1 完全相同，并产生相同的输出。唯一的区别是大部分工作被委托了一个名为 `MultiplyNumbers()` 的函数，由 `main()` 调用。注意，变量 `FirstNumber` 和 `SecondNumber` 不能在 `MultiplyNumbers()` 之外使用。如果你取消注释 `main()` 中的第 28 行或 29 行，将会遇到编译错误，最可能是类型“未定义的标识符”。

这是因为变量 `FirstNumber` 和 `SecondNumber` 的作用域是局部的，并且局限于它们所在的函数（在本例中为 `MultiplyNumbers()`）。局部变量可以在函数声明后一直到函数结束为止使用。表示函数结束的大括号 `{}` 限制了在同一范围内声明的变量的作用域。当函数结束时，所有局部变量都会被销毁，它们占据的内存会被释放。

在编译时，在 `MultiplyNumbers()` 中声明的变量在函数结束时消失，如果它们在 `main()` 中使用，编译将失败，因为这些变量在其中没有被声明。

> 注意
> 如果你在 `main()` 中声明了另一组同名的变量，不要期望它们会带有可能赋值给 `MultiplyNumbers()` 的值。
> 编译器将 `main()` 中的变量视为独立的实体，即使它们与另一个函数中声明的变量同名，因为这两个变量受其各自作用域的限制。

### 全局变量

如果列表 3.2 中函数 `MultiplyNumbers()` 使用的变量是在函数 `MultiplyNumbers()` 作用域之外而不是内部定义的，那么它们在 `main()` 和 `MultiplyNumbers()` 中都可以使用。列表 3.3 展示了全局变量，全局变量是程序中作用域最广的变量。

### 列表 3.3 使用全局变量

```cpp
1: #include <iostream>
2: using namespace std;
3:
4: //三个全局整数
5: int FirstNumber = 0;
6: int SecondNumber = 0;
7: int MultiplicationResult = 0;
8:
9: void MultiplyNumbers ()
10: {
11: cout << "Enter the first number: ";
12: cin >> FirstNumber;
13:
14: cout << "Enter the second number: ";
15: cin >> SecondNumber;
16:
17: // 两个数字相乘，将结果存储在变量中
18: MultiplicationResult = FirstNumber * SecondNumber;
19:
20: // 显示结果
21: cout << "Displaying MultiplyNumbers(): ";
22: cout << FirstNumber << " x " << SecondNumber;
23: cout << " = " << MultiplicationResult << endl;
24: }
25: int main ()
26: {
27: cout << "This program will help you two numbers" << endl;
28:
29: // 调用完成所有工作的函数
30: MultiplyNumbers();
31:
32: cout << "Displaying from main(): ";
33:
34: // 这行现在可以编译并运行了！
35: cout << FirstNumber << " x " << SecondNumber;
36: cout << " = " << MultiplicationResult << endl;
37:
38: return 0;
39: }
```

# 课程 3：使用变量、声明常量

# 输出

此程序将帮助你将两个数字相乘
输入第一个数字：51
输入第二个数字：19
Displaying from MultiplyNumbers(): 51 x 19 = 969
Displaying from main(): 51 x 19 = 969

# 分析

列表 3.3 在两个函数中显示了乘法结果，这两个函数都没有声明 `FirstNumber`、`SecondNumber` 和 `MultiplicationResult` 变量。这些变量是全局变量，因为它们在第 5-7 行被声明，位于在任何函数的作用域之外。注意第 23 行和第 36 行使用了这些变量并显示了它们的值。特别注意 `MultiplicationResult` 是如何在 `MultiplyNumbers()` 中赋值的，却在 `main()` 中被实际使用。

> 注意
> 不加区分地使用全局变量通常被认为是不良的习惯。
> 全局变量可以在任何函数中赋值，并可能包含不可预测的状态，特别是当团队中不同函数模块由不同程序员编写时。
> 像列表 3.3 那在 `main()` 中获取乘法结果的优雅方法是让 `MultiplyNumbers()` 将结果返回给 `main`。

# 编译器支持的常用++ 变量类型

在你找到的大多数示例中，C++ 都定义了 `int` 类型的变量——即整数。然而，C++ 程序员有多种编译器直接支持的基础变量类型可供选择。选择正确的变量类型与为任务选择正确的工具一样重要！菲利斯螺丝刀无法很好地配合普通的螺丝头，就像无符号整数无法存储负数的值一样！表 3.1 列出了各种变量类型以及它们可以包含的数据性质。这些信息对于编写高效且可靠的 C++ 程序非常重要。

### 表 3.1 变量类型

| 类型 | 值 |
|---|---|
| bool | true 或 false |
| char | 字符 |
| unsigned short | 0 到 65535 |
| short int | -32768 到 32767 |
| unsigned int | 0 到 4294967295 |
| long int | -2147483648 到 2147483647 |
| unsigned long long | 0 到 18446744073709551615 |
| long long | -9223372036854775808 到 9223372036854775807 |
| float | -3.4e-38 到 3.4e38 |
| double | -1.8e308 到 1.8e308 |

以下章节将详细解释这些类型。

### 使用 bool 类型存储布尔值

C++ 提供了一种专门用于包含布尔值（true 或 false）的类型，这些都是保留字。这对于存储开启或关闭、可用或不可用等标记特别有用。

一个初始化的布尔变量示例：

```cpp
bool AlwaysOn = false;
```

一个求值为布尔类型的表达式：

```cpp
bool DeleteFile = (UserSelection == "yes"); // 求值为 true
```

### 使用 char 类型存储字符值

使用 `char` 存储单个字符。示例声明：

```cpp
char UserInput = 'Y';
```

# 课程 3：使用变量、声明常量

注意内存由位组成。位可以是 0 或 1，字节可以包含数值表示。拉丁字母 A-Z、a-z、数字 0-9 以及某些特殊字符（如退格键）已由信息标准标准化，即 ASCII。

你可以查看附录 E 中的表格，可以看到赋值字符 'Y' 的 ASCII 值为 89。

### 有符号和无符号整数的概念

符号意味着正或负。你处理的所有数字都以位和字节的形式存储在内存中。1 字节内存位置包含 8 位。每个位可以是 0 或 1。因此，1 字节内存位置最多包含 2^8 个值。同样，16 位内存位置可以包含 2^16 个值——即 65536 个唯一值。

如果这些值是无符号的（假设仅为正），那么一个可以包含 0 到 255 的整数值，而两个字节分别包含 0 到 65535 的值。查看表 3.1 并注意 `unsigned short` 是支持此范围的类型，它包含在我们 16 位中。通过位和字节对值建模非常容易（见图 3.1）。

![](img/fd01f923cb963a04200115e3b215851c_60_0.png)

| | 位 0 |
|------|
| 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | = 65535 |

# 编译器支持的常用C++变量类型

图 3.2
16位符号整数的位结构。

| 15. . . . . . . . . . . . . . . . . 位 0 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 符号位 | | | | | | | | | | | | | | | |
| 15位包含绝对值 | | | | | | |

0: 表示正整数
1: 表示负整数

因此，占用 8 位的数字可以包含从 -128 到 127 之间的值，而占用 16 位的数字可以包含从 -32768 到 32767 之间的值。再次查看表3.1，请注意（符号的）`short` 是在 16 位空间内支持正、负整数值的类型。

### 符号整数类型 short, int 和 long long

这些类型在大小和它们能包含的值范围上不同。`int` 是最常用的类型，在大多数编译器上宽度为 32 位。根据你对该变量预期最大值的预测，使用正确的类型。

声明一个符号类型的变量非常简单：

```cpp
short SmallNumber = -100;
int LargerNumber = -70000;
long PossiblyLargerThanInt = -70000; // 在某些平台上，long 是一个 int
long longLargerThanInt = -7000000000;
```

### 无符号整数类型 unsigned short, unsigned int, unsigned 和 unsigned long long

与它们的对应类型不同，无符号整数类型不包含符号信息，它们实际上可以存储双倍的正值。

声明一个无符号类型的变量就像这样简单：

```cpp
unsigned SmallNumber = 255;
unsigned LargerNumber = 70000;
// 在某些平台上，long 是 int
unsigned PossiblyLargerThanInt = 70000;
unsigned longLargerThanInt = 70000000000;
```

# 节 3：使用变量，声明常量

注意

当你预期只有正值时，你应该使用无符号变量类型。所以，如果你在数苹果的数量，不要使用 `int`；请使用 `unsigned int`。后者在正数范围内包含的值是前者的两倍。

警告

因此，无符号类型可能不适用于银行应用程序中存储账户余额的变量。

### 浮点类型 float 和 double

浮点数就是你在学校里学过的实数。这些数字可以是正的也可以是负的。它们可以包含小数值。所以，如果你想在 C++ 变量中存储 pi 的值（22 / 7 或 3.14），你会使用浮点类型。

声明这些类型的变量遵循着与列表 3.1 中 `int` 完全相同的模式。因此，允许你存储小数的 `float` 声明如下所示：

```cpp
float Pi = 3.14;
```

而双精度浮点数（简单称为 `double`）定义为 `double MorePrecisePi = 22 / 7;`。

注意

表中提到的数据类型通常被称为 POD（纯旧数据）。POD 类别包含了这些类型以及它们的聚合体（结构体、枚举、联合体或类）。

### 使用 sizeof 确定变量的大小

大小是程序员在声明变量以存储分配给它的数据时，编译器保留的内存量。变量的大小取决于它的类型，C++ 有一个非常方便的操作符 `sizeof`，它可以告诉你变量或类型的字节（bytes）大小。

### 使用 sizeof 确定变量的大小

`sizeof` 的用法非常。要确定整数的大小，如列表 3.4 所示，通过参数 `int`（类型）调用 `sizeof`。

```cpp
cout << "Size of an int: " << sizeof (int);
```

### 列表 3.4 查找标准 C++ 变量的大小

```cpp
#include <iostream>
int main() {
    using namespace std;
    cout << "Computing the size of some C++ inbuilt variable types*" << endl;
    cout << "Size of an int: " << sizeof (int);
}
```

## 44 第 3 节：使用变量，声明常量

你可以使用以下代码访问或遍历数组中的元素并显示它们：

```cpp
for ( vector<int>::const_iterator Iterator = MyNumbers.begin();
     Iterator != MyNumbers.end();
     ++Iterator;
cout << *Iterator << " ";
```
