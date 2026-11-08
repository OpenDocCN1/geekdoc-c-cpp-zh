

例如，以下程序统计排序过程中所需的交换次数。

```cpp
// https://godbolt.org/z/j7qoMdG3n
#include <vector>
#include <string>
#include <algorithm> // sort
#include <iostream>  // cout
using std::string; using std::vector; using std::cout;
// as before
int main() {
    vector dwarfs{          // as before
        /* sort */
        bool backwards = true;    // or false. Variable outside the lambda
        unsigned rightway = 0;   // counts <
        unsigned wrongway = 0;   // counts >
        std::ranges::sort(dwarfs,
            [backwards,&rightway,&wrongway](const Dwarf& a, const Dwarf& b) {
                bool result = backwards
                    ? a.name_ > b.name_
                    : a.name_ < b.name_;
                if(result==false) ++wrongway; else ++rightway;
                return result;
            }
        );
        /* output */
        cout << "Wrongway: " << wrongway << " Rightway: " << rightway << "\n";
        for(const auto& z : dwarfs) // backwards: "Thorin" to "Balin"
            cout << z.name_ << " ";
        cout << "\n";
    }
}
```

**清单 23.21** 捕获子句也可以包含引用。

这表明对七个矮人排序需要 17 次比较。其中，六次比较处于“错误顺序”，十一次处于“正确顺序”。

```text
Wrongway: 6 Rightway: 11
Thorin Oin Kili Gloin Fili Dwalin Balin
```

只有在绝对必要时，才应该在捕获子句中使用引用。一如既往，引用会带来一定的风险。对于匿名函数，通常会将它们传递出去——也就是说，将它们作为参数传给其他函数、作为结果返回等等。这时可能发生 lambda 比被引用的变量“活得更久”的情况。然而，如果你访问的是副本，就没有这种危险。

## 可变 Lambda

在第 13 章 13.10.10 节中，我承诺过会解释 lambda 中的 `mutable`，现在就在这里说明。

使用 `mutable`，你可以修改那些被拷贝到 lambda 中的捕获变量。为此，需要将 `mutable` 放在 lambda 之后。

```cpp
//https://godbolt.org/z/zMWo69974
#include <iostream>
int main() {
    int count = 0;
    auto plus1 = [count](int x) mutable {  // count as a copy
        std::cout << ++count; return x+1;
    };
    for(int i=0; i<5; ++i) {
        plus1(i);
    }
    std::cout << "\n";
    // Output: 12345
}
```

**清单 23.22 “mutable” 使 lambda 中的值捕获变得可变。**

即使是 `mutable` 也应谨慎使用。也许你希望对 `count` 使用引用捕获。如果是这样，你也可以在不使用 `mutable` 的情况下进行修改。

```cpp
// https://godbolt.org/z/8GxPMEcSo
#include <iostream>
int main() {
    int count = 0;
    auto plus1 = [&count](int x) { // count as reference
        ++count; return x+1;
    };
    for(int i=0; i<5; ++i) { plus1(i); }
    std::cout << "plus1 was called " << count << " times\n";
    // Output: plus1 was called 5 times
}
```

**清单 23.23 如果可能，最好不用 mutable。**

然而，如果 lambda 作为返回值或参数传递，引用就可能是危险的，因为被引用的变量可能已不存在。在特殊情况下，`mutable` 可以在这里有所帮助。

## 为了方便起见

现在唯一要告诉你的是，如果你的捕获子句内容很满，你还可以使用简写形式：

-   使用 `[a=b]`，可以用外部表达式 `b` 初始化 lambda 变量 `a`。
-   `[&r=s]` 用外部表达式 `s` 初始化 lambda 的引用 `r`。
-   使用 `[=]`，你可以按值（拷贝）访问所有可见变量。尤其要避免在成员函数中使用，因为目前 `*this` 也会被拷贝（即整个对象）。从 C++20 起，拷贝 `*this` 已被弃用。
-   `[&]` 允许你按引用访问所有变量。
-   `[this]` 和 `[*this]` 分别允许成员函数中的 lambda 以引用或拷贝的方式访问整个实例（后者从 C++17 起）。由于 `[*this]` 很快将不再拷贝 `*this`，显式写出 `[*this]` 将是必要的。
-   `[...]` 在具有可变参数的模板中展开——并且可以与 `[&...]` 结合使用（从 C++20 起）。
-   所有这些元素都可以组合使用，用逗号分隔。
-   你可以指定 `[&,backwards]`，表示除 `backwards` 外所有变量都按引用访问，而 `backwards` 以拷贝形式提供。
-   相反，`[=,&wrong,&right]` 将所有变量以拷贝形式提供，只有 `wrong` 和 `right` 作为引用。

如果捕获变量的名字在函数体内使用起来不合适，你也可以在捕获变量列表中声明一个新变量，并通过*捕获变量初始化子句*来定义它：

```cpp
bool backwards = true;    // or false; variable outside the lambda
unsigned correct = 0;      // counts with &
unsigned incorrect = 0;    // counts with
std::sort(begin(dwarfs), end(dwarfs),
    [dir=backwards,&cf=incorrect,&cr=correct](const Dwarf& a, const Dwarf& b) {
        bool result = dir ? a.name_ > b.name_ : a.name_ < b.name_;
        if(result==false) ++cf; else ++cr;
        return result;
    }
);
```

你可能很少需要这种用法。

更多的时候，你可能会用到让编译器自动确定匿名函数参数类型的能力。这时，只需使用 `auto` 来代替具体类型——在我们的例子中是 `Dwarf`。编译器通常能为上下文确定必要的类型：

```cpp
std::ranges::sort(dwarves,
  [](const auto &a, const auto &b) { return a.year_ > b.year_; }
);
```

除此之外，`auto` 与 `const` 和 `&` 结合使用的常规类型推断规则同样适用。如果你希望按值（拷贝）接收参数，直接写 `auto`。如果你希望参数是常量引用，请使用 `const auto&`。

### 23.3.7 不用“template”，而用“auto”的模板函数

现在你一定能把两点结合起来：lambda 是一种函数，`auto` 确定参数类型，而且我可以将 lambda 赋值给变量，其中 `auto` 也处理了烦人的返回类型。那么为什么我不能把这一切结合起来，得到一个紧凑、可读（因为没有尖括号）的函数模板定义呢？

```cpp
// https://godbolt.org/z/xnbvExSKc
#include <iostream>
#include <string>
using std::cout; using std::string; using namespace std::literals;
auto min2 = [](const auto &a, const auto &b) {
  return a<b ? a : b;
};
auto min3 = [](const auto &a, const auto &b, const auto &c) {
  return min2(a, min2(b,c));
};
int main() {
  cout << min3( 3, 7, 2 ) << '\n';             // Output: 2
  cout << min3( 8.11, 113.2, -3.1 ) << '\n';   // Output: -3.1
  cout << min3( "Zoo"s, "Ape"s, "Mule"s ) << '\n'; // Output: Ape
}
```

你在 23.1.3 节的“C++20：缩写函数模板”框中看到，自 C++20 起，`auto` 的这种用法也适用于函数。同样在 C++20 中引入的，还有编写真正的模板 lambda 的能力：

```cpp
// https://godbolt.org/z/ncnW8aM8f
auto min2 = []<typename T>(const T &a, const T &b) {
  return a<b ? a : b;
};
auto min3 = []<typename T>(const T &a, const T &b, const T &c) {
  return min2(a, min2(b,c));
};
```

使用这一特性，你可以强制要求参数必须具有相同类型。

## 23.4 C++ 概念（Concepts）

自 C++20 起，可以限制用作模板参数的类型。为此，引入了概念（concepts）。这些概念在 C++ 中定义了一种语言，允许你对模板参数进行断言。当你实例化（即使用）模板时，这些断言会被检查，并给出比没有概念时更清晰的错误消息。

标准库带有大量概念，其中许多在 `<concepts>` 头文件中，也在 `<iterators>`、`<ranges>` 等头文件中。

### 23.4.1 如何阅读概念

当你查看带有概念的函数头时，会看到类似下面清单的内容。

```cpp
// https://godbolt.org/z/jP75nY4EW
#include <concepts>  // integral
#include <iostream>
using namespace std;
// Concept explicitly with requires
template<typename T> requires integral<T>
auto add_1(T val) { return val+1; }
// abbreviated concept
template<integral T>
auto add_2(T val) { return val+2; }
// abbreviated function template with concept
auto add_3(integral auto val) { return val+3; }
// Ad-hoc requirements for function template
auto add_4(auto val) requires integral<decltype(val)>
{ return val+4; }
int main() {
    cout << add_1(1) << '\n';              // Output: 2
    cout << add_2(1) << '\n';              // Output: 3
    cout << add_3(1) << '\n';              // Output: 4
    cout << add_4(1) << '\n';              // Output: 5
    cout << add_3("text") << '\n';          // Error
    integral auto val = add_1(99);           // also for auto variables
    cout << val << '\n';                     // Output: 100
}
```

**清单 23.24** 概念可以有多种写法。

函数 add_1、add_2、add_3 和 add_4 实质上是相同的，只是使用了不同的记法：

