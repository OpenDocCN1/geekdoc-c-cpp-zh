
```text
fig15_18.cpp:23:4: error: no matching function for call to 'foldingSum'
  foldingSum(1, 2, "hello"); // error: three different types
  ^~~~~~~~~~
fig15_18.cpp:14:6: note: candidate template ignored: constraints not satisfied
[with FirstItem = int, RemainingItems = <double, std::basic_string<char>>]
auto foldingSum(FirstItem first, RemainingItems... theRest) {
     ^
fig15_18.cpp:13:13: note: because 'SameTypeElements<int, double,
std::basic_string<char> >' evaluated to false
  requires SameTypeElements<FirstItem, RemainingItems...>
           ^
fig15_18.cpp:9:34: note: because 'std::same_as<int, double>' evaluated to
false
concept SameTypeElements = (std::same_as<T, Us> && ...);
                                  ^
/usr/bin/../lib/gcc/x86_64-linux-gnu/10/../../../../include/c++/10/concepts:63:19: note: because '__detail::__same_as<int, double>' evaluated to
false
      __detail::__same_as<_Tp, _Up> && __detail::__same_as<_Up, _Tp>;
      ^
/usr/bin/../lib/gcc/x86_64-linux-gnu/10/../../../../include/c++/10/concepts:57:27: note: because 'std::is_same_v<int, double>' evaluated to false
    concept __same_as = std::is_same_v<_Tp, _Up>;
                          ^
fig15_18.cpp:9:34: note: and 'std::same_as<int, std::basic_string<char> >'
evaluated to false
concept SameTypeElements = (std::same_as<T, Us> && ...);
                                  ^
/usr/bin/../lib/gcc/x86_64-linux-gnu/10/../../../../include/c++/10/concepts:63:19: note: because '__detail::__same_as<int, std::basic_string<char>
>' evaluated to false
      __detail::__same_as<_Tp, _Up> && __detail::__same_as<_Up, _Tp>;
      ^
/usr/bin/../lib/gcc/x86_64-linux-gnu/10/../../../../include/c++/10/concepts:57:27: note: because 'std::is_same_v<int, std::basic_string<char> >'
evaluated to false
    concept __same_as = std::is_same_v<_Tp, _Up>;
                          ^

1 error generated.
```

**图 15.18** | 将可变参数函数模板的参数包约束为相同类型的元素。（第 2 部分，共 2 部分。）

## 可变参数模板的自定义概念

第 8–9 行定义了一个自定义概念 SameTypeElements，它带有两个类型参数：

- 第一个表示单个类型，以及
- 第二个是**可变参数**类型参数。

## 调用 `foldingSum`

约束

```cpp
std::same_as<T, Us>
```

将类型 T 与参数包 Us 中的一个类型进行比较。该约束位于折叠表达式中，因此**参数包展开**（`...`）会对参数包 Us 中的每个类型应用一次 `std::same_as<T, Us>`，将 Us 中的每个类型与类型 T 进行比较。如果参数包 Us 中的每一项都与 T 相同，则约束求值为 true。`foldingSum` 函数模板中的第 13 行将我们的 `SameTypeElements` 概念应用于该函数的类型参数。

在 `main` 中，第 21 行和第 22 行分别用三个 int 和三个 string 调用 `foldingSum`。每次调用都有三个相同类型的实参，因此这些语句将成功编译。然而，第 23 行尝试用一个 int、一个 double 和一个 string 调用 `foldingSum`。在该调用中，`SameTypeElements` 概念中的类型 T 是 int，而类型 double 和 string 被放入参数包 Us 中。当然，double 和 string 不是 int，因此每次使用概念 `std::same_as<T, Us>` 都会失败。图 15.18 显示了 Clang C++ 编译器的错误消息。我们用粗体突出显示了关键消息，并添加了垂直间距以提高可读性。Clang 指出

```text
error: no matching function for call to 'foldingSum'
```

以及

```text
note: candidate template ignored: constraints not satisfied
```

它还在注释中指出每个因类型与 int 不相同而失败的单独 `std::same_as` 测试：

```text
note: because 'std::same_as<int, double>' evaluated to false
note: and 'std::same_as<int, std::basic_string<char> >' evaluated to false
```

## 15.13 模板元编程

正如我们提到的，现代 C++ 的一个目标是在编译时完成更多工作，使编译器能够针对运行时性能优化你的代码。这些优化工作很大一部分是通过模板元编程（TMP）完成的，它使编译器能够

- 操作类型，
- 执行编译时计算，以及
- 生成优化后的代码。

到目前为止介绍的**概念**、**基于概念的重载**和**类型特征**是关键的模板元编程能力。

模板元编程很复杂。如果使用得当，它可以帮助你提高程序的运行时性能。因此，了解模板元编程的强大能力很重要。

本节的目标是展示易于处理的模板元编程示例。我们提供了许多脚注引用，其中包含进一步学习的资源。我们将展示以下示例：

- 使用元函数在编译时计算值，
- 使用 `constexpr` 函数在编译时计算值，
- 通过 `constexpr if` 语句在编译时使用类型特征以优化运行时性能，以及
- 使用元函数在编译时操作类型。

### 15.13.1 C++ 模板是图灵完备的

Todd Veldhuizen 证明了 C++ 模板是图灵完备的，92,93 因此任何可计算的内容都可以通过 C++ 模板元编程在编译时计算。展示这种编译时计算的早期尝试之一是在 1994 年 C++ 早期标准化工作期间提出的。Erwin Unruh 编写了一个模板元程序来计算小于 30 的素数。94,95 该程序没有编译通过，但编译器的错误消息中包含了素数计算结果。你可以在以下网址查看原始程序（它已不再是有效的 C++）和原始编译器错误消息：

http://www.erwin-unruh.de/primorig.html

以下是这些错误消息中的一些选定行。他的类模板 D 的特化显示了前几个素数，并以粗体突出显示：

```text
|	Type `enum{}' can't be converted to type `D<2>`: ("primes.cpp",L2/C25).
|	Type `enum{}' can't be converted to type `D<3>`: ("primes.cpp",L2/C25).
|	Type `enum{}' can't be converted to type `D<5>`: ("primes.cpp",L2/C25).
|	Type `enum{}' can't be converted to type `D<7>`: ("primes.cpp",L2/C25).
```

### 15.13.2 在编译时计算值

编译时计算的目标是优化程序的运行时性能。96 图 15.19 使用模板元编程在编译时计算阶乘。首先，我们使用由模板实现的递归阶乘定义。然后，我们展示两个编译时 `constexpr` 函数，它们分别使用第 5.16 节介绍的迭代算法和递归算法。C++ 核心准则建议使用 `constexpr` 函数在编译时计算值 97——此类函数使用传统 C++ 语法。

- 92. Todd Veldhuizen，“C++ 模板是图灵完备的”，2003 年。访问于 2023 年 4 月 18 日。https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.14.3670。
- 93. “模板元编程。”维基百科。维基媒体基金会。访问于 2023 年 4 月 18 日。https://en.wikipedia.org/wiki/Template_metaprogramming。
- 94. Erwin Unruh，“素数计算”，1994 年。ANSI X3J16-94/005/JISO WG21-94-62。
- 95. Rainer Grimm，“C++ 核心准则：模板元编程的规则”，2019 年 1 月 7 日。访问于 2023 年 4 月 18 日。https://www.modernescpp.com/index.php/c-core-guidelines-rules-for-template-metaprogramming。感谢 Rainer Grimm 的这篇博客文章，它引导我们注意到关于 Erwin Unruh 的历史注记。
- 96. “模板元编程。”维基百科。
- 97. C++ 核心准则，“T.123：使用 constexpr 函数在编译时计算值。”访问于 2023 年 4 月 18 日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rt-ct。

```cpp
// calling the recursive constexpr function recursiveFactorial
std::cout << "\n\nCALCULATING FACTORIALS AT COMPILE TIME "
          << "WITH A RECURSIVE CONSTEXPR FUNCTION"
          << "\nrecursiveFactorial(0): " << recursiveFactorial(0)
          << "\nrecursiveFactorial(1): " << recursiveFactorial(1)
          << "\nrecursiveFactorial(2): " << recursiveFactorial(2)
          << "\nrecursiveFactorial(3): " << recursiveFactorial(3)
          << "\nrecursiveFactorial(4): " << recursiveFactorial(4)
          << "\nrecursiveFactorial(5): " << recursiveFactorial(5);

// calling the iterative constexpr function iterativeFactorial
std::cout << "\n\nCALCULATING FACTORIALS AT COMPILE TIME "
          << "WITH AN ITERATIVE CONSTEXPR FUNCTION"
          << "\niterativeFactorial(0): " << iterativeFactorial(0)
          << "\niterativeFactorial(1): " << iterativeFactorial(1)
          << "\niterativeFactorial(2): " << iterativeFactorial(2)
          << "\niterativeFactorial(3): " << iterativeFactorial(3)
          << "\niterativeFactorial(4): " << iterativeFactorial(4)
          << "\niterativeFactorial(5): " << iterativeFactorial(5) << "\n";
}
```

```text
CALCULATING FACTORIALS AT COMPILE TIME WITH A RECURSIVE METAFUNCTION
Factorial(0): 1
Factorial(1): 1
Factorial(2): 2
Factorial(3): 6
Factorial(4): 24
Factorial(5): 120

CALCULATING FACTORIALS AT COMPILE TIME WITH A RECURSIVE CONSTEXPR FUNCTION
recursiveFactorial(0): 1
recursiveFactorial(1): 1
recursiveFactorial(2): 2
recursiveFactorial(3): 6
recursiveFactorial(4): 24
recursiveFactorial(5): 120

CALCULATING FACTORIALS AT COMPILE TIME WITH AN ITERATIVE CONSTEXPR FUNCTION
iterativeFactorial(0): 1
iterativeFactorial(1): 1
iterativeFactorial(2): 2
iterativeFactorial(3): 6
iterativeFactorial(4): 24
iterativeFactorial(5): 120
```

**图 15.19** | 在编译时计算阶乘。（第 2 部分，共 2 部分。）

## 元函数

你可以使用元函数执行编译时计算。与你目前定义的函数类似，元函数也有参数和返回值，但它们的语法显著不同。元函数实现为类模板——通常使用结构体。元函数的参数是用于特化类模板的项，其返回值是一个公有类成员。第 15.5 节介绍的类型特征是元函数。

