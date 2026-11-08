
## 函数的声明与定义

```cpp
int add1(int, int);                 // declaration
int add2(int a, int b) { return a + b; } // definition
```

函数 `add1` 被声明，而 `add2` 被定义。这意味着，如果你在求值上下文中使用 `add1`，例如通过调用它，就会得到链接时错误。关键观察是，你可以在未求值上下文中使用 `add1`，例如 `typeid`[^70] 或 `decltype`[^71]。这两个运算符都接受未求值操作数。

## 未求值上下文

```cpp
 1    // unevaluatedContext.cpp
 2
 3    #include <iostream>
 4    #include <typeinfo>  // typeid
 5
 6    int add1(int, int);                 // declaration
 7    int add2(int a, int b) { return a + b; } // definition
 8
 9    int main() {
10
11        std::cout << '\n';
12
13        std::cout << "typeid(add1).name(): " << typeid(add1).name() << '\n';
14
15        decltype(*add1) add = add2;
16
17        std::cout << "add(2000, 20): " << add(2000, 20) << '\n';
18
19        std::cout << '\n';
20    }
```

`typeid(add1).name()`（第 13 行）返回该类型的字符串表示，而 `decltype`（第 15 行）推导其参数的类型。

[^70]: https://en.cppreference.com/w/cpp/language/typeid
[^71]: https://en.cppreference.com/w/cpp/language/decltype

![](img/c60a87adb7f61e2e82071d081bbb389a_212_0.png)

## 4.7.3.2 无状态 Lambda

无状态 lambda 是不从环境中捕获任何内容的 lambda。或者换句话说，无状态 lambda 是 lambda 定义中初始方括号 `[]` 为空的 lambda。例如，lambda 表达式 `auto add = [](int a, int b){ return a + b; };` 是无状态的。

## 4.7.3.3 适配标准模板库的关联容器

在我向你展示示例之前，我必须补充几点说明。容器 `std::set` 以及标准模板库中的所有其他有序关联容器（`std::map`、`std::multiset` 和 `std::multimap`）都使用函数对象 `std::less` 对键进行排序。默认情况下，`std::less` 按字典序升序对所有键进行排序。`std::set`[^28] 的声明展示了 `std::less` 的隐式使用。

`std::set` 的声明

```cpp
template<
    class Key,
    class Compare = std::less<Key>,
    class Allocator = std::allocator<Key>
> class set;
```

[^28]: https://en.cppreference.com/w/cpp/container/set

### 在未求值上下文中使用的 Lambda

```cpp
 1    // lambdaUnevaluatedContext.cpp
 2
 3    #include <cmath>
 4    #include <iostream>
 5    #include <memory>
 6    #include <set>
 7    #include <string>
 8
 9    template <typename Cont>
10    void printContainer(const Cont& cont) {
11        for (const auto& c: cont) std::cout << c << " ";
12        std::cout << "\n";
13    }
14
15    int main() {
16
17        std::cout << '\n';
18
19        std::set<std::string> set1 = {"Scott", "Bjarne", "Herb", "Dave", "michael"};
20        printContainer(set1);
21
22        using SetDecreasing = std::set<std::string,
23                                      decltype([](const auto& l, const auto& r) {
24                                          return l > r;
25                                      })>;
26        SetDecreasing set2 = {"scott", "Bjarne", "Herb", "Dave", "michael"};
27        printContainer(set2);
28
29        using SetLength = std::set<std::string,
30                                  decltype([](const auto& l, const auto& r) {
31                                      return l.size() < r.size();
32                                  })>;
33        SetLength set3 = {"scott", "Bjarne", "Herb", "Dave", "michael"};
34        printContainer(set3);
35
36        std::cout << '\n';
37
38        std::set<int> set4 = {-10, 5, 3, 100, 0, -25};
39        printContainer(set4);
40
41        using SetAbsolute = std::set<int, decltype([](const auto& l, const auto& r) {
42            return std::abs(l) < std::abs(r);
43        })>;
44        SetAbsolute set5 = {-10, 5, 3, 100, 0, -25};
45        printContainer(set5);
46
47        std::cout << "\n\n";
48
49    }
```

下面是程序的输出。

```
Bjarne Dave Herb michael scott
scott michael Herb Dave Bjarne
Herb scott Bjarne michael

-25  -10  0  3  5  100
0  3  5  -10  -25  100
```

### 在未求值上下文中使用 lambda

当你研究程序的输出时，可能会感到惊讶。特殊的 `set3` 使用 lambda `[](const auto& l, const auto& r){ return l.size() < r.size(); }` 作为谓词，却忽略了名字 Dave。原因很简单。Dave 与先添加的 Herb 长度相同。`std::set` 支持唯一键，而在这种情况下，使用特殊谓词后这些键是相同的。如果我使用 `std::multiset`，就不会发生这种情况。

## 4.7.4 consteval Lambda

C++20 支持 `consteval`。`consteval` lambda 意味着该 lambda 是一个在编译时执行的立即函数。

一个 `consteval` lambda

```cpp
 1    // constevalLambda.cpp
 2
 3    #include <algorithm>
 4    #include <iostream>
 5    #include <vector>
 6
 7    int main() {
 8
 9        std::cout << '\n';
10
11        auto constevalLambda = [] () consteval {
12            std::vector myVec = {1, 2, 4, 3};
13            std::sort(myVec.begin(), myVec.end());
14            return myVec.back();
15        };
16
17        std::cout << "constevalLambda: " << constevalLambda() << '\n';
18
19        std::cout << '\n';
20
21    }
```

lambda `constevalLambda`（第 11 行）被声明为 `consteval`。因此，lambda 调用（第 17 行）在编译时执行。

![](img/c60a87adb7f61e2e82071d081bbb389a_215_0.png)

### 空参数子句

当你将 lambda 声明为 `consteval` 时，在 C++20 中仍然需要冗余的空参数子句 `[] () consteval`。到了 C++23，这一限制取消了，你可以定义不带参数子句的 `consteval` lambda：

```cpp
// A consteval lambda with empty parameter clause
auto constevalLambda = [] () consteval {
    std::vector myVec = {1, 2, 4, 3};
    std::sort(myVec.begin(), myVec.end());
    return myVec.back();
};
```

## 4.7.5 初始化捕获中的包展开

C++20 修复了 lambda 表达式的一个语法限制：初始化捕获中的包展开。C++ 中的 lambda 表达式支持捕获子句中的参数包。自 C++14 起，广义捕获允许它从外围作用域初始化捕获变量，并在 lambda 中使用它们。以下简短代码示例说明了这两个特性。

### 捕获子句中的参数包

```cpp
// parameterPacksLambda.cpp

void hello(int, double, bool) { }

template<typename... Args>
void func(Args... args) {
    auto newFunc = [args...] { return hello(args...); };
    newFunc();
}

int main() {

    func(5, 5.5, true);

}
```

### 广义捕获

```cpp
// generalizedCaptures.cpp

#include <memory>
#include <utility>

int main() {

    auto uniq = std::make_unique<int>(5);

    auto lamb = [newUniq = std::move(std::move(uniq))] {
        int val = *newUniq;
    };

    lamb();

}
```

在 C++20 之前，无法将这两个特性结合起来。自 C++20 起，这种不对称性消失了。

### 初始化捕获中的包展开

```cpp
// packExpansionInitCapture.cpp

#include <iostream>
#include <memory>
#include <utility>

template<typename Callable, typename ... Args>
auto packExpansion(Callable call, Args ... args) {
    return [call, ...args = std::move(args)] {
        return call(args...);
    };
}

void func(int fir, double sec, bool thi) {
    std::cout << std::boolalpha;
    std::cout << "fir: " << fir << '\n';
    std::cout << "sec: " << sec << '\n';
    std::cout << "thi: " << thi << '\n';
}

int main() {

    std::cout << '\n';

    auto lamb1 = packExpansion(func, 1, 2, true);
    lamb1();

    std::cout << '\n';

}
```

在第 10 行，我在初始化捕获中应用了包展开。由于语法限制，省略号位于 `args` 之前：`[call, ...args = std::move(args)]`。

