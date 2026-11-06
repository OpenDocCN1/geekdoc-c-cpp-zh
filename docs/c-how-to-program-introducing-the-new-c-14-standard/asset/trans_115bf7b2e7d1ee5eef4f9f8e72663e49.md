

```cpp
// Fig. 17.9: fig17_09.cpp
// Demonstrating unique_ptr.
#include <iostream>
#include <memory>
using namespace std;

#include "Integer.h"

// use unique_ptr to manipulate Integer object
int main() {
   cout << "Creating a unique_ptr object that points to an Integer\n";

   // "aim" unique_ptr at Integer object
   unique_ptr<Integer> ptrToInteger{make_unique<Integer>(7)};

   cout << "\nUsing the unique_ptr to set the Integer\n";
   ptrToInteger->setInteger(99); // use unique_ptr to set Integer value

   // use unique_ptr to get Integer value
   cout << "Integer after setInteger: " << (*ptrToInteger).getInteger()
      << "\n\nTerminating program" << endl;
}
```

```text
Creating a unique_ptr object that points to an Integer
Constructor for Integer 7

Using the unique_ptr to set the Integer
Integer after setInteger: 99

Terminating program
Destructor for Integer 99
```

**图 17.9** `unique_ptr` 对象管理动态分配的内存。

第 17 行使用 `unique_ptr` 重载的 `->` 运算符，对 `ptrToInteger` 所管理的 `Integer` 对象调用函数 `setInteger`。第 20 行使用 `unique_ptr` 重载的 `*` 运算符解引用 `ptrToInteger`，然后使用点（`.`）运算符对 `Integer` 对象调用函数 `getInteger`。与常规指针一样，`unique_ptr` 的 `->` 和 `*` *重载运算符*可用于访问 `unique_ptr` 所指向的对象。

由于 `ptrToInteger` 是 `main` 中的一个非 `static` 局部变量，当 `main` 终止时它会被销毁。`unique_ptr` 析构函数会 `delete` 动态分配的 `Integer` 对象，这将调用 `Integer` 对象的析构函数。无论控制流以何种方式离开该块（例如，通过 `return` 语句或异常），`Integer` 所占用的内存都会被释放。最重要的是，使用这种技术可以*防止内存泄漏*。例如，假设某个函数返回一个指向某对象的指针。不幸的是，接收该指针的函数调用者可能不会 `delete` 该对象，从而导致*内存泄漏*。但是，如果函数返回一个指向该对象的 `unique_ptr`，那么当 `unique_ptr` 对象的析构函数被调用时，该对象将被自动删除。

### 17.9.1 `unique_ptr` 的所有权

这个类之所以命名为 `unique_ptr`，是因为同一时刻只能有*一个* `unique_ptr` 拥有一个动态分配的对象。当你将一个 `unique_ptr` 赋值给另一个 `unique_ptr` 时，赋值右侧的 `unique_ptr` 会将其管理的动态内存的*所有权转移*给赋值左侧的 `unique_ptr`。当一个 `unique_ptr` 作为参数传递给另一个 `unique_ptr` 的构造函数时也是如此。（这些操作使用 `unique_ptr` 的移动赋值运算符和移动构造函数——我们将在第 24 章讨论移动语义。）最后一个持有指向动态内存指针的 `unique_ptr` 对象将删除该内存。这使得 `unique_ptr` 成为将动态分配的内存返回给客户端代码的理想机制。当 `unique_ptr` 在*客户端*代码中超出作用域时，`unique_ptr` 的析构函数会删除动态分配的对象——如果该对象有析构函数，它会在内存返还给系统之前被调用。

### 17.9.2 `unique_ptr` 指向内置数组

你也可以使用 `unique_ptr` 来管理动态分配的内置数组。例如，考虑以下语句：

```cpp
unique_ptr<string[]> ptr{make_unique<string[]>(10)};
```

因为 `make_unique` 的类型被指定为 `string[]`，该函数会获取一个由参数（10）指定元素数量的*动态分配的内置数组*。默认情况下，使用 `make_unique` 分配的数组元素对于基本类型会初始化为 0，对于 `bool` 类型初始化为 `false`，对于类对象则通过默认构造函数初始化——因此在这种情况下，该数组将包含 10 个初始化为空 `string` 的 `string` 对象。

管理数组的 `unique_ptr` 提供了重载的 `[]` 运算符来访问数组元素。例如，语句：

```cpp
ptr[2] = "hello";
```

将 `"hello"` 赋值给 `ptr[2]` 处的 `string`，下面的语句显示该 `string`：

```cpp
cout << ptr[2] << endl;
```

## 17.10 标准库异常层次结构

异常可以很好地分为多个类别。C++ 标准库包含一个异常类层次结构，其中部分类如图 17.10 所示。正如我们在 17.2 节首次讨论的，该层次结构的顶端是基类 `exception`（定义在头文件 `<exception>` 中），它包含虚函数 `what`，派生类可以覆盖该函数以发出适当的错误消息。如果 `catch` 处理程序捕获基类类型异常的引用，它也可以捕获从该基类公开派生的所有类的对象的引用——这允许对相关错误进行多态处理。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2197_0.png)

**图 17.10** 标准库异常类中的一部分。

基类 `exception` 的直接派生类包括 `runtime_error` 和 **`logic_error`**（两者都定义在头文件 `<stdexcept>` 中），它们各自又有几个派生类。同样派生自 `exception` 的还有 C++ 运算符抛出的异常——例如，`new` 抛出 `bad_alloc`（[17.8 节](Section 17.8)），`dynamic_cast` 抛出 `bad_cast`（[第 12 章](Chapter 12)），`typeid` 抛出 `bad_typeid`（[第 12 章](Chapter 12)）。

类 `logic_error` 是几个表示程序逻辑错误的标准异常类的基类。例如，我们在 set 函数中使用了类 **`invalid_argument`**（从[第 9 章](Chapter 9)开始）来表示尝试设置无效值的情况。（当然，正确的编码可以防止无效参数到达函数。）类 **`length_error`** 表示用于所操作对象的长度大于该对象允许的最大大小。类 **`out_of_range`** 表示某个值（例如数组下标）超出了其允许的取值范围。

类 `runtime_error`（我们在[17.4 节](Section 17.4)中简要使用过）是几个表示执行时错误的其他标准异常类的基类。例如，类 **`overflow_error`** 描述**算术上溢错误**（即算术运算的结果大于给定数值类型可以存储的最大数），类 **`underflow_error`** 描述**算术下溢错误**（即算术运算的结果小于给定数值类型可以存储的最小数）。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2199_0.png)

### 错误预防提示 17.8

*将继承与异常结合使用，可以使异常处理程序以简洁的记法捕获相关错误。一种方法是单独捕获指向派生类异常对象的每种引用类型，但更简洁的方法是改为捕获指向基类异常对象的指针或引用。此外，单独捕获指向派生类异常对象的指针或引用容易出错，尤其是当你忘记显式测试一个或多个派生类引用类型时。*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2199_1.png)

### 常见编程错误 17.6

*将捕获基类对象的 `catch` 处理程序放在捕获派生类对象的 `catch` 之前是一个逻辑错误。基类的 `catch` 会捕获所有从该基类派生的类的对象，因此派生类的 `catch` 永远不会执行。*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2200_0.png)

### 常见编程错误 17.7

*异常类不一定派生自类 `exception`，因此捕获类型 `exception` 并不能保证捕获程序可能遇到的所有异常。*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2200_1.png)

### 错误预防提示 17.9

*要捕获 `try` 块中可能抛出的所有异常，请使用 `catch(...)`。以这种方式捕获异常的一个弱点是，捕获到的异常类型是未知的。另一个弱点是，没有命名参数，就无法在异常处理程序内部引用异常对象。*

