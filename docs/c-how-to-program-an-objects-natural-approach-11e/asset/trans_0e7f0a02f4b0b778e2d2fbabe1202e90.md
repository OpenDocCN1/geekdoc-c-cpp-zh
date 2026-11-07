
**约束表达式**是一个编译期逻辑表达式，用于确定模板实参是否满足一组特定要求——在本例中，是整数或浮点类型。约束表达式通常包括预定义概念、类型特征，以及（如你将在 15.6.5 节中看到的）**requires 表达式**，后者使你能够指定其他要求。**Numeric** 概念的模板头有一个类型参数，表示要测试的类型。

具有多个模板参数的概念也可以指定类型之间的关系。[44] 例如，如果模板有两个类型参数，你可以使用预定义概念 **std::same_as** 来确保两个类型实参具有相同类型，如下所示：

```cpp
template<typename T, typename U>
    requires std::same_as<T, U>
// rest of template definition
```

在 15.12 节中，我们将介绍可变参数模板，它们可以拥有任意数量（类型或非类型）的模板实参。在那里，我们将在一个可变参数函数模板中使用 **std::same_as**，该模板要求其所有实参具有相同类型。

## 15.6.2 使用概念

定义概念后，你可以用四种方式之一来约束模板参数。这里展示前三种，第四种在 15.6.5 节展示。

### 位于模板头之后的 requires 子句

任何概念都可以放在模板头之后的 **requires** 子句中，就像我们在图 15.5 中所做的那样。下面是使用自定义概念 `Numeric<T>` 的 multiply 函数模板：

```cpp
template<typename T>
    requires Numeric<T>
T multiply(T first, T second) {return first * second;}
```

### 位于函数模板签名之后的 requires 子句

你也可以将 **requires** 子句放在函数模板签名之后、函数模板体之前，如下所示：

```cpp
template<typename T>
T multiply(T first, T second) requires Numeric<T> {
    return first * second;
}
```

尾置 **requires** 子句必须在两种场景中使用：[45]

- 在类模板体内定义的成员函数没有模板头，因此必须使用尾置 requires 子句。
- 要在约束中使用函数模板的参数名，必须使用尾置 requires 子句，以便在编译器求值 requires 子句之前，参数名已在作用域内。

### 将概念作为模板头中的类型

当你只有一个受概念约束的类型参数时，C++ 核心准则建议在模板头中用概念名代替 typename。[46] 这样做通过**消除 requires 子句：**简化了模板定义：

```cpp
template<Numeric T>
T multiply(T first, T second) {return first * second;}
```

现在，每个参数都必须满足概念 Numeric 的要求。该函数模板仍然只有一个类型参数，因此函数的实参必须具有相同类型；否则会发生编译错误。

## 15.6.3 在缩写函数模板中使用概念

图 15.3 介绍了缩写函数模板，其中的参数声明为 **auto**，以便编译器能够推断函数的参数类型。**在代码中任何可以使用 auto 的地方，都可以在它前面加上概念名来约束允许的类型。**[47] 这包括

- 缩写函数模板参数列表，
- 指定为函数返回类型的 auto，
- 从初始化器推断变量类型的 auto 局部变量定义，以及
- 泛型 lambda 表达式。

图 15.7 将 multiply 重新实现为**缩写函数模板**。在本例中，我们为每个参数使用了**受约束的 auto**，并使用我们的 **Numeric 概念**来限制可以作为实参传递的类型。我们还使用 **auto** 作为**返回类型**，因此编译器将从第 12 行表达式的类型推断它。

```cpp
// fig15_07.cpp
// Constrained multiply abbreviated function template.
#include <concepts>
#include <iostream>

// Numeric concept aggregates std::integral and std::floating_point
template<typename T>
concept Numeric = std::integral<T> || std::floating_point<T>;

// abbreviated function template with constrained auto
auto multiply(Numeric auto first, Numeric auto second) {
    return first * second;
}
```

**图 15.7** | 受约束的 multiply 缩写函数模板。（第 1 部分，共 2 部分。）

```cpp
int main() {
    std::cout << "Product of 5 and 3: " << multiply(5, 3)
        << "\nProduct of 7.25 and 2.0: " << multiply(7.25, 2.0)
        << "\nProduct of 5 and 7.25: " << multiply(5, 7.25) << "\n";
}
```

```text
Product of 5 and 3: 15
Product of 7.25 and 2.0: 14.5
Product of 5 and 7.25: 36.25
```

**图 15.7** | 受约束的 `multiply` 缩写函数模板。（第 2 部分，共 2 部分。）

这个**缩写函数模板**与 15.4.2 节中受约束的 `multiply` 函数模板之间的关键区别在于，编译器将第 11 行中的每个 **auto** 视为一个**单独的模板类型参数**。因此，first 和 second 可以具有**不同的数据类型**，如第 18 行所示，它传递了一个 `int` 和一个 `double`。我们之前受概念约束的 `multiply` 版本会对不同类型的实参产生编译错误。第 11–13 行实际上等价于一个具有**两个类型参数**的模板：

```cpp
template<Numeric T1, Numeric T2>
auto multiply(T1 first, T2 second) { return first * second;}
```

如果你要求两个或更多参数具有相同类型，

- 使用常规函数模板而不是缩写函数模板，并且
- 对每个必须具有相同类型的函数参数使用相同的类型参数名。

## 15.6.4 基于概念的重载

函数模板与重载密切相关。**当重载函数对不同类型执行语法上相同的操作时，可以使用函数模板更紧凑、更方便地表达它们。** 然后，你可以编写具有不同实参类型的函数调用，并让编译器为每个函数调用适当地实例化模板。这些实例化都具有相同的函数名，因此编译器使用**重载解析**来调用正确的那个。

### 重载函数的匹配过程

在确定要调用哪个函数时，编译器会查看函数和函数模板，以定位与调用匹配的现有函数，或生成与调用匹配的函数模板特化：

- 如果没有匹配项，编译器会发出错误消息。
- 如果函数调用有**多个匹配项**，编译器会尝试确定**最佳匹配**。
- 如果**最佳匹配不止一个**，则该调用是**有歧义的**，编译器会发出错误消息。

### 重载函数模板

你也可以重载函数模板。例如，你可以提供具有不同签名的其他函数模板。还可以通过提供具有相同函数名但不同参数的非模板函数来重载函数模板。

### 使用概念重载函数模板

在 C++20 中，你可以在函数模板中使用概念，根据类型要求选择重载。[50] 考虑来自 `<iterator>` 头文件的标准函数 `std::distance` 和 `std::advance`——它们各自通过迭代器对容器进行操作：

- `std::distance` 计算两个迭代器之间的元素数量。[51]
- `std::advance` 将迭代器从其当前位置向前移动 *n* 个位置。[52]

这些操作中的每一个都可以实现为 *O(n)* 操作：

- `std::distance` 可以使用 ++ 从开始迭代器迭代到结束迭代器（但不包括结束迭代器），并统计递增次数（*n*）。
- `std::advance` 可以循环 *n* 次，每次循环迭代将迭代器递增一次。

某些算法可以针对特定迭代器类型进行优化。对于*随机访问迭代器*，`std::distance` 和 `std::advance` 都可以实现为 *O(1)* 操作：

- `std::distance` 可以使用 operator- 从结束迭代器中减去开始迭代器，以一次操作计算迭代器之间的项数。
- `std::advance` 可以使用 operator+ 将一个整数 *n* 加到一个迭代器上，以一次操作将迭代器向前移动 *n* 个位置。

图 15.8 实现了**重载的 `customDistance` 函数模板**。每个模板都需要两个迭代器实参，并计算它们之间的元素数量。我们使用基于概念的重载（也称为概念重载），使编译器能够根据我们用来约束每个模板参数的概念，在**这些重载之间进行选择**。

```cpp
// fig15_08.cpp
// Using concepts to select overloads.
#include <array>
#include <iostream>
#include <iterator>
#include <list>
```

**图 15.8** | 使用概念选择重载。（第 1 部分，共 2 部分。）

- 44. Bjarne Stroustrup，“概念：泛型编程的未来——3.1 指定模板接口，”2017 年 1 月 31 日。访问于 2023 年 4 月 18 日，https://wg21.link/p0557r0。
- 45. “向模板应用约束的三种方式之间有什么区别？”访问于 2023 年 4 月 18 日。https://stackoverflow.com/a/61875483。[注：原始 stackoverflow.com 问题提到了向模板应用约束的三种方式，但实际上有四种，引用的回答中提到了每一种。]
- 46. C++ 核心准则，“T.13：对于简单的单类型实参概念，优先使用简写表示法。”访问于 2023 年 4 月 18 日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#t-shorthand。
- 47. “占位符类型说明符。”访问于 2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/language/auto。
- 48. 编译器解析函数调用的过程很复杂。完整细节在 C++ 标准“12.2 重载解析。”中讨论。访问于 2023 年 4 月 18 日。https://timsong-cpp.github.io/cppwp/n4861/over.match。
- 49. Jeff Preshing，“C++ 如何解析函数调用。”2021 年 3 月 15 日。访问于 2023 年 5 月 7 日。https://preshing.com/20210315/how-cpp-resolves-a-function-call/。
- 50. Bjarne Stroustrup，“概念：泛型编程的未来——6. 概念重载，”2017 年 1 月 31 日。访问于 2023 年 4 月 18 日。http://wg21.link/p0557r0。
- 51. “std::distance。”访问于 2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/iterator/distance。
- 52. “std::advance。”访问于 2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/iterator/advance。
