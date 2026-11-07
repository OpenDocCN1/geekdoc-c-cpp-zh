
```text
/usr/bin/.../lib/gcc/x86_64-linux-gnu/10/../../../.../include/c++/10/bits/range_access.h:934:37: note: because 'iterator_t<MyArray<int, 7> &>' (aka 'Iterator<int>') does not satisfy 'random_access_iterator'
        = bidirectional_range<_Tp> && random_access_iterator<iterator_t<_Tp>>;
                                      ^

/usr/bin/.../lib/gcc/x86_64-linux-gnu/10/../../../.../include/c++/10/bits/iterator_concepts.h:614:10: note: because 'derived_from<__detail::__iter_concept<Iterator<int> >, std::random_access_iterator_tag>' evaluated to false
    && derived_from<__detail::__iter_concept<_Iter>,
       ^

/usr/bin/.../lib/gcc/x86_64-linux-gnu/10/../../../.../include/c++/10/concepts:67:28: note: because '__is_base_of(std::random_access_iterator_tag, std::bidirectional_iterator_tag)' evaluated to false
    concept derived_from = __is_base_of(_Base, _Derived)
                           ^

/usr/bin/.../lib/gcc/x86_64-linux-gnu/10/../../../.../include/c++/10/bits/ranges_algo.h:2019:7: note: candidate function template not viable: requires at least 2 arguments, but 1 was provided
        operator()(_Iter __first, _Sent __last,
        ^

1 error generated.
```

## 15.10 模板类型参数的默认实参

类型参数也可以指定默认类型实参。例如，C++ 标准中的 **栈容器适配器** 类模板开头为：

```cpp
template <class T, class Container = deque<T>>
```

它指定 stack 默认使用 deque 来存储类型为 T 的 stack 元素。当编译器看到声明

```cpp
stack<int> values;
```

时，它会实例化 **int 类型的 stack 类模板**，并使用得到的特化来实例化名为 values 的对象。stack 的元素存储在 **deque<int>** 中。

默认类型参数必须是模板类型参数列表中最右侧（尾部）的参数。当使用两个或更多默认实参实例化模板时，如果省略的实参不是最右侧的，那么它右侧的所有类型参数也必须省略。**在函数模板中，可以为模板类型参数使用默认类型实参。**

## 15.11 变量模板

你已经实例化函数模板和类模板，分别用于定义一组相关函数和一组相关类。可以使用变量模板定义一组相关变量。你在图 15.6 的类型特征演示中使用了几个预定义变量模板。C++ 标准库提供了方便的 **用于访问每个类型特征 value 成员的变量模板**。例如，变量模板：

```cpp
is_arithmetic_v<T>
```

在标准中定义为

```cpp
template<class T>
inline constexpr bool is_arithmetic_v = is_arithmetic<T>::value;
```

这个变量模板定义了一个 **内联 bool** 变量，其求值结果为 **编译期常量**（由 constexpr 表示）。C++ 添加内联变量是为了更好地支持仅头文件库，这类库可以包含在同一应用程序的多个源代码文件（即翻译单元）中。当在头文件中定义常规变量时，在同一应用程序中多次包含该头文件会导致该变量出现多重定义错误。另一方面，**允许在同一应用程序的独立翻译单元中出现相同的内联变量定义**。

83. Alex Pomeranz，“6.8——全局常量与内联变量”，2020 年 1 月 3 日。访问于 2023 年 4 月 18 日。https://www.learncpp.com/cpp-tutorial/global-constants-and-inline-variables/。

84. “inline 说明符。”访问于 2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/language/inline。

## 15.12 可变参数模板与折叠表达式

在 C++11 之前，每个类模板或函数模板都有固定数量的模板参数。定义具有不同数量模板参数的类模板或函数模板需要为每种情况分别提供模板定义。**可变参数模板接受任意数量的实参。** 它们简化了模板编程，因为你可以提供一个可变参数函数模板，而不必提供许多具有不同参数数量的重载版本。

### 15.12.1 tuple 可变参数类模板

tuple 类（来自头文件 <tuple>）是类 **模板 pair**（在第 13.11 节介绍）的可变参数类模板泛化。tuple 是相关值的集合，这些值可能具有混合类型。图 15.13 演示了 tuple 的几项功能。第 9 行的 using 声明为以下类型定义了别名 Part：

```cpp
std::tuple<int, std::string, int, double>
```

这称为别名声明，使你能够为复杂类型创建方便的名称。

```cpp
// fig15_13.cpp
// Manipulating tuples.
#include <format>
#include <iostream>
#include <string>
#include <tuple>

// type alias for a tuple representing a hardware part's inventory
using Part = std::tuple<int, std::string, int, double>;
```

**图 15.13** | 操作 tuple。（第 1 部分，共 2 部分。）

```cpp
// return a part's inventory tuple
Part getInventory(int partNumber) {
    using namespace std::string_literals; // for string object literals

    switch (partNumber) {
    case 1:
        return {1, "Hammer"s, 32, 9.95}; // return a Part tuple
    case 2:
        return {2, "Screwdriver"s, 106, 6.99}; // return a Part tuple
    default:
        return {0, "INVALID PART"s, 0, 0.0}; // return a Part tuple
    }
}

int main() {
    // display the hardware part inventory
    for (int i{1}; i <= 2; ++i) {
        // unpack the returned tuple into four variables;
        // variables' types are inferred from the tuple's element values
        auto [partNumber, partName, quantity, price] {getInventory(i)};

        std::cout << std::format("{}: {}, {}: {}, {}: {:.2f}\n",
            "Part number", partNumber, "Tool", partName,
            "Quantity", quantity, "Price", price);
    }

    std::cout << "\nAccessing a tuple's elements by index number:\n";
    auto hammer{getInventory(1)};
    std::cout << std::format("{}: {}, {}: {}, {}: {:.2f}\n",
        "Part number", std::get<0>(hammer), "Tool", std::get<1>(hammer),
        "Quantity", std::get<2>(hammer), "Price", std::get<3>(hammer));

    std::cout << std::format("A Part tuple has {} elements\n",
        std::tuple_size_v<Part>); // get the tuple size
}
```

```text
Part number: 1, Tool: Hammer, Quantity: 32, Price: 9.95
Part number: 2, Tool: Screwdriver, Quantity: 106, Price: 6.99

Accessing a tuple's elements by index number:
Part number: 1, Tool: Hammer, Quantity: 32, Price: 9.95
A Part tuple has 4 elements
```

**图 15.13** | 操作 tuple。（第 2 部分，共 2 部分。）

第 9 行的 using 声明创建了一个类型别名——为复杂类型提供的方便名称。别名 Part 表示用于硬件零件库存的 tuple。每个 Part 包含

- 一个 int 类型的零件编号，
- 一个 string 类型的零件名称，
- 一个 int 类型的数量，以及
- 一个 double 类型的价格。

在 tuple 声明中，每个模板类型参数都对应 tuple 中同一位置的值。tuple 元素的数量始终与类型参数的数量匹配。我们使用 Part 类型别名来简化其余代码。

#### 打包 tuple

创建 tuple 对象称为打包 tuple。第 12–23 行定义了一个 getInventory 函数，它接收零件编号并返回一个 Part tuple。该函数通过返回一个包含四个元素（一个 int、一个 string、一个 int 和一个 double）的初始化列表（第 17、19 和 21 行）来打包 Part tuple，编译器使用该列表初始化返回的 Part std::tuple 对象。tuple 的大小一旦创建就固定不变。

#### 使用 `std::make_tuple` 创建 tuple

还可以使用 tuple 头文件中的 make_tuple 函数来打包 tuple，该函数从函数实参推断 tuple 的类型参数。例如，可以用如下 make_tuple 调用来创建第 17、19 和 21 行中的 tuple：

```cpp
std::make_tuple(1, "Hammer", 32, 9.95)
```

如果采用这种方法，就可以将 getInventory 的返回类型指定为 **auto**，以便从 make_tuple 的结果推断返回类型。

#### 使用结构化绑定解包 tuple

使用结构化绑定（第 14.4.5 节），可以解包 tuple 以访问其元素。第 30 行将 Part 的成员解包到变量中，我们在第 32–34 行显示这些变量。

#### 使用 `get<index>` 按索引获取 tuple 成员

类模板 pair 包含公有成员 first 和 second，用于访问 pair 的两个成员。创建的每个 tuple 都可以包含任意数量的元素，因此 tuple 没有类似命名的数据成员。相反，`<tuple>` 头文件提供了函数模板 `get<index>(tupleObject)`，它返回对 `tupleObject` 在指定索引处成员的引用。第一个成员的索引为 0。第 38 行获取 hammer 库存的 tuple，然后第 39–41 行按索引访问每个 tuple 元素。

#### 使用 `get<type>` 按类型获取 tuple 成员

如果 tuple 中只包含一个特定类型的成员，则可以将 get 与类型实参一起使用来访问该 tuple 成员。例如，下面的语句获取 hammer tuple 的 string 成员：

```cpp
auto partName{get<std::string>(hammer)};
```

然而，下面的语句

```cpp
auto partNumber{get<int>(hammer)};
```

会生成编译错误，因为该调用是**有歧义的**——hammer tuple 包含两个 int 成员，分别表示零件编号和数量。

#### tuple 的其他功能

下表展示了 **tuple** 类模板的其他几项功能。有关 tuple 类模板的完整详细信息，请参阅

https://en.cppreference.com/w/cpp/utility/tuple/tuple

