
一个例子是 `ranges::sized_range` 概念。它要求必须能够在 O(1) 时间内计算范围的大小。提供 `size()` 的容器通常满足这一点——至少可以这样假定。然而，如果你自己编写一个 File 容器，它有一个并非在 O(1) 时间内工作的 `size()` 方法，那么这个容器就不应满足 `sized_range` 概念。这是一种语义约束。

因此，`ranges::sized_range` 概念还会检查 `disable_sized_range<...>` 表达式是否已定义——或者更准确地说：

```
constexpr bool std::ranges::disable_sized_range<...> = true;
```

因此，你可以使用自己的定义来传达容器的语义，而 `sized_range` 这一语义概念会注意到它。

## 23.4.5 阶段性小结

概念是为类型和表达式定义要求的一种方式。以下是一些补充建议：

- 为你的概念编写文档。
- 优先使用具名概念。仅名称本身就是一份文档，而且有助于复用。经验法则：你是否正要写 `<typename ...>` 或 `<class ...>`？很可能最好写成 `<SomeConcept ...>`。
- 使用标准库概念。
- 利用概念改进错误消息。
- 将概念应用于你用 `auto` 声明的局部变量。
- 不要让你的概念过于复杂。
- 始终一致地格式化概念。遵循你工作环境的约定。

## 23.5 模板类

模板技术正如你刚刚通过函数模板学到的那样，并不限于函数，也可以用于类。准确地说，如果没有类模板，C++ 就不会像今天这样流行和受人喜爱。标准库定义了许多类模板，其中你已经使用过 `std::vector` 或 `std::string`。使用 `std::vector` 时，你在尖括号中指定了类型。另一方面，`std::string` 是 char 类型的实例化，其内部定义如下：

```
using string = basic_string<char>;
```

除了像 `std::vector`、`std::list` 等标准容器类之外，用于输入/输出的流类（见第 26 章）也大多实现为 `char` 的实例化。

### 23.5.1 实现类模板

首先，我想向你展示如何创建一个非常原始的容器（容器类），它可以容纳（几乎）任何类型。这里引入类模板同样使用以下语句：

```cpp
template <typename T>
```

同样，`T` 表示形式数据类型，编译器在实例化期间——即生成机器代码时——会用所需的类型替换它。名称 `T` 同样可以是任何有效标识符；`T` 在这里是非常常见的用法。你也可以使用 `<class T>` 代替 `<typename T>`。与函数模板一样，此时使用哪一种都没有区别。

从 C++20 起，你可以在这里使用概念代替 `typename`。这将是更简短且更受青睐的写法。另外，在这一行之后，也可以用 `requires` 指定对类型 `T` 的要求。

以下清单展示了一个完整类模板的定义。

```cpp
// https://godbolt.org/z/jqzTMxYk
template <std::copyable T>      // C++20 concept
class MyContainer {
    T data_;
public:
    void setData(const T& d) { data_ = d; }
    T getData() const { return data_; }
};
```

**清单 23.29** 类模板将类型作为形式参数。

一开始，我定义了一个 `MyContainer` 类模板，现在几乎可以像 `std::vector<T>` 那样定义它；当然，还缺少许多功能，但这已经可以用作理论上的比较。我用 copyable 这一 C++20 概念对 `T` 进行了合理的限制。不过，你也可以直接写 `typename` 或 `class`。如果你现在创建一个像 `MyContainer<int>` 这样的对象，编译器会把所有形式数据类型（这里是 `T`）替换为 `int`，并相应地生成机器代码。你很快就会进一步了解如何将对象实例化为类模板。

### 23.5.2 实现类模板的方法

在最近创建的 `MyContainer<T>` 类模板示例中，你可以看到，完全可以在方法的参数（如 `setData`）或返回值（如 `getData`）中设置形式数据类型。

> **优先以引用或指针传递模板类型的参数**
>
> 这里还缺少一条建议：像 `setData(const T&)` 示例中的值那样，应通过引用（或指针）传递，而不是按副本传递。因为如果类模板与对象一起使用，可能会累积大量数据，而这些数据随后会被不必要地放到栈上再移除。不过，对于模板函数和模板类，你必须比平时更仔细地考虑是要按值传递参数还是按引用传递参数。

在实践中，只有当函数体确实非常短时，你才会在类模板定义内联编写方法定义。你已经知道如何在类外定义方法，但对于类模板的方法，情况要更特殊一些，因此需要在这里单独讨论。带有形式数据类型的类模板方法的语法如下：

```cpp
template <typename T>
void ClassName<T>::method( parameter ) { ... }
```

参照我们的 MyContainer 类模板，在类模板定义之外定义该方法将如下一清单所示。

```cpp
// https://godbolt.org/z/4K5WdoG8
template <std::copyable T>
class MyContainer {
    T data_;
public:
    void setData(const T& d);
    T getData() const;
};
template <std::copyable T>
void MyContainer<T>::setData(const T& d) {
    data_ = d;
}
template <std::copyable T>
T MyContainer<T>::getData() const {
    return data_;
}
```

**清单 23.30** 类模板体之外的方法定义在语法上稍微复杂一些。

重要的是，对于类模板的方法，你还要在类名之后的尖括号中（这里是 `<T>`）指定形式数据类型，如 `MyContainer<T>::...` 所示。像 `MyContainer<T>` 这样的指定对应于指定一个完整类型。“空的” `MyContainer` 仅仅是一个模板名称。

### 初步定义

与函数模板一样，方法的定义只是初步定义；该类型仍然不完整，因为它只包含一个形式数据类型。实际的方法只有在你实例化类模板的对象时才会生成——也就是说，在你首次使用它时，即用具体类型指定它时。

### 重写（特化）方法

与函数模板一样，你可以根据需要，使用 `template<>` 和所需的数据类型来重写（*特化*）类模板的方法。此时，你必须为形式数据类型 `T` 指定实际数据类型，而不是 `MyContainer<T>`。你可以为 `setData()` 和 `getData()` 方法实现针对 `std::string` 的这种特化，如下一清单所示。

```cpp
// https://godbolt.org/z/M6earoWMn
#include <iostream>
#include <string>
#include <concepts>    // copyable, C++20
template <std::copyable T>
class MyContainer {
    T data_;
public:
    void setData(const T& d) { data_ = d; } // general case
    T getData() const { return data_; }     // general case
};
template<>
void MyContainer<std::string>::setData(const std::string& d) {
    data_ = "[" + d + "]";
}
int main() {
    MyContainer<std::string> mcString;
    mcString.setData("History");
    std::cout << mcString.getData() << '\n';  // Output: [History]
    MyContainer<int> mcInt;
    mcInt.setData(5);
    std::cout << mcInt.getData() << '\n';     // Output: 5
}
```

**清单 23.31** 像函数模板一样特化类模板方法。
