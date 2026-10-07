

# 第 02 章：语言易性增强

## 2.2 变量与初始化

在上面的代码中，我们可以看到 `itr` 变量定义在整个 `main()` 作用范围内，这导致我们在再次遍历 `std::vectors` 时必须重命名其他变量。C++17 消除了这一限制，使得我们可以在 `if`（或 `switch`）语句中这样做：

```cpp
if (const std::vector<int>::iterator itr = std::find(vec.begin(), vec.end(), 3);
    itr = vec.end()) {
    *itr = 4;
}
```

这类似于 Go 语言吗？

### 初始化列表

初始化是一项非常重要的语言特性，最常见的是对象初始化。在传统的 C++ 中，不同的对象有不同的初始化方法，例如普通数组、POD（普通旧数据，没有构造函数、析构函数和虚函数的类）、struct 类型可以使用 `{}` 初始化，这就是我们所说的初始化列表。对于类对象的初始化，你需要使用拷贝构造函数，或者使用 `()`。这些不同的方法彼此是相互特定的，无法通用的。例如：

```cpp
#include <iostream>
#include <vector>
```

class Foo {
public:
    int value_a;
    int value_b;
    Foo(int a, int b) : value_a(a), value_b(b) {}
};

int main() {
    // C++11 
    int arr[3] = {1, 2, 3};
    Foo foo(1, 2);
    std::vector<int> vec = {1, 2, 3, 4, 5};

    std::cout << "arr[0]:" << arr[0] << std::endl;
    std::cout << "foo:" << foo.value_a << ", " << foo.value_b << std::endl;
    for (std::vector<int>::iterator it = vec.begin(); it != vec.end(); ++it) {
        std::cout << *it << std::endl;
    }
    return 0;
}
```

为了解决这个问题，C++11 首先将初始化列表的概念绑定到类型，并称之为 `std::initializer_list`，允许构造函数或其他函数使用初始化列表作为参数，其中类对象的初始化为普通数组和 POD 初始化方法之间提供了一个统一的桥梁，如下：

```cpp
#include <initializer_list>
#include <vector>
class MagicFoo {
public:
    std::vector<int> vec;
    MagicFoo(std::initializer_list<int> list) {
        for (std::initializer_list<int>::iterator it = list.begin(); it != list.end(); ++it) {
            vec.push_back(*it);
        }
    }
};
int main() {
    // C++11 之后
    MagicFoo magicFoo = {1, 2, 3, 4, 5};
    std::cout << "MagicFoo: ";
    for (std::vector<int>::iterator it = magicFoo.vec.begin(); it != magicFoo.vec.end(); ++it) std::cout << *it << "";
}
```

该构造函数可以初始化列表构造函数，并且带有该构造函数的类型在初始化期间会被特殊对待。

除了对象构造外，初始化列表还可以作为普通函数的形参，例如：

```cpp
public:
    void foo(std::initializer_list<int> list) {
        for (std::initializer_list<int>::iterator it = list.begin(); it != list.end(); ++it) {};
    }
magicFoo.foo({6,7,8,9});
```

其次，C++11 还为任意对象的初始化提供了统一的语法，例如：

```cpp
Foo foo {3, 4};

## 2.3 类型推导

### 结构化绑定

结构化绑定提供了类似于其他语言多返回值的功能。在容器章节中，我们将学习 C++11 添加了 `std::tuple` 容器来构造多个值的返回值。但缺陷是 C++11/14 没有提供一种简单的方法从 `tuple` 中获取并定义元素，尽管可以使用 `std::tie` 进行解包。我们仍然必须非常清楚 `tuple` 包含多少对象、每个对象是什么，这非常麻烦。C++17 完成了这一点，结构化绑定允许我们编写如下代码：

```cpp
#include <iostream>
#include <tuple>

std::tuple<int, double, std::string> f() {
    return std::make_tuple(1, 2, "456");
}

int main() {
    auto [x, y, z] = f();
    std::cout << x << " " << y << " " << z << std::endl;
    return 0;
}
```

`auto` 在类型推导章节中描述。在传统的 C 和 C++ 中，类型必须明确定义，这并没有帮助我们快速编码，特别是面对大量复杂类型时，必须指示变量类型。这不仅降低了我们的开发效率，还让代码变得冗长。

C++11 引入了 `auto` 和 `decltype` 两个关键字来实现类型推导，让 C++ 与其他语言一样，不再担心变量类型。

#### auto

`auto` 在 C++ 中已经存在很久，但它一直是类型的指示器。在传统的 C++ 中，如果变量没有声明为 `auto`。随着 `auto` 被弃用（在 C++17 之后作为保留关键字），语义的改变变得非常自然。使用 `auto` 进行类型推导最常见且值得注意的例子是在之前的章节中：

```cpp
// C++11 之前
vector<int>::const_iterator it = vec.begin(); it != vec.end();
```

当我们有：

```cpp
#include <initializer_list>
#include <vector>
#include <iostream>

class MagicFoo {
public:
    std::vector<int> vec;
    MagicFoo(std::initializer_list<int> list) {
        for (auto it = list.begin(); it != list.end(); ++it) {
            vec.push_back(*it);
        }
    }
};

int main() {
    MagicFoo magicFoo = {1, 2, 3, 4, 5};
    std::cout << "MagicFoo: ";
    for (auto it = magicFoo.vec.begin(); it != magicFoo.vec.end(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;
    return 0;
}
```

一些常见的用法：

```cpp
auto i = 5; // 作为 int
auto arr = 10; // 作为 int
```

注意：`auto` 不能用于函数参数，因此以下编译是不可能的（考虑到重载，我们应该使用模板）：

```cpp
int add(auto x, auto y);
// 2.6.auto.cpp:16:9: error: 'auto' not allowed in prototype
```

此外，`auto` 不能用于推导数组类型：

```cpp
auto arr2[10]; // 非法，无法推导数组类型
// 2.6.auto.cpp:30:19: error: 'arr2' declared as array of 'auto'
```

#### decltype

`decltype` 关键字用于解决 `auto` 只能类型变量缺陷。它的用法类似于 `typeof`。有时我们需要计算表达式的类型，例如：

```cpp
auto x = 1;
auto y = 2;
decltype(x+y) z;
```

你已经在上一个例子中看到 `decltype` 用于推断类型的用法。下面的示例用于判断上述变量 `x, y, z` 是否为同一类型：

```cpp
if (std::is_same<decltype(x), int>::value)
  std::cout << "type x == int" << std::endl;
if (std::is_same<decltype(y), float>::value)
  std::cout << "type y == float" << std::endl;
if (std::is_same<decltype(x), decltype(z)>::value)
  std::cout << "type z == type x" << std::endl;
```

其中，`std::is_same<T, U>` 用于判断两个类型 `T` 和 `U` 是否相等。输出是：

```
type x == int
type z == type x
```

#### 后置类型推导

你可能认为，当我们引入 `auto` 时，已经提到过 `auto` 不能用于函数参数的类型推导。`auto` 可以推导函数的返回类型吗？仍然考虑 `add` 函数的例子，我们必须在传统的 C++ 中这样写：

```cpp
template<typename R, typename T, typename U>
R add(T x, U y) {
  return x+y;
}
```

注意：在模板参数列表中，`typename` 和 `class` 没有任何区别。在 `typename` 出现之前，使用 `class` 来定义模板参数。然而，当定义模板中的嵌套依赖类型时，你需要使用 `typename` 来消除歧义。

这种代码实际上非常丑，因为程序员在使用这个模板函数时必须显式指示返回类型。事实上我们不知道 `add()` 函数将执行什么操作，以及要获取什么类型的返回值。

这个问题在 C++11 中得到了解决。尽管你可能立即反应可以使用 `decltype` 来推导 `x+y` 的类型，但我们编写如下代码：

```cpp
decltype(x+y) add(T x, U y)
```

但实际上，这种写法无法编译。这是因为在读取 `decltype(x+y)` 时，`x` 和 `y` 还没有定义。为了解决这个问题，C++11 还提供了后置返回类型，它使用 `auto` 后置返回类型：

```cpp
template<typename T, typename U>
add2(T x, U y) -> decltype(x+y){
  return x + y;
}
```

好消息是，从 C++14 开始，可以直接推导普通函数的返回值的，所以这种方式是合法的：

```cpp
template<typename T, typename U>
add3(T x, U y) {
  return x + y;
}
```

