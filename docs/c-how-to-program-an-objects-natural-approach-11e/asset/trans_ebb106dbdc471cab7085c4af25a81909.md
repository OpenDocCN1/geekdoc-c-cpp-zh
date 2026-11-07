

当使用转换构造函数或转换运算符执行隐式转换时，C++ 对每个表达式只能应用一次隐式构造函数或运算符函数调用（即一次用户定义的转换）来尝试满足该表达式的需求。编译器不会通过执行一系列隐式的用户定义转换来满足表达式的需求。

### 检查点

- 1. *(填空)* ________ 构造函数使编译器能够在用户定义类型之间或在用户定义类型与基本类型之间进行转换。  
  **答案：** 转换。
- 2. *(判断正误)* 编译器可以隐式使用强制转换运算符和转换构造函数来创建对象。  
  **答案：** 正确。
- 3. *(判断正误)* C++ 可以通过执行一系列隐式的用户定义转换来满足表达式的需求。  
  **答案：** 错误。实际上，C++ 对每个表达式只能应用一次用户定义的转换。

## 11.9 explicit 构造函数和转换运算符

回想一下，我们一直将每个可以用一个参数调用的构造函数声明为 `explicit`，包括我们为其指定了默认参数的多参数构造函数。除了复制构造函数和移动构造函数外，任何可以用*单个参数*调用且未声明为 `explicit` 的构造函数，都可以被编译器用来执行*隐式转换*。该构造函数的参数被转换为一个该构造函数所在类的对象。这种转换是自动的——无需强制转换。

在某些情况下，隐式转换是不受欢迎的或容易出错的。例如，我们的 `MyArray` 类定义了一个接受单个 `size_t` 参数的构造函数。该构造函数的意图是创建一个包含指定数量元素的 `MyArray` 对象。然而，如果这个构造函数没有声明为 `explicit`，它就可能被编译器滥用来执行隐式转换。

不幸的是，编译器可能会在你没有预料到的情况下使用隐式转换，从而导致运行时逻辑错误或产生编译错误的歧义表达式。

### 意外地将单参数构造函数用作转换构造函数

程序（图 11.7）使用第 11.6 节的 `MyArray` 类来演示一次不恰当的隐式转换。为了允许这种隐式转换，我们从 `MyArray.h`（图 11.4）的第 16 行删除了 `explicit` 关键字。

```cpp
// fig11_07.cpp
// 单参数构造函数和隐式转换。
#include <iostream>
#include "MyArray.h"
using namespace std;

void outputArray(const MyArray&); // 原型

int main() {
    MyArray ints1(7); // 7 个元素的 MyArray
    outputArray(ints1); // 输出 MyArray ints1
    outputArray(3); // 将 3 转换为 MyArray 并输出内容
}

// 打印 MyArray 内容
void outputArray(const MyArray& arrayToOutput) {
    std::cout << "The MyArray received has " << arrayToOutput.size()
              << " elements. The contents are: " << arrayToOutput << "\n";
}
```

```
MyArray(size_t) constructor
The MyArray received has 7 elements. The contents are: {0, 0, 0, 0, 0, 0, 0}
MyArray(size_t) constructor
The MyArray received has 3 elements. The contents are: {0, 0, 0}
MyArray destructor
MyArray destructor
```

**图 11.7** | 单参数构造函数和隐式转换。

main（图 11.7）中的第 10 行实例化了 MyArray 对象 ints1，并调用*单参数构造函数*，传入值 7 来指定 ints1 的元素个数。回想一下，接收 size_t 参数的 MyArray 构造函数会将所有 MyArray 元素初始化为 0。第 11 行调用函数 outputArray（在第 16–19 行定义），该函数接收一个 const MyArray& 作为其参数。该函数输出其参数的元素个数和内容。在此例中，MyArray 的大小为 7，因此 outputArray 显示七个 0。

第 12 行以值 3 作为参数调用 outputArray。该程序*没有*包含接受 int 参数的 outputArray 函数。因此，编译器判断参数 3 是否可以转换为 MyArray 对象。由于类 MyArray 提供了一个带有一个 size_t 参数（可以接收 int）的构造函数，并且该构造函数未声明为 *explicit*，编译器假定该构造函数是一个*转换构造函数*，并使用它将参数 3 转换成一个包含三个元素的临时 MyArray 对象。然后，编译器将这个临时 MyArray 对象传递给函数 outputArray，后者显示临时 MyArray 的大小和内容。因此，即使我们没有*显式*提供接受 int 的 outputArray 函数，编译器也能编译第 12 行。输出显示了包含 0 的三个元素的 MyArray 的内容。

### 使用单参数构造函数防止隐式转换

我们将每个单参数构造函数都声明为 *explicit* 的原因，是为了在不应允许此类转换时，*抑制通过转换构造函数进行的隐式转换*。

声明为 **explicit** 的构造函数不能用于隐式转换。我们的下一个程序使用来自第 11.6 节的 MyArray 类，该类在其接收 `size_t` 的单参数构造函数的声明中包含了关键字 `explicit`：

```cpp
explicit MyArray(size_t size);
```

图 11.8 展示了图 11.7 中程序的一个稍作修改的版本。当编译图 11.8 中的程序时，编译器会产生一条错误消息，例如

```
error: invalid initialization of reference of type ‘const MyArray&’
from expression of type ‘int’
```

在 g++ 上，这表明第 12 行传递给 outputArray 的整数值无法转换为 const MyArray&。第 13 行演示了如何使用 explicit 构造函数创建一个包含 3 个元素的临时 MyArray 并将其传递给 outputArray。

```cpp
// fig11_08.cpp
// 演示 explicit 构造函数。
#include <iostream>
#include "MyArray.h"
using namespace std;

void outputArray(const MyArray&); // 原型

int main() {
   MyArray ints1{7}; // 7 个元素的 MyArray
   outputArray(ints1); // 输出 MyArray ints1
   outputArray(3); // 将 3 转换为 MyArray 并输出其内容
   outputArray(MyArray(3)); // 显式调用单参数构造函数
}

// 打印 MyArray 内容
void outputArray(const MyArray& arrayToOutput) {
   std::cout << "The MyArray received has " << arrayToOutput.size()
      << " elements. The contents are: " << arrayToOutput << "\n";
}
```

**图 11.8** | 演示 explicit 构造函数。

除非单参数构造函数旨在被隐式用作转换构造函数，否则你应始终对其使用 **explicit** 关键字。在这种情况下，你应该将单参数构造函数声明为 `explicit(false)`。这会向类的用户表明你希望允许使用该构造函数执行隐式转换。

### explicit 转换运算符

正如你可以将单参数构造函数声明为 explicit，你也可以将转换运算符声明为 explicit——或者在 C++20 中，`explicit(true)`——以防止编译器使用它们执行隐式转换。例如，在类 MyArray 中，原型

```cpp
explicit operator bool() const noexcept;
```

将 `bool` 强制转换运算符声明为 `explicit`，因此你通常必须使用 `static_cast` 显式调用它，例如

```cpp
static_cast<bool>(myArrayObject)
```

`static_cast` 运算符将其参数显式转换为尖括号中的类型。正如我们在 MyArray 案例研究中所展示的，C++ 仍然可以使用显式的 `bool` 转换运算符，在条件中将对象转换为 `bool` 值来执行上下文转换。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_702_0.png)

### 检查点

- 1. *(判断正误)* 任何可以用一个参数调用且未声明为 `explicit` 的构造函数都可以用来执行隐式转换。  
  **答案：** 错误。复制构造函数和移动构造函数各自接收一个参数，但不执行隐式转换。
- 2. *(代码)* 在单参数构造函数或转换运算符之前，你应该写什么来标明它可用于隐式转换？  
  **答案：** `explicit(false)`。
- 3. *(代码)* 在单参数构造函数或转换运算符之前，你应该写什么来标明它不能用于隐式转换？  
  **答案：** `explicit` 或 `explicit(true)`。

## 11.10 重载函数调用运算符 ()

重载函数调用运算符 `()` 非常强大，因为函数可以接受任意数量的逗号分隔参数。我们将在第 14.5 节的一个自然场景中演示重载的函数调用运算符。

## 11.11 小结

本章演示了如何通过运算符重载来精心设计有价值的类，使 C++ 现有的运算符能够用于自定义类对象。首先，我们使用了一些 string 类的重载运算符。接下来，我们介绍了运算符重载的基础知识，包括哪些运算符可以被重载，以及运算符重载的各种规则和限制。

我们介绍了使用运算符 `new` 和 `delete` 进行动态内存管理，这些运算符在运行时为对象和基于指针的内置数组获取和释放内存。我们讨论了使用旧式 `new` 和 `delete` 语句的问题，例如忘记使用 `delete` 来释放不再需要的内存。我们介绍了 RAII（资源获取即初始化），并演示了智能指针。你看到了在创建 unique_ptr 智能指针对象时如何动态分配内存。该 unique_ptr 在对象超出作用域时自动释放内存，从而防止内存泄漏。

接下来，我们介绍了本章的重点 MyArray 案例研究，该研究使用重载运算符和其他功能来解决基于指针的数组的各种问题。我们实现了在自己管理资源的类中通常会定义的五种特殊成员函数——复制构造函数、复制赋值运算符、移动构造函数、移动赋值运算符和析构函数。我们还讨论了如何自动生成

