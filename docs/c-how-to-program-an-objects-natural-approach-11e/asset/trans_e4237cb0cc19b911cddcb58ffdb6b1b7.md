
```cpp
std::string s1{"hi"};
std::string s2{"bye"};
auto result(multiply(s1, s2)); // string does not have * operator
```

类 `string` 不支持 `*` 运算符。如果我们将这些行添加到图 15.4 的 `main` 中并重新编译，我们会从首选编译器得到以下错误消息——为了可读性，我们添加了垂直间距。Clang 生成

```text
fig15_04.cpp:6:45: error: invalid operands to binary expression
('std::basic_string<char>' and 'std::basic_string<char>')
T multiply(T first, T second) { return first * second; }
                                      ~~~~~ ^ ~~~~~~

fig15_04.cpp:14:16: note: in instantiation of function template
specialization 'multiply<std::basic_string<char>>' requested here
auto result(multiply(s1, s2)); // string does not have * operator
                 ^
1 error generated.
```

GNU g++ 生成

```text
fig15_04.cpp: In instantiation of 'T multiply(T, T) [with T =
std::__cxx11::basic_string<char>]':
fig15_04.cpp:14:24:   required from here
fig15_04.cpp:6:45: error: no match for 'operator*' (operand types are
'std::__cxx11::basic_string<char>' and 'std::__cxx11::basic_string<char>')
    6 | T multiply(T first, T second) { return first * second; }
      |                                        ~~~~~~^~~~~~~~
```

Visual C++ 生成

```text
1>fig15_04.cpp
1>c:\pauldeitel\Documents\examples\ch15\fig15_04.cpp(6,45): error C2676: binary '*': 'std::string' does not define this operator or a conversion to a type acceptable to the predefined operator
1>          with
1>          [
1>              T=std::string
1>          ]
1>
1>c:\pauldeitel\Documents\examples\ch15\fig15_04.cpp(14): message : see reference to function template instantiation 'T multiply<std::string,T>()' being compiled
1>          with
1>          [
1>              T=std::string
1>          ]
1>Done building project "concurrencpp_test.vcxproj" -- FAILED.
```

这些错误相对较小且直接，但这并不典型。更复杂的模板往往会导致冗长的错误消息列表。例如，将错误类型的迭代器传递给一个未受概念约束的标准库算法，可能会产生数百行错误消息。我们尝试编译一个只包含以下两条简单语句的程序，这两条语句试图对 `std::list` 进行排序：

```cpp
std::list integers{10, 2, 33, 4, 7, 1, 80};
std::sort(integers.begin(), integers.end());
```

`std::list` 具有双向迭代器，但 `std::sort` 要求随机访问迭代器。我们的一个首选编译器为 `std::sort` 调用生成了超过 1,000 行错误消息。只需改用受概念约束的 `std::ranges::sort` 算法，产生的消息就会少得多，并表明需要随机访问迭代器。

## 15.4.2 带 C++20 概念 requires 子句的受约束函数模板

C++20 概念使您能够指定约束。每个约束都是一个在编译期求值为 true 或 false 的谓词表达式。<sup>35</sup> 编译器使用约束在实例化模板之前检查类型要求。C++ 核心准则建议

- 为每个模板参数指定概念<sup>36</sup>，并且
- 尽可能使用标准预定义的概念。<sup>37</sup>

您可以将概念应用于函数模板参数，以明确说明对应类型实参的要求。如果某个类型实参满足要求，编译器就会实例化该模板；否则，该模板会被忽略。当编译器找不到函数调用的匹配项时，概念相对于其部分或完全取代的先前技术的一个好处是，编译器通常会产生（可能少得多）更少、更精确的错误消息。

### requires 子句

图 15.5 使用 C++20 `requires` 子句（第 8 行）来约束 `multiply` 的模板参数 `T`。关键字 `requires` 后面跟着一个约束表达式，该表达式由一个或多个编译期 `bool` 表达式组成，并结合逻辑 `&&` 和 `||` 运算符。

```cpp
// fig15_05.cpp
// Constrained multiply function template that allows
// only integers and floating-point values.
#include <concepts>
#include <iostream>

template<typename T>
  requires std::integral<T> || std::floating_point<T>
T multiply(T first, T second) { return first * second; }
```

**图 15.5** | 受约束的 `multiply` 函数模板，仅允许整数和浮点值。输出显示了 g++ 编译器的错误消息。（第 1 部分，共 2 部分。）

35. C++ 标准，“13.5 模板约束”。访问于 2023 年 4 月 18 日。https://timsong-cpp.github.io/cppwp/n4861/temp.constr.

36. C++ 核心准则，“T.10：为所有模板实参指定概念”。访问于 2023 年 4 月 18 日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rt-concepts.

37. C++ 核心准则，“T.11：尽可能使用标准概念”。访问于 2023 年 4 月 18 日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rt-std-concepts.

```cpp
int main() {
    std::cout << "Product of 5 and 3: " << multiply(5, 3)
        << "\nProduct of 7.25 and 2.0: " << multiply(7.25, 2.0) << "\n";

    std::string s1{"hi"};
    std::string s2{"bye"};
    auto result{multiply(s1, s2)};
}
```

```text
fig15_05.cpp: In function ‘int main()’:
fig15_05.cpp:17:24: error: no matching function for call to
‘multiply(std::string&, std::string&)’
   17 |     auto result{multiply(s1, s2)};
      |                 ~~~~~~~~^~~~~~~~
fig15_05.cpp:9:3: note: candidate: ‘template<class T> requires (integral<T>) || (floating_point<T>) T multiply(T, T)’
    9 | T multiply(T first, T second) { return first * second; }
      |   ^~~~~~~~
fig15_05.cpp:9:3: note:   template argument deduction/substitution failed:
fig15_05.cpp:9:3: note: constraints not satisfied
fig15_05.cpp: In substitution of ‘template<class T> requires (integral<T>) || (floating_point<T>) T multiply(T, T) [with T = std::__cxx11::basic_string<char>]’:
fig15_05.cpp:17:24:   required from here
fig15_05.cpp:9:3:   required by the constraints of ‘template<class T> requires (integral<T>) || (floating_point<T>) T multiply(T, T)’
fig15_05.cpp:8:30: note: no operand of the disjunction is satisfied
    8 |     requires std::integral<T> || std::floating_point<T>
      |              ~~~~~~~~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~~~~~
```

**图 15.5** | 受约束的 `multiply` 函数模板，仅允许整数和浮点值。输出显示了 g++ 编译器的错误消息。（第 2 部分，共 2 部分。）

第 8 行指定有效的 `multiply` 类型实参必须满足以下概念之一，其中每个概念都是**对参数 `T` 的约束**：

- `std::integral<T>` 表示 `T` 可以是任意整数数据类型。
- `std::floating_point<T>` 表示 `T` 可以是任意浮点数据类型。

所有整数和浮点类型都支持算术运算符，因此我们知道这些类型的值可与第 9 行的 `*` 运算符配合使用。如果上述两个约束都不满足，则类型实参与 `multiply` 函数模板不兼容，编译器将不会实例化该模板。如果没有其他函数匹配该调用，编译器会生成错误消息。

你很快会看到，**有些概念指定了许多单独的约束。** 前面的概念来自头文件 `<concepts>`，它们是 C++20 的 74 个预定义概念中的两个。

38. C++ 标准，“库概念索引”。访问于 2023 年 4 月 18 日。https://timsong-cpp.github.io/cppwp/n4861/library/conceptindex.

15.4.3 节列出了预定义概念类别、每个类别中的概念以及定义它们的头文件。

### 析取与合取

在第 8 行中，逻辑 OR（`||`）运算符构成一个**析取**。至少有一个操作数必须为 true，编译器才会实例化该模板。如果两个操作数都为 false，编译器会忽略该模板，不将其视为对 `multiply` 调用的潜在匹配项。函数 `multiply` 只定义了一个类型参数，因此**两个操作数必须具有相同类型**。因此，在此示例中，对于每次 `multiply` 调用，第 8 行中只有一个概念可以为 true。

您可以使用逻辑 AND（`&&`）运算符构成一个**合取**，以表明两个操作数都必须为 true，编译器才会实例化该模板。析取和合取使用**短路求值**（4.11.3 节）。

### 用满足其约束的实参调用 multiply

第 12 行和第 13 行分别用两个 `int` 值和两个 `double` 值调用 `multiply`。当编译器查找与这些调用匹配的函数定义时，它只会遇到第 7–9 行中的 `multiply` 函数模板。它将检查实参的类型，以确定它们是否满足第 8 行 **requires 子句**中的任一概念。每次调用中的两个实参都满足该**析取**的要求之一，因此编译器将为第 12 行中的类型 `int` 和第 13 行中的类型 `double` 实例化该模板。再次强调，**multiply 只有一个类型参数，因此两个实参必须是同一类型**。否则，编译器将不知道使用哪个类型来实例化该模板，并会生成错误。

### 用不满足其约束的实参调用 multiply

第 17 行用两个 `string` 实参调用 `multiply`。当编译器查找与此调用匹配的函数定义时，它只会遇到 `multiply` 函数模板。接下来，它将检查实参的类型，以确定它们是否满足第 8 行 **requires 子句**中列出的任一概念。**string 类型两者都不满足**。此外，没有其他 `multiply` 函数可以接收两个 `string` 实参，因此编译器会生成错误消息。图 15.5 显示了 g++ 的错误消息。我们用粗体突出显示了若干消息，并添加了垂直间距以便阅读。请注意此输出的最后几行，编译器在其中指出**“析取中没有任何操作数得到满足”**，并指向第 8 行的 **requires** 子句。对于此示例，Visual C++ 在我们三个首选编译器中产生了最简单的错误消息：

```text
1>c:\pauldeitel\Documents\examples\ch15\fig15_05.cpp(17,16): error
   C2672: 'multiply': no matching overloaded function found

1>c:\pauldeitel\Documents\examples\ch15\fig15_05.cpp(17,31): error
   C7602: 'multiply': the associated constraints are not satisfied

1>c:\pauldeitel\Documents\examples\ch15\fig15_05.cpp(9): message :
   see declaration of 'multiply'
```

## 15.4.3 C++20 预定义概念

C++ 标准的“库概念索引”<sup>39</sup> 按字母顺序列出了标准中定义的概念。下表按头文件——`<concepts>`——列出了所有标准概念。

39. C++ 标准，“库概念索引”。访问于 2023 年 4 月 18 日。https://timsong-cpp.github.io/cppwp/n4861/conceptindex.

