
```cpp
double calculatePay() const;
//Function to calculate and return the wages.
//Postcondition: Pay is calculated and returned

void setNameRateHours(string first, string last,
                      double rate, double hours);
//Function to set the first name, last name, payRate,
//and hoursWorked according to the parameters.
//Postcondition: firstName = first; lastName = last,
//              payRate = rate; hoursWorked = hours

partTimeEmployee(string first = "", string last = "",
                 double rate = 0, double hours = 0);
//Constructor with parameters
//Sets the first name, last name, payRate, and hoursWorked
//according to the parameters. If no value is specified,
//the default values are assumed.
//Postcondition: firstName = first; lastName = last,
//              payRate = rate; hoursWorked = hours

private:
    double payRate;      //variable to store the pay rate
    double hoursWorked;  //variable to store the hours worked
};
```

成员函数的定义可以放在单独的文件中。回想一下，要在用户程序中包含系统提供的头文件（例如 iostream），需要将头文件括在尖括号中；要在程序中包含用户定义的头文件，需要将头文件括在双引号中。

## 头文件的多重包含

上一节讨论了如何创建派生类的头文件。要在程序中包含头文件，需要使用预处理命令。回想一下，在程序编译之前，预处理器会首先处理该程序。考虑以下头文件：

```cpp
//Header file test.h

const int ONE = 1;
const int TWO = 2;
```

假设头文件 testA.h 包含文件 test.h，以便使用标识符 ONE 和 TWO。具体来说，假设头文件 testA.h 如下所示：

```cpp
//Header file testA.h

#include "test.h"
.
.
.
```

现在，考虑以下程序代码：

```cpp
//Program headerTest.cpp

#include "test.h"
#include "testA.h"
.
.
```

当编译程序 headerTest.cpp 时，它首先由预处理器处理。预处理器首先包含头文件 test.h，然后包含头文件 testA.h。当包含头文件 testA.h 时，由于它包含预处理指令 `#include "test.h"`，头文件 test.h 会在程序中被包含两次。第二次包含头文件 test.h 会导致编译时错误，例如标识符 ONE 已被声明。出现此问题是因为第一次包含头文件 test.h 时已经定义了变量 ONE 和 TWO。为了避免在程序中多次包含同一个文件，我们在头文件中使用某些预处理命令。让我们首先使用这些预处理命令重写头文件 test.h，然后解释这些命令的含义。

```cpp
//Header file test.h

#ifndef H_test
#define H_test
const int ONE = 1;
const int TWO = 2;
#endif
```

- a. `#ifndef H_test` 表示“如果未定义 H_test”
- b. `#define H_test` 表示“定义 H_test”
- c. `#endif` 表示“结束 if”

这里，H_test 是预处理器标识符。

这些命令的作用如下：如果标识符 H_test 未定义，则必须定义标识符 H_test，并让 `#define` 和 `#endif` 之间的其余语句交由编译器处理。如果头文件 test.h 在程序中被第二次包含，则语句 `#ifndef` 失败，直到 `#endif` 的所有语句都会被跳过。事实上，所有头文件都使用类似的预处理命令编写。

## C++ 流类

第 3 章详细介绍了如何使用标准 I/O 设备和文件 I/O 执行输入/输出（I/O）。特别地，你使用了对象 cin、提取运算符 >> 以及 get 和 ignore 等函数，从标准输入设备读取数据。你还使用了对象 cout 和插入运算符 <<，将输出发送到标准输出设备。为了使用 cin 和 cout，程序包含了头文件 iostream，其中包含类 `istream` 和 `ostream` 的定义。

此外，对于文件 I/O，程序包含了头文件 `fstream`，并且使用 `ifstream` 类型的对象进行文件输入，使用 `ofstream` 类型的对象进行文件输出。本节简要描述流类在 C++ 中如何关联和实现。

在 C++ 中，流类使用继承机制实现，如图 12-6 所示。

![](img/f97f778697507bb6fdd80c5991210cba_738_0.png)

**图 12-6** C++ 流类层次结构

图 12-6 展示了我们在前面几章中遇到的流类。从该图可以看出，类 `ios` 是所有流类的基类。类 `istream` 和 `ostream` 直接派生自类 `ios`。类 `ifstream` 派生自类 `istream`，类 `ofstream` 派生自类 `ostream`。此外，利用多重继承机制，类 `iostream`（不要与头文件 `iostream` 混淆——它们是不同的东西）和类 `fstream` 派生自类 `istream` 和 `ostream`。（本书不讨论类 `iostream` 和 `fstream`。）

类 `ios` 包含格式化标志，以及用于访问和/或修改这些标志设置的成员函数。为了标识 I/O 状态，类 `ios` 包含一个整数状态字。这个整数状态字持续更新，报告流的状态。

类 `istream` 和 `ostream` 负责提供内存与设备之间数据传输的操作。类 `istream` 定义了提取运算符 `>>`，以及 `get` 和 `ignore` 等函数。类 `ostream` 定义了插入运算符 `<<`，对象 `cout` 使用该运算符。

类 `ifstream` 派生自类 `istream`，以提供文件输入操作。类似地，类 `ofstream` 派生自类 `ostream`，以提供文件输出操作。`ifstream` 类型的对象用于文件输入；`ofstream` 类型的对象用于文件输出。头文件 `fstream` 包含类 `ifstream` 和 `ofstream` 的定义。

### 类的受保护成员

类的 `private` 成员对该类而言是私有的，不能在类外部直接访问。只有该类的成员函数可以访问 `private` 成员。如前所述，派生类不能直接访问基类的 `private` 成员。然而，有时（例如为了提高效率和/或简化代码）派生类需要直接访问基类的 `private` 成员。如果将 `private` 成员变为 `public`，那么任何人都可以访问该成员。回想一下，类的成员分为三类：`public`、`private` 和 `protected`。因此，基类若要允许其派生类访问某个成员，同时仍阻止在类外部直接访问该成员，就必须在成员访问说明符 `protected` 下声明该成员。因此，类的 `protected` 成员的可访问性介于 `public` 和 `private` 之间。派生类可以直接访问基类的 `protected` 成员。

总之，如果基类的某个成员需要由派生类访问，则该成员应在成员访问说明符 `protected` 下声明。

### 继承为 `public`、`protected` 或 `private`

假设 `class B` 派生自 `class A`。那么，B 不能直接访问 A 的 `private` 成员。也就是说，A 的 `private` 成员在 B 中是隐藏的。那么 A 的 `public` 和 `protected` 成员呢？本节给出访问基类成员时通常适用的规则。

考虑以下语句：

```cpp
class B: memberAccessSpecifier A
{
    .
    .
    .
};
```

在此语句中，`memberAccessSpecifier` 是 `public`、`protected` 或 `private`。

- 1. 如果 `memberAccessSpecifier` 是 `public`——也就是说，继承是 `public`——那么：
  - a. A 的 `public` 成员是 B 的 `public` 成员。它们可以在 `class B` 中直接访问。
  - b. A 的 `protected` 成员是 B 的 `protected` 成员。它们可以由 B 的成员函数（以及 `friend` 函数）直接访问。
  - c. A 的 `private` 成员在 B 中是隐藏的。它们不能在 B 中直接访问。它们可以由 B 的成员函数（以及 `friend` 函数）通过 A 的 `public` 或 `protected` 成员访问。
