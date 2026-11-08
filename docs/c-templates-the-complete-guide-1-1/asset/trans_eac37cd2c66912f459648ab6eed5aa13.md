
一个有趣的例子是重载 maximum 模板，以便仅显式指定返回类型：

点击此处查看代码图片

boost/max1.cpp

```cpp
template<typename T1, typename T2>
auto max (T1 a, T2 b)
{
    return b < a ? a : b;
}

template<typename RT, typename T1, typename T2>
RT max (T1 a, T2 b)
{
    return b < a ? a : b;
}
```

现在，例如，我们可以如下调用 max()：

点击此处查看代码图片

```cpp
auto a = max(4, 12.5);                 // uses float
decltype(a) b = max<long double>(7.2, 4); // uses decltype
and template
```

然而，当调用：

点击此处查看代码图片

```cpp
auto b = max<double>(4, 7.2);        // ERROR:
both function templates match
```

两个模板都匹配，这导致重载解析过程实际上无法偏向其中一个，并产生歧义错误。因此，在重载函数模板时，应确保对于任何调用，只有一个模板匹配。

一个有用的例子是为指针和普通 C 字符串重载 maximum 模板：

点击此处查看代码图片

boost/max2.cpp

```cpp
#include <cstring>
#include <string>

// maximum of two values of any type:
template<typename T>
T max (T a, T b)
{
    return b < a ? a : b;
}

// maximum of two pointers:
template<typename T>
T* max (T* a, T* b)
{
    return *b < *a ? a : b;
}

// maximum of two C-strings:
char const* max (char const* a, char const* b)
{
    return std::strcmp(a,b) < 0 ? a : b;
}

int main ()
{
int a = 7;
int b = 42;

auto m1 = ::max(a,b);     // max() for two val...
std::string s1 = "hey";
std::string s2 = "you";

auto m2 = ::max(s1,s2);   // max() for two val...

int* p1 = &b;
int* p2 = &a;

auto m3 = ::max(p1,p2);   // max() for two poi...

char const* x = "hello";
char const* y = "world";

auto m4 = ::max(x,y);     // max() for two C-...
}
```

注意，在 max() 的所有重载中，我们按值传递实参。通常，在重载函数模板时，最好不要做超出必要的修改。在为了允许特殊功能而更改参数数量或参数顺序之前，你应三思。通常更好的做法是提供一个重载函数来执行该任务。例如，如果 max() 的第二个实参应按值传递，你可以使用三参数版本来模拟三个 C++ 字符串的最大值。

点击此处查看代码图片

basics/max3ref.cpp

```cpp
#include <string>

// maximum of two values of any type (call-by-reference)
template<typename T>
T const& max (T const& a, T const& b)
{
    return b < a ? a : b;
}

// maximum of two C-strings (call-by-value)
char const* max (char const* a, char const* b)
{
    return std::strcmp(b,a) < 0 ? a : b;
}

// maximum of three values of any type (call-by-reference)
template<typename T>
T const& max (T const& a, T const& b, T const& c)
{
    return max (max(a,b), c);   // error if max...
}

int main ()
{
    auto m1 = ::max(7, 42, 68); // OK

    char const* s1 = "frederic";
    char const* s2 = "anica";
    char const* s3 = "lucas";

    auto m2 = ::max(s1, s2, s3); // runtime ERROR
}
```

会变成运行时错误，因为对于 C 字符串，`max(a, b)` 会创建一个新的临时局部值，该值按引用返回，但这个临时值在 return 语句完成后立即失效，留下悬空引用。不幸的是，这个错误相当隐蔽，并且可能不会在所有情况下显现。

注意：相比之下，`main()` 中对 `max()` 的第一次调用不会遇到同样的问题。这些临时值是为实参（7、42 和 68）创建的，但这些临时值是在 `main()` 中创建的，它们会持续到该语句结束。

这只是一个示例，说明由于重载解析规则，代码的行为可能不同于预期。此外，确保在调用函数之前已声明该函数的所有重载版本。这是因为在发起相应函数调用时，所有重载函数都可见这一事实可能很重要。例如，在尚未看到针对 `int` 的特殊双参数版本 `max()` 的声明的情况下定义三参数版本的 `max()`，会导致三参数版本使用双参数模板。

`basics/max.cpp`

点击此处查看代码图片

```cpp
#include <iostream>

// maximum of two values of any type:
template<typename T>
T max (T a, T b)
{
    std::cout << "max(T,T) \n";
    return b < a ? a : b;
}

// maximum of three values of any type:
template<typename T>
T max (T a, T b, T c)
{
    return max(max(a,b), c);        // use the two-argument version
                                      // because the two-argument
                                      // is too late!
}

// maximum of two int values:
int max (int a,
         int b)
{
    std::cout << "max(int,int) \n";
    return b < a ? a : b;
}

int main()
{
    max(7, 42, 68); // error: case max(T,T) isn't instantiated
}
```

我们在第 317 页的 13.2 节讨论细节。

## 1.6. 但是，我们难道不应该……？

可能，甚至这些简单的函数模板示例也会引出合理的问题。有三个问题可能非常常见，因此我们应在此简要讨论它们。

### 1.6.1 按值传递还是按引用传递？

你可能会想，为什么通常声明函数按值传递实参，而不是使用引用。一般来说，对于除像 `std::string_view` 这样只有一种值类型的类型之外的类型，建议按引用传递，因为按值传递会创建不必要的副本。

然而，出于多种原因，按值传递通常往往更好。

-   移动语义通常使复制成本很低。
-   而且有时根本没有复制或移动。

此外，对于模板，可能还会涉及一个特定目的：

-   模板可能同时用于简单类型和复杂类型，因此为复杂类型选择的方法对简单类型可能适得其反。
-   作为调用者，你通常可以选择按引用传递实参，使用 `std::ref()` 和 `std::cref()`（见第 99 页的 7.3 节）。
-   尽管传递字符串字面量或原始数组始终可能成为问题，但按引用传递它们通常被认为会成为更大的问题。所有这些都将在第 7 章详细讨论。目前，在本书中，我们通常会按值传递实参，除非某些功能只有在使用引用时才可能实现。

### 1.6.2 为什么不用 `inline`？

一般来说，函数模板不必用 `inline` 声明。与普通的非 inline 函数不同，我们可以在头文件中定义非 inline 函数模板，并在多个翻译单元中包含该头文件。

此规则的唯一例外是针对特定类型的模板完全特化，因此生成的代码不再是泛型的（所有模板参数都已定义）。更多细节见第 140 页的 9.2 节。

从严格的语言定义角度来看，`inline` 仅表示函数的定义可以在程序中多次出现。然而，`inline` 也意味着向编译器提供一个提示，告诉它该函数应“内联展开”。这样做在某些情况下可以生成更高效的代码，但在许多其他情况下也可能使代码效率降低。如今，编译器通常更擅长在没有 `inline` 关键字所隐含提示的情况下做出这一决定。不过，编译器在决策时仍会考虑 `inline` 的存在。

### 1.6.3 为什么不用 `constexpr`？

自 C++11 起，你可以使用 `constexpr` 来提供在编译期使用代码计算某些值的能力。对许多模板来说，这是有意义的。

例如，为了能够在编译期使用 maximum 函数，你必须如下声明它：

点击此处查看代码图片

```cpp
template<typename T>
constexpr auto max (T a, T b)
{
    return b < a ? a : b;
}
```

这样，你可以在需要编译期常量的地方使用 maximum 函数模板，例如在声明原始数组的大小时：

点击此处查看代码图片

```cpp
int a[::max(sizeof(int),100)];
```

或 `std::array<>` 的大小：

点击此处查看代码图片

```cpp
std::array<char, std::max(sizeof(char),100)> arr;
```

注意，我们会使用 `std::max` 来避免关于在模板内部比较有符号值与无符号值的警告。第 123 页的 8.2 节将讨论使用 `constexpr` 的其他示例。然而，为了保持对基础内容的关注，在讨论其他模板特性时，我们通常会跳过 `constexpr`。

## 1.7 总结

-   函数模板为不同的模板实参定义了一族函数。
-   当你将实参传递给依赖于模板参数的函数参数时，函数模板推导会确定要为相应参数类型实例化的模板参数。
-   你可以显式限定前导模板参数。
-   你可以为模板参数定义默认实参。它们可以引用之前的模板参数，并且后面可以跟没有默认实参的参数。
-   你可以重载函数模板。
-   当用其他函数模板重载函数模板时，应确保对于任何调用，只有一个模板匹配。
-   当你重载函数模板时，将修改限制为显式指定模板参数。
-   确保编译器在你调用函数模板之前看到它们的所有重载版本。
-   注意，根据 [std::max] 的注释，`max()` 模板 inter-
