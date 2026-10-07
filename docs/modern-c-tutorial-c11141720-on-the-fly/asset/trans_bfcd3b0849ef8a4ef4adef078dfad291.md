

## 结论 第02 章：语言易用性增强

```cpp
std::cout << "new_enum::value3 == new_enum::value4" << std::endl;
}
```

在这种语法中，枚举类型后面跟着一个冒号和一个类型关键字，用于指定枚举中的枚举值，这允许我们为为枚举赋值（如果未指定，则默认使用 `int`）。

如果我们想要获取枚举值的值，将必须进行显式的类型转换，但我们可以重载 `<<` 运算符来输出它，你可以收集以下代码段：

```cpp
#include <iostream>
template<typename T>
std::ostream& operator<<(typename std::enable_if<std::is_enum<T>>::type&, std::ostream& stream, T value) {
    return stream << static_cast<typename std::underlying_type<T>::type>(value);
}
```

此时，以下代码将能够被编译：

```cpp
std::cout << new_enum::value3 << std::endl;
```

## 结论

本节介绍了现代 C++ 中语言用法的增强，我认为这些是几乎每个人都需要知道和使用的最重要的特性：

- 1. auto 类型推导
- 2. 迭代的作用域
- 3. 初始化列表
- 4. 变长参数模板

## 练习

1. 使用结构化绑定，仅用一行函数代码实现函数：

```cpp
#include <string>
#include <map>
#include <iostream>
template <typename Key, typename Value, typename F>
void update(std::map<Key, Value>& m, F foo) {
    // TODO:
}
```

```cpp
int main() {
    std::map<std::string, long long int> m {
        {"a", 1},
        {"b", 2},
        {"c", 3}
    };

    update(m, [] (std::string key) {
        return std::hash<std::string>{}(key);
    });
    for (auto& [key, value] : m) {
        std::cout << key << " : " << value << std::endl;
    }
}
```

- 2. 尝试使用折叠表达式（Fold Expression）实现一个计算平均值的函数，允许传递任何参数。

参考答案参见此处。

## 第03 章：语言运行时增强

### 3.1 Lambda 表达式

Lambda 表达式是现代 C++ 中最重要的特性之一，Lambda 表达式提供了类似匿名函数的功能。当需要函数但不想使用名称来调用函数时，就会使用匿名函数。实际上有很多很多这样的场景。因此，匿名函数几乎是现代编程语言的标配。

## 基础

Lambda 表达式的基本语法如下：

```cpp
[capture list] (parameter list) mutable(optional) exception attribute -> return type {
// 函数体
}
```

上述语法规则除了 `[capture list]` 中的内容外，其他都是容易理解的，只是普通函数的函数名被省略了。返回值以 `->` 的形式出现（我们在上一节的尾部返回类型中已经提到这一点）。

被调用的捕获列表可以理解为一种参数类型。默认情况下，Lambda 表达式的内部函数体无法使用函数体外部的变量。此时，

### 3.1 Lambda 表达式

捕获列表可以用于传递外部数据。根据传递的行为，捕获列表还分为以下类型：

- 1. 值捕获 类似于参数传递，值捕获基于变量可以复制的事实，不同在于被捕获的变量是在 Lambda 表达式创建时复制的，而不是在调用时：

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

总结来说，捕获提供了 Lambda 表达式使用外部值的能力。四种常见的捕获列表形式可以是：

- 空捕获列表

### 3.1 Lambda 表达式
## 第03 章：语言运行时增强

- [name1,name2, ...] 捕获一系列变量
- [&] 引用捕获，让编译器自己推导引用列表
- [=] 值捕获，让编译器自己推导值列表

### 4. 表达式

上一节提到捕获列表可以理解为一种参数类型。默认情况下，Lambda 表达式的内部函数体无法使用函数体外部的变量。此时，捕获列表可以用于传递外部数据。

本节讨论泛型 Lambda 表达式。在 C++14 中，`auto` 关键字可以用于参数列表：

```cpp
void lambda_generic() {
    auto generic = [](auto x, auto y) {
        return x + y;
    };
    std::cout << generic(1, 2) << std::endl;
}
```

### 3.2 对象封装
## 第03 章：语言运行时增强

```cpp
std::cout << generic(1.1, 2.2) << std::endl;
}
```

### 3.2 对象封装

虽然这些特性属于标准库而非位于运行时，但它增强了 C++ 的运行时能力。这部分内容也非常重要，所以放在这里介绍。

#### std::function

Lambda 表达式的本质是一个类类型的对象（称为闭包类型），它类似于函数类型（称为闭包对象）。当 Lambda 表达式的捕获列表为空时，闭包对象也可以转换为函数指针值，例如：

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

C++11 的 `std::function` 是一种通用的多态函数封装器，其实例可以存储、拷贝任何可调的目标实体。它也是存在于 C++ 中的。一种类型安全的包（相对而言，对函数指针的调用不是类型安全的），换句话说，是一个函数容器。当我们有一个函数容器时，可以更容易更容易将函数和函数指针作为对象处理。例如：

```cpp
#include <functional>
#include <iostream>
```

