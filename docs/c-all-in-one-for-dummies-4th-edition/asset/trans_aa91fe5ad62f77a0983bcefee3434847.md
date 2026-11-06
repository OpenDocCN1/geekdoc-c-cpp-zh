
AddIt() 的工作方式与你预期的一致。你可以像调用任何其他函数一样调用它，并在 vector 内提供起点和终点。前两次调用 AddIt 对整个 vector 求和，第三次调用创建一个迭代器，改变其偏移量，然后对 vector 内的一个范围求和。以下是此示例的输出：

```text
30.431
30.431
12.82
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_793_0.png)

随机访问迭代器可以沿任一方向移动。此外，你可以使用提供给迭代器的容器内的各个成员。因此，你为迭代器创建的函数必须能够以任意顺序处理输入。如何处理这一要求取决于你创建的函数类型。

## 使用 Find 算法定位值

标准库包含许多函数，用于在容器中查找你所需的内容。尽可能高效地定位所需内容始终是一个好主意。四种常见的 `find()` 算法是

- `find()`
- `find_end()`
- `find_first_of()`
- `find_if()`

你使用的算法取决于你想查找什么以及你期望在哪里找到它。你可能会最常使用普通的 `find()` 算法。FindString 示例展示了如何定位 vector 中的特定字符串。你可以使用相同的方法在任何容器类型中定位内容：

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
    vector<string> Words;
    Words.push_back("Blue");
    Words.push_back("Green");
    Words.push_back("Teal");
    Words.push_back("Brick");
    Words.push_back("Purple");
    Words.push_back("Brown");
    Words.push_back("LightGray");

    vector<string>::iterator Result =
        find(Words.begin(), Words.end(), "LightGray");
    if (Result != Words.end())
        cout << *Result << endl;
    else
        cout << "Value not found!" << endl;

    Result = find(Words.begin(), Words.end(), "Black");
    if (Result != Words.end())
        cout << *Result << endl;
    else
        cout << "Value not found!" << endl;
}
```

该示例从一个包含颜色字符串的 vector 开始。在两种情况下，代码都尝试定位 vector 中的特定颜色。第一次代码成功，因为 LightGray 是 Words 中列出的颜色之一。然而，第二次尝试失败了，因为 Black 不是 Words 中的颜色。以下是此示例的输出：

```text
LightGray
Value not found!
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_794_0.png)

切勿假设代码一定会找到特定值。始终假设有人会提供一个不存在的值，然后确保你提供处理不存在值的方法。在此示例中，你只是看到一条消息，说明未找到该值。然而，在真实世界的代码中，你通常必须对未找到值的情况做出反应，方法是：

- 指示错误条件
- 将值添加到容器
- 替换为标准值
- 根据无效输入定义替代操作

使用前缀和后缀可以节省大量时间。清单 2-1 中的 PrefixesAndSuffixes 示例演示了如何使用它们创建各种变量。

## 清单 2-1：使用前缀和后缀创建字面量

```cpp
#include <iostream>
#include <typeinfo>
#include <cxxabi.h>

using namespace std;
using namespace abi;

char* Demangle(const char* Object) {
    int Status;
    char* RealName;
    RealName = __cxa_demangle(Object, 0, 0, &Status);
    return RealName;
}

int main() {
    auto Int1 = 23;
    auto Int2 = 23L;
    auto Int3 = 23U;
    auto Int4 = 23u;

    auto String1 = "Hello";
    auto String2 = L"Hello";
    auto String3 = U"Hello";
    auto String4 = u"Hello";

    cout << Int1 << endl;
    cout << Demangle(typeid(Int1).name()) << endl;
    cout << Int2 << endl;
    cout << Demangle(typeid(Int2).name()) << endl;
    cout << Int3 << endl;
    cout << Demangle(typeid(Int3).name()) << endl;
    cout << Int4 << endl;
    cout << Demangle(typeid(Int4).name()) << endl;

    cout << String1 << endl;
    cout << Demangle(typeid(String1).name()) << endl;
    cout << String2 << endl;
    cout << Demangle(typeid(String2).name()) << endl;
}
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_804_0.png)

请注意，熟形式确实输出了括号，但生形式没有。括号是生形式输入的必要组成部分。正如你可能想象的，熟形式将 `\r\n` 组合输出为控制字符，而生形式输出实际字符。

## 使用标准库中的 UDL

尽管你目前可以为本章前面“理解 UDL 的必要性”一节中描述的基本类型创建 UDL，但许多情况下开发者也需要为类创建 UDL。在某些情况下，这些类是标准库的一部分。为了避免这些 UDL 出现大量非标准实现，标准委员会决定将 UDL 直接添加到标准库中。你可以在 http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2013/n3531.pdf 阅读“标准库类型的用户自定义字面量”的详细信息。一致且标准化的 UDL 现在已附加到某些类上。以下各节描述了更重要的类并展示了如何使用它们。

### std::basic_string

`std::basic_string` 类使你能够处理类似 char 的对象序列。该类目前定义了以下模板：

- `char`
- `wchar_t`
- `char16_t`
- `char32_t`

### 获取标准库 UDL 支持

将 UDL 添加到标准库是 C++14 的新功能。要真正看到此功能的效果，你的编译器必须支持所有 C++14 新增内容。由于其中一些功能需要时间来实现，你的 C++ 编译器可能不会提供所有标准化功能，即使它声称支持 C++14。

此示例执行三个基本的转换级别，以便你可以看到从一个级别到另一个级别的进展。在第一种情况下，你看到创建简单 basic_string 对象 std::string 的直接方法。如你所见，它的工作方式与任何其他模板一样。第二种情况依赖于 C++11 类型运算符定义来模拟包含在 C++14 中的 UDL。本章的“创建你自己的 UDL”一节将告诉你有关创建此类运算符的所有详细信息。你现在真正需要知道的是，该运算符使得在创建 basic_string 对象时可以使用快捷方式。第三种情况显示了相同 _s 定义的 C++14 版本，但这个版本直接内置于标准库中，因此你不必做任何特殊事情即可使用它。在所有三种情况下，你都会创建相同的 basic_string 对象类型，但每次的技术都不同。运行此示例时，你会看到以下输出：

```text
A standard string.
std::__cxx11::basic_string<char, std::char_traits<char>,
    std::allocator<char> >
This is an auto string.
std::__cxx11::basic_string<char, std::char_traits<char>,
    std::allocator<char> >
This is a UDL string.
std::__cxx11::basic_string<char, std::char_traits<char>,
    std::allocator<char> >
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_806_0.png)

关于 basic_string 的生形式和熟形式应该如何工作，网上似乎存在一些困惑。查看 _s 和 s 运算符时，代码已经提供了生形式和熟形式两种实现。例如，如果你将以下代码与 _s 运算符一起使用：

```cpp
auto RawString = R"(This is a\\r\\nraw string.)";
auto CookedString = "This is a \\r\\ncooked string.";
cout << RawString << endl;
cout << CookedString << endl;
```

你会看到以下输出：

```text
This is a \r\nraw string.
This is a
cooked string.
```

s 运算符以相同的方式工作。因此，你可以对同一个运算符使用生字符串或熟字符串，并获得相应的结果。

