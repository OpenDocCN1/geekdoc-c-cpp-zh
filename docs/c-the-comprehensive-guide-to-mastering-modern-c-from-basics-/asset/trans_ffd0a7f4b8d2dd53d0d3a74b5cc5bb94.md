
（继续）。

+   所有这些元素都可以组合，并用逗号分隔。

+   你可以通过 `[&backwards]` 指定你希望通过引用访问所有变量，但 `backwards` 除外，它将以拷贝的形式供给你使用。

+   相反，`[=&wrong,right]` 为你提供了所有变量的拷贝，唯有 `wrong` 和 `right` 是引用。

如果访问变量的名称看起来不适合在函数内部使用，你也可以在访问变量列表中声明新变量，该变量通过访问变量初始化子进行定义：

```cpp
bool backwards = true; // 或 false; lambda 外部的变量
unsigned correct = 0; // 计数 <
unsigned incorrect = 0; // 计数 >
std::sort(begin(dwarves), end(dwarves),const Dwarf&a, const Dwarf&b)[dir=backwards,cf=incorrect,cr=correct]{
    bool result = dir ? a.name_ > b.name_ : a.name_ < b.name_;
    if(result==false) ++cf; else ++cr;
    return result;
}
```

你可能很少会用到这种用法。

更多情况下，你可能会发现自己利用编译器自动确定匿名函数参数类型的能力。这时，与其使用特定类型——在我们的用例中是 Dwarf——不如直接使用 `auto`。编译器通常可以从上下文中推导出所需的类型。

```cpp
std::ranges::sort(dwarves,
    [](const auto& a, const auto& b) { return a.year_ > b.year_; }
);
```

否则，适用于 `auto` 结合 `const &` 的类型推推规则。如果你想以值（拷贝）接收参数，只需写 `auto`。如果你想将其作为常量引用，请使用 `const auto&`。

## 23.3.7 不使用 "template" 但使用 "auto" 的模板函数

现在你一定能推断出：lambda 是一种函数，`auto` 决定参数类型，我可以将 lambda 赋值给变量，而 `auto` 也处理了烦人的返回类型。
那么难道我不能把所有这一切结合起来，得到一个紧凑、易读（因为没有角括号）的函数模板定义吗？

```cpp
// https://godbolt.org/znxvbEx5Kc
#include <iostream>
#include <string>

using std::cout; using std::string; using namespace std::literals;
auto min2 = [](const auto& a, const auto& b) {
    return a<b ? a : b;
};

auto min3 = [](const auto& a, const auto& b, const auto& c) {
    return min2(a, min2(b,c));
};

int main() {
    cout << min3(3, 7, 2) << '\n'; // 输出: 2
    cout << min3(8.11, 113.2, -3.1) << '\n'; // 输出: -3.1
    cout << min3("Zoo", "Ape", "Mule"s) << '\n'; // 输出: Ape
}
```

你在第 23.1.3 节的“C++20：简写函数模板”框中看到，这种 `auto` 的用法自 C++20 起也适用于函数。此外，C++20 还引入了编写真正的模板 lambda 的能力：

```cpp
// https://godbolt.org/z/nenW8aM81
auto min2 = [<typename T>(const T &a, const T &b) {
    return a < b ? a : b;
};
auto min3 = [<typename T>(const T &a, const T &b, const T &c) {
    return min2(a, min2(b,c));
};
```

通过此功能，你可以强制参数必须具有相同的类型。

## 23.4 C++ 概念 (Concepts)

自 C++20 起，有了限制你作为模板参数使用的类型的可能。为此引入了概念（concepts）。它们定义了 C++ 内部的语言结构，允许你对模板参数进行断言（即使用模板时，这些断言会被检查，并以比不使用概念时更清晰的错误信息进行确认）。

标准库带了许多概念，其中许多在 `<concepts>` 头文件中，但也也在 `<iterators>`、`<ranges>` 等头文件中。

### 23.4.1 如何阅读概念

当你看到一个带有概念的函数头时，你会看到类似下面的列表。

```cpp
// https://godbolt.org/z/jp75nY4EW
#include <concepts> // integral
#include <iostream>
using namespace std;
// 显式要求概念
template<typename T> requires integral<T>
auto add_1(T val) { return val+1; }
// 简写概念
template<integral T>
auto add_2(T val) { return val+2; }
// 带有概念的简写函数模板
auto add_3(integral auto val) { return val+3; }
// 函数模板的临时性要求
auto add_4(auto val) requires decltype(val)
{ return val+4; }
int main() {
	cout << add_1(1) << '\n'; // 输出: 2
	cout << add_2(1) << '\n'; // 输出: 3
}
```

cout << add_3(1) << '\n';
cout << add_4(1) << '\n';

cout << add_3("text") << '\n';
integral auto val = add_1(99);
cout << val << '\n';

// 输出: 4
// 输出: 5
// 错误
// 同样适用于 auto 变量
// 输出: 100

## 列表 23.24 概念有多种写法

函数 `add_1`、`add_2`、`add_3` 和 `add_4` 本质上是相同的，只是表示方法不同：

-   `add_1` 在模板头部使用了 `requires` 语法。在这里，类型 `T` 有一个名称可以在 `requires` 中引用。
-   `add_2` 在模板头部使用特别紧凑的简写，利用了之前定义的概念。
-   `add_3` 使用带有 `auto` 参数的简写函数模板代替了模板头部。你几乎意识不到正在定义模板。
-   `add_4` 补偿了 `add_3` 的缺点，即在没有模板头部的情况下无法命名类型。

