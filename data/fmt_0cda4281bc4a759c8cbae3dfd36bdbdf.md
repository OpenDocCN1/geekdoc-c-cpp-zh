
```cpp
using std::cin;
using std::endl;
using std::setw;
// 简单的 const 变量声明和初始化
// 习惯对编译时已知的值大写
// （取代原来的宏 #define）
const int MAX = 50;
// 简单的 constexpr 变量声明和初始化（优先）
constexpr int LARGEST = 50;
constexpr int Minimum(int a, int b)
// 带有形式参数的函数定义
{
    return (a < b) ? a : b; // 条件运算符 ?:
}
```

在在上一个程序段中，注意我们如何在数据类型之前使用 `const` 限定符声明变量。在这里，`const MAX = 50;` 仅仅将 `MAX` 初始化为 50。在代码后续部分不能通过赋值修改 `Max`。根据习惯，简单的 `const` 和 `constexpr` 限定变量（取代 `#define` 宏）通常全大写，而计算出的（或可能计算出的）值则使用典型的命名约定声明。接下来，我们使用 `constexpr LARGEST = 50;` 引入一个常量变量，以声明一个不可修改的变量。这种选项正成为首选用法，但并非总是可以利用。

接下来，我们有函数 `Minimum()` 的定义；注意在该体内使用了三元条件运算符 `?:`。还要注意此函数的返回值带有 `constexpr` 限定符（我们稍后会检查）。接下来，在我们继续程序的剩余部分时，检查 `main()` 函数体：

```cpp
int main()
{
```

在 `main()` 中，让我们考虑以下代码序列，其中我们提示用户“输入两个值：”并分别输入变量 `x` 和 `y`。在这里，我们调用函数 `Minimum(x,y)`，并将刚读取的两个值作为实际参数传递。注意在声明 `const` 变量的同时，我们使用函数的返回值初始化了 `min`。重要的是，设置 `min` 是作为一个单一声明和初始化的。如果将其分成两行代码——变量声明后接赋值——编译器将标记错误。带有 `const` 限定符的变量只能被初始化，而不能在声明后赋值。

接下来，我们用 `Minimum(a, b)` 的返回值初始化 `smallest`；注意参数 `a` 和 `b` 是可以在编译时确定的字面量。还注意 `Minimum()` 函数的返回值已带有 `constexpr` 限定符。这种限定对于 `constexpr smallest` 使用函数值进行初始化是必要的。注意如果我们尝试将 `x` 和 `y` 传递给 `Minimum()` 来设置 `smallest` 将得到错误，因为 `x` 和 `y` 的值不是字面量。

在上示例的最后一个代码序列中，注意我们使用 `MAX`（在程序示例的前部定义）为声明为 `char bigName[MAX]` 的固定大小数组 `bigName` 定义大小。我们同样使用 `LARGEST` 为固定大小数组 `largeName` 定义大小。在这里看到 `const` 或 `constexpr` 都可以以此方式为数组设置大小。然后我们进一步在 `setw(MAX)` 和 `setw(LARGEST)` 中使用 `MAX` 和 `LARGEST`，以在使用 `cin` 配合提取运算符 `>>` 读取键盘输入时不会溢出 `bigName` 或 `largeName`。最后，我们用函数 `strlen(bigname)` 的返回值初始化变量 `const int namelen` 并使用 `cout` 输出此值。注意由于 `strlen()` 不是带有 `constexpr` 限定符的函数，我们无法使用此返回值来初始化 `constexpr`。

上述完整程序示例对应的输出如下：

```
Enter两个 <int> values: 39 17
Minimum is: 17
Smallest of 10 15 is: 10
Enter two names: Gabby Dorothy
Length of name 1: 5
```

名称长度 2: 7

现在我们已经看到了如何使用 `const` 和 `constexpr` 来限定变量，让我们来考虑函数的常量限定。

## 函数的 `const` 限定

`const` 和 `constexpr` 关键字也可以与函数结合使用。这些修饰符可以用于参数，以指示参数本身不会被修改。这是一个非常有用的特性——函数的调用者将理解该函数不会修改通过这些方式限定的输入参数。然而，由于非指针（且非引用）变量是*按值*作为栈上实际参数的拷贝传递给函数的，对这些固有的参数拷贝进行 `const` 或 `constexpr` 限定并没有意义。因此，对标准数据类型的参数进行 `const` 或 `constexpr` 限定是没有必要的。

同样的原理也适用于函数的返回值。函数的返回值可以被 `const` 或 `constexpr` 限定；但是，除非返回的是指针（或引用），否则在栈上作为返回值传回的项目是一个拷贝。出于这个原因，当返回类型是指向常量对象的指针时（我们将在第3章*间接寻址：指针*及后续章节中介绍），`const` 限定的返回值更具意义。请注意，正如我们在之前的示例中所看到的，如果一个函数的返回值用于初始化 `constexpr` 变量，则该函数需要一个 `constexpr` 限定的返回值。作为 `const` 的最后一个用途，当我们转向类的面向对象（OO）细节时，我们可以利用此关键字来指定特定的成员函数不会修改该类的任何数据成员。我们将在第5章“深入探索类”中查看这种情况。

现在我们已经理解了 `const` 和 `constexpr` 修饰符的用法，并看到了它们与函数结合使用的潜在用途，让我们继续学习本章下一个语言特性：函数原型。

### 使用函数原型

在本节中，我们将检查函数原型的机制，例如在文件和跨文件中的位置布局，以获得更大的程序灵活性。我们还为原型参数添加可选的名称，并理解我们为何以及如何选择为 C++ 原型添加默认值。函数原型确保了 C++ 代码经过了强类型检查。

在继续学习函数原型之前，让我们花一点时间回顾一些编程术语。函数定义指的是包含函数的代码体，而函数的声明（也称为前向声明）仅仅是引入一个函数名及其返回类型和参数类型。前向声明允许编译器通过将调用与前向声明进行比较，从而在函数调用与其定义之间执行强类型检查。前向声明是有用的，因为函数定义并不总是出现在函数调用的之前的文件中；有时，函数定义出现在与其调用不同的文件中。

### 定义函数原型

函数原型是函数的前向声明，它描述了如何正确调用该函数。原型确保了函数调用与其定义之间的强类型检查。一个简单的函数原型由以下几个部分组成：

- 函数的返回类型
- 函数名
- 函数的类型和参数数量

函数原型允许函数调用位于函数定义之前，或者允许调用存在于单独文件的函数。随着我们学习更多 C++ 语言特性（如异常），我们将看到额外的元素构成了函数的扩展原型和扩展签名。现在，让我们来看一个简单的示例：

https://github.com/PackPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter02/Chp2-Ex2.cpp

```cpp
#include <iostream> // 优于：using namespace std;
using std::cout;
using std::endl;
[[nodiscard]] int Minimum(int, int);    // 函数原型

int main()
{
  int x = 5, y = 89;
  // 使用实际参数的函数调用
  cout << Minimum(x, y) << endl;
  return 0;
}
[[nodiscard]] int Minimum(int a, int b) // 函数定义
```

```cpp
// 使用形式参数
{
  return (a < b) ? a : b;
}
```

注意我们在上述示例的开头附近原型化了 `int Minimum(int, int);`。这个原型让编译器知道对 `Minimum()` 的任何调用都接受两个整数参数，并返回一个整数值（我们将在本节稍后的部分讨论类型转换）。

还要注意在函数返回类型之前使用了 `[[nodiscard]]`。这表示程序员应该存储返回值或以其他方式利用返回值（例如在表达式中）。如果忽略了此函数的返回值，编译器将发出警告。

接下来，在 `main()` 函数中，我们调用了函数 `Minimum(x, y)`。此时，编译器检查函数调用在类型、参数数量以及返回类型上是否符合上述原型。也就是说，两个参数都是整数（可以很容易转换为整数），且返回类型是整数（可以很容易转换为整数）。返回值将用作打印到 `cout` 的值。最后，函数 `Minimum()` 在文件中定义。如果函数与原型不匹配，编译器将抛出错误。

原型的存在允许在编译器看到函数定义之前对给定函数的调用进行完全的类型检查。目前的示例当然是为了说明这一点而刻意设计的；我们本可以交换 `Minimum()` 和 `main()` 在文件中出现的顺序。然而，想象一下 `Minimum()` 的定义包含在一个单独的文件中（这是更常见的情况）。

在多文件的情况下，函数定义将会被单独编译。然后，链接器的工作将是确保在链接多个文件时，原型是匹配的，以便链接器可以解析此类调用。如果原型不匹配，链接器将无法链接编译后的单元。

此示例的输出为：

5

现在我们已经理解了函数原型的基础知识，让我们看看如何为函数原型添加可选的名称。

### 在函数原型中命名参数

函数原型可以可选包含名称，这些名称可能与形式参数或实际参数不同。编译器会忽略参数名称，但这些名称通常可以增强可读性。让我们回顾之前的示例，在函数原型中添加可选的名称：

https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter02/Chp2-Ex3.cpp

```cpp
#include <iostream>
using std::cout; // 优于：using namespace std;
using std::endl;
// 带有可选参数名的函数原型
[[nodiscard]] int Minimum(int arg1, int arg2);
```

```cpp
int main()
{
    int x = 5, y = 89;
    cout << Minimum(x, y) << endl; // 函数调用
    return 0;
}
[[nodiscard]] int Minimum(int a, int b) // 函数定义
{
    return (a < b) ? a : b;
}
```

这个示例与之前的示例几乎相同。然而，请注意函数原型包含了命名参数 `arg1` 和 `arg2`。这些标识符会被编译器立即忽略。因此，这些命名参数不需要与函数的形式参数或实际参数匹配，它们的存在仅仅是为了可选增强可读性。

此示例的输出与上一个示例相同：

5

接下来，让我们通过为函数原型添加一个非常有用的特性：默认值，继续我们的讨论。

### 为函数原型添加默认值

可以在函数原型中指定默认值。当函数调用中缺少实际参数时，这些值将会被使用并

作为实际参数本身。默认值遵循以下标准：

- 在函数原型中，默认值必须从右到左指定，不能遗漏任何值。
- 实际参数在函数调用时是从左到右进行替换的，因此在原型中从右到左指定默认值的顺序是至关重要的。

函数原型可以为全部、部分或不填充其值默认值，只要这些默认值符合上述规范即可。

让我们来看一个使用默认值的示例：

https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter02/Chp2-Ex4.cpp

```cpp
#include <iostream>
using std::cout; // preferred to: using namespaces std;
using std::endl;
// fn. prototype with one default value
[[nodiscard]] int Minimum(int arg, int arg2 = 100000);
int main()
{
  int x = 5, y = 89;
  cout << Minimum(x) << endl; // function call with only
  // one argument (uses default)
  cout << Minimum(x, y) << endl; // no default vals used
  return 0;
}

[[nodiscard]] int Minimum(int a, int b) // fn. definition
{
  return (a < b) ? a : b;
}
```

在这个示例中，注意在函数原型 `int Minimum(int arg1, int arg2 = 100000);` 中最右侧的参数添加了默认值。这意味着当从 `main()` 调用 `Minimum()` 时，可以使用带有一个参数的 `Minimum(x)` 或带两个参数的 `Minimum(x, y)`。当调用单个参数的 `Minimum()` 时，该单个参数将绑定到函数形式参数中最左侧的参数，而默认值将绑定到形式参数列表中的下一个参数。然而，当调用两个参数的 `Minimum()` 时，两个实际参数都将绑定到函数的形式参数上；不会使用默认值。

以下是该示例的输出：

5

5

现在我们已经掌握了函数原型中默认值的用法，让我们通过在不同程序作用域的原型中使用不同的默认值来扩展这一概念。

### 在不同作用域中使用不同默认值进行原型

函数可以在不同的作用域下使用不同的值进行原型。这允许函数以通用的方式构建，并通过原型在多个应用程序中或代码的多个部分进行自定义。

这里是一个展示了同一函数（在不同作用域下）使用不同默认值的多个原型示例：

https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter02/Chp2-Ex5.cpp

```cpp
#include <iostream>
using std::cout;      // preferred to: using namespace std
using std::endl;
// standard function prototype
[[nodiscard]] int Minimum(int, int);
void Function1(int x)
{
    // local prototype with default default value
    [[nodiscard]] int Minimum(int arg1, int arg2 = 500);
    cout << Minimum(x) << endl;
}
void Function2(int x)
{
    // local prototype with default value
    [[nodiscard]] int Minimum(int arg1, int arg2 = 90);
    cout << Minimum(x) << endl;
}

[[nodiscard]] int Minimum(int a, int b) // fn. definition
{
    return (a < b) ? a : b;
}
int main()
{
    Function1(30);
    Function2(450);
    return 0;
}
```

在这个示例中，注意 `int Minimum(int, int);` 在文件顶部定义了原型。然后注意 `Minimum()` 在 `Function1()` 的局部作用域内被重新原型为 `Minimum(int arg1, int arg2 = 500);`，为其最右侧的参数指定了500的默认值。同样，在 `Function2()` 的作用域内，函数 `Minimum()` 被重新原型为 `int Minimum(int arg1, int arg2 = 90);`，为其最右侧的参数指定了90的默认值。当从 `Function1()` 或 `Function2()` 内部调用 `Minimum()` 时，将分别使用这两个函数作用域中的局部原型——每个原型都有它们自己的默认值。

通过这种方式，程序的特定区域可以很容易用默认值进行自定义，这些默认值对于应用程序的特定部分可能有意义。然而，请确保 _仅在调用函数的作用域内对具有个性化默认值的函数进行重新原型_，以确保这种自定义可以很容易包含在非常有限的作用域范围内。千万不要在全局作用域内用不同的默认值重新原型函数——这可能会导致意外且易错的结果。

该示例的输出如下：

30

90

现在我们已经探讨了单个和多个文件中函数原型的默认用法、在原型中使用默认值，以及在不同作用域内使用个性化默认值对函数重新原型，现在我们可以进入本章的最后一个主要主题：函数重载。

## 理解函数重载

C++ 允许两个或多个具有相似目的但在参数类型或数量上不同的函数以相同的名称共存。这被称为**函数重载**（function overloading）。这允许编译器根据参数选择函数的正确版本。

函数重载的基础知识

当存在两个或多个同名函数时，它们的签名（signatures）不同是至关重要的。函数重载的基础知识

- 函数的签名帮助编译器根据参数选择正确的版本。
- 只要签名不同，就可以存在两个或多个同名函数。
- 函数的签名取决于它的参数。

让我们花几分钟来理解一个稍大的示例，它将包含完整的程序；程序可以在以下链接找到：
