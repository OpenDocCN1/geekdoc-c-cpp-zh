
- 2. 尝试使用折叠表达式（Fold Expression）实现一个计算平均值的函数，允许传递任何参数。

参考答案参见此处。

## 第03章：语言运行时增强

### 3.1 Lambda 表达式

`Lambda` 表达式是现代 `C++` 中最重要的特性之一，`Lambda` 表达式提供了类似匿名函数的功能。当需要函数但不想使用名称来调用函数时，就会使用匿名函数。实际上有很多很多这样的场景。因此，匿名函数几乎是现代编程语言的标配。

#### 基础

`Lambda` 表达式的基本语法如下：

```cpp
[capture list] (parameter list) mutable(optional) exception attribute -> return type {
// 函数体
}
```

上述语法规则除了 `[capture list]` 中的内容外，其他都是容易理解的，只是普通函数的函数名被省略了。返回值以 `->` 的形式出现（我们在上一节的尾部返回类型中已经提到这一点）。

被调用的捕获列表可以理解为一种参数类型。默认情况下，`Lambda` 表达式的内部函数体无法使用函数体外部的变量。此时，

捕获列表可以用于传递外部数据。根据传递的行为，捕获列表还分为以下类型：

- 1. 值捕获 类似于参数传递，值捕获基于变量可以复制的事实，不同在于被捕获的变量是在 `Lambda` 表达式创建时复制的，而不是在调用时：

```cpp
void lambda_value_capture() {
    int value = 1;
    auto copy_value = [value]() {
        return value;
    };
    value = 100;
    auto stored_value = copy_value();
    std::cout << "stored_value = " << stored_value << std::endl;
    // 此时，stored_value == 1，而 value == 100。
    // 因为 copy_value 在它创建时已经被复制了。
}
```

- 2. 引用捕获 类似于引用传递，引用捕获保存引用且值会变化：

```cpp
void lambda_reference_capture() {
    int value = 1;
    auto copy_value = [&value]() {
        return value;
    };
    value = 100;
    auto stored_value = copy_value();
    std::cout << "stored_value = " << stored_value << std::endl;
    // 此时，stored_value == 100，value == 100。
    // 因为 copy_value 保存了引用
}
```

- 3. 隐式捕获 手动编写捕获列表有时是复杂的。这种机械工作可以由编译器处理。此时，你可以向编译器写入 `&` 或 `=` 来声明引用捕获或值捕获。

总结来说，捕获提供了 `Lambda` 表达式使用外部值的能力。四种常见的捕获列表形式可以是：

- 空捕获列表
- `[name1,name2, ...]` 捕获一系列变量
- `[&]` 引用捕获，让编译器自己推导引用列表
- `[=]` 值捕获，让编译器自己推导值列表

#### 4. 表达式

上一节提到捕获列表可以理解为一种参数类型。默认情况下，`Lambda` 表达式的内部函数体无法使用函数体外部的变量。此时，捕获列表可以用于传递外部数据。

本节讨论泛型 `Lambda` 表达式。在 `C++14` 中，`auto` 关键字可以用于参数列表：

```cpp
void lambda_generic() {
    auto generic = [](auto x, auto y) {
        return x + y;
    };
    std::cout << generic(1, 2) << std::endl;
}
```

### 3.2 对象封装

虽然这些特性属于标准库而非位于运行时，但它增强了 `C++` 的运行时能力。这部分内容也非常重要，所以放在这里介绍。

#### std::function

`Lambda` 表达式的本质是一个类类型的对象（称为闭包类型），它类似于函数类型（称为闭包对象）。当 `Lambda` 表达式的捕获列表为空时，闭包对象也可以转换为函数指针值，例如：

```cpp
#include <iostream>
using foo = void(*)(int); // 函数指针
void functional(foo f) {
  f(1);
}
int main() {
  auto f = [](int value) {
    std::cout << value << std::endl;
  };
  functional(f); // 通过函数指针调用
  f(1); // 通过 Lambda 表达式调用
  return 0;
}
```

`C++11` 的 `std::function` 是一种通用的多态函数封装器，其实例可以存储、拷贝任何可调的目标实体。它也是存在于 `C++` 中的。一种类型安全的包（相对而言，对函数指针的调用不是类型安全的），换句话说，是一个函数容器。当我们有一个函数容器时，可以更容易更容易将函数和函数指针作为对象处理。例如：

```cpp
#include <functional>
#include <iostream>
```

```cpp
int foo(int para) {
  return para;
}
```

```cpp
int main() {
  // std::function 封装了一个接收 int 参数并返回 int 值的函数
  std::function<int(int)> func = foo;

  int important = 10;
  std::function<int(int)> func2 = [&](int value) -> int {
    return 1+value+important;
  };

  std::cout << func(10) << std::endl;
  std::cout << func2(10) << std::endl;
}
```

`std::bind` 和 `std::placeholder` 用于绑定函数调用的参数。它解决了我们可能无法一次性获取函数所有参数的问题。通过此函数，部分调用参数被预先绑定到函数中成为一个新对象，然后在参数完备后完成调用。例如：

```cpp
int foo(int a, int b, int c) {
  //
}
int main() {
  // 在函数 foo 上绑定参数 1, 2，并使用 std::placeholders::_1 作为
  // 第一个参数的占位符
  auto bindFoo = std::bind(foo, std::placeholders::_1, 1,2);
  // 调用 bindFoo 时，我们只需要一个参数
  bindFoo();
}
```

> 提示：`auto` 关键字的魔力。有时我们可能熟悉函数的返回类型，但可以使用 `auto` 来规避这个问题。

### 3.3 rvalue Reference（右值引用）

右值引用（`rvalue references`）是 `C++11` 引入的重要特性之一，与 `Lambda` 表达式同义。它的引入解决了 `C++` 中大量的历史遗留问题。它消除了诸如 `std::vector`、`std::string` 等额外开销，并使得函数对象容器 `std::function` 成为可能。

#### lvalue, rvalue, prvalue, xvalue

要理解什么是右值引用，你必须对 `lvalue` 和 `rvalue` 有清晰的理解。

`lvalue`（左值），顾名思义，是指赋值符号左侧的值。准确来说，`lvalue` 是一个在表达式（不一定是赋值表达式）之后仍然存在的持久性对象。

`Rvalue`（右值），右侧的值指的是在表达式结束后就不再存在的临时对象。

在 `C++11` 中，为了引入强大的右值引用，右值值的概念被进一步划分为：`prvalue` 和 `xvalue`。

`prvalue`（纯右值，pure rvalue），完全的右值，要么是纯粹的，如 `10`、`true`；要么求值结果等同于字面量或匿名临时变量，例如 `1+2`。非引用返回的临时变量、操作表达式生成的临时变量、原始字面量以及 `Lambda` 表达式都是纯右值。

注意，字符串字面量在类中会变成 `rvalue`，在其他情况下仍保持为 `lvalue`（例如，在函数中）。

```cpp
class Foo {
  const char*& right = "this is a rvalue";

public:
  void bar() {
    right = "still rvalue"; // 字符串字面量是一个 rvalue
  }
};

int main() {
  const char* const &left = "this is an lvalue"; // 字符串字面量是一个 lvalue
}
```

`xvalue`（将亡右值，expiring rvalue）是 `C++11` 为引入右值引用提出的概念（在传统的 `C++` 中，`prvalue` 和 `rvalue` 是同一个概念），指一个会被销毁但可以移动的值。

理解 `xvalue` 可能会困难，让我们来看像这样的代码：

```cpp
std::vector<int> foo() {
  std::vector<int> temp = {1, 2, 3, 4};
  return temp;
}

std::vector<int> v = foo();
```

在代码中，就传统的理解而言，函数的返回值 `temp` 在内部被创建并赋值给 `v`，而 `v` 获得了这个对象，整个 `temp` 被复制了。然后销毁 `temp`。如果这个 `temp` 很大，将导致产生大量的额外开销（这是传统 `C++` 受批评的问题之一）。

在最后一行中，`v` 是 `lvalue`，而 `foo()` 的返回值是 `rvalue`（也是纯右值）。然而，`v` 可以被其他变量捕获，`foo()` 的返回值被用作临时值。一旦离开 `v`，它将被销毁，且无法获取或修改。`xvalue` 定义了一种行为，使得临时值可以在被识别的同时仍被移动。在 `C++11` 之后，编译器为我们做了一些工作，让 `lvalue` 经历了这种隐式的右值转换，等同于 `static_cast<std::vector<int>&&>(temp)`，这里移动了局部返回的值。

#### rvalue reference and lvalue reference

要创建一个 `xvalue`，你需要声明右值引用：`T&&`，其中 `T` 是类型。右值引用的语句扩展了这个临时值的生命周期，只要变量存，它就会持续存在。`C++11` 提供了 `std::move` 方法无条件地将 `lvalue` 转换为 `rvalues`。通过它，我们可以获得一个临时右值对象，例如：

```cpp
#include <iostream>
#include <string>

void reference(std::string& str) {
    std::cout << "lvalue" << std::endl;
}
void reference(std::string&& str) {
    std::cout << "rvalue" << std::endl;
}

int main() {
    std::string l1 = "string"; // l1 是一个 lvalue
    std::string&& r1 = l1; // 非法，右值不能引用左值
    std::string&& rv1 = std::move(l1); // 合法，std::move 可以将 lvalue 转换为 rvalue
    std::cout << rv1 << std::endl;

    const std::string& lv2 = l1; // 合法，const 左值引用可以扩展变量生命周期
    lv2 += "Test"; // 非法，const 引用不能修改
    std::cout << lv2 << std::endl;

    std::string& rv2 = l1 + l2; // 合法，右值引用扩展生命周期
    rv2 += "string"; // 非法，非 const 引用可以修改
    std::cout << rv2 << std::endl;

    reference(rv2); // 输出: lvalue
    return 0;
}
```

`rv2` 指的是一个 `rvalue`，但由于它是一个引用，`rv2` 仍然是一个 `lvalue`。注意这里有一个有趣的历史性问题，让我们来看下面的代码：

```cpp
rv2 refers to an rvalue,但由于它是一个引用，rv2 仍然是一个 lvalue. Note that there is a very interesting historical issue, let's look at the following code:

#include <iostream>

int main() {
    int &a = std::move(1); // 非法，非 const 左值引用绑定右值
    const int &b = std::move(1); // 合法，const 左值引用可以
    std::cout << b << std::endl;
}
```

- 1. 首先构造两个作为返回右值（as-return-rvalue）的 `A` 对象，并获取这两个构造函数的输出；
- 2. 函数返回后，它将生成一个 `xvalue`，它被 `A` 的移动结构（`A&&`）引用，从而扩展其生命周期，并将右值中的指针保存到 `obj` 中。在移动操作过程中，指向值的指针被设置为 `nullptr`，这防止了区域被销毁。

这避免了无意义的拷贝构造并提升了性能。让我们来看涉及标准库的示例：

```cpp
#include <iostream> // std::cout
#include <utility> // std::move
#include <vector> // std::vector
#include <string> // std::string

int main() {

    std::string str = "Hello world.";
    std::vector<std::string> v;

    // push_back(const T&), copy
    v.push_back(str);
    // "str: Hello world."
    std::cout << "str: " << str << std::endl;

    // push_back(const T&), no copy
    // 字符串将被移动到 vector 中，因此 std::move 可以减少拷贝成本
    v.push_back(std::move(str));
    // str 现在是空的
    std::cout << "str: " << str << std::endl;

    return 0;
}
```

#### 完美转发 (Perfect forwarding)

正如我们之前提到的，声明的右值引用实际上是一个左值（`lvalue`）。这为我们进行参数化（传递）造成了问题：

```cpp
#include <iostream>
#include <utility>
void reference(int& v) {
    std::cout << "lvalue reference" << std::endl;
}
void reference(int&& v) {
    std::cout << "rvalue reference" << std::endl;
}
template <typename T>
void pass(T& v) {
    std::cout << " normal param passing: ";
    reference(v);
}
int main() {
    std::cout << "rvalue pass:" << std::endl;
    pass(1);

    int l = 1;
    pass(l);

    return 0;
}
```

对于 `pass(1)`，虽然值是右值，但 `v` 是一个引用，它也是一个左值。因此 `reference(v)` 将调用 `reference(int&)` 并输出 `lvalue`。对于 `pass(1)`，`1` 是一个右值，为什么它能成功地传递给 `pass(T& v)` 呢？

这是基于引用折叠规则（reference collapsing rule）：在传统的 `C++` 中，我们无法继续引用引用类型。然而，`C++` 随着右值引用的出现放宽了这一限制，产生了引用折叠规则，允许我们使用左值引用和右值引用。但必须遵循以下规则：

| 函数参数类型 | 实际参数类型 | 推导后的函数参数类型 |
|---|---|---|
| `T&` | `lvalue ref` | `T&` |
| `T&` | `rvalue ref` | `T&` |
| `T&&` | `lvalue ref` | `T&` |
| `T&&` | `rvalue ref` | `T&` |
