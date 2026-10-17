
```cpp
public :
    SimpleOverloaded(TCall tf, UCall uf) : TCall(tf), UCall(uf) {
        using TCall::operator();
        using UCall::operator();
    }

template <typename TCall, typename UCall> MadeOverloaded(TCall& tf, UCall& uf) {
    return SimpleOverloaded<TCall, UCall>(tf, uf);
}

int main() {
    const auto func = std::cout << "Int! \n ", {
        [](int) { },
        [](float) { std::cout << "Float! \n " }
    };
    func(10);
    func(10.0f);
}
```

这次我们的代码稍多一点：我们继承了两个模板参数，但同时也需要显式地暴露它们的调用运算符。

为什么呢？这是因为编译器在寻找正确的函数重载时，要求候选必须处于同一个作用域内。

为了理解这一点，让我们写一个派生自两个基类的简单类型。示例注释包含了两个 `using` 语句：

```cpp
#include <iostream>

struct BaseInt {
    void Func(int) { std::cout << "BaseInt... \n " ; }
};

struct BaseDouble {
    void Func(double) { std::cout << "BaseDouble... \n " ; }
};

struct Derived : public BaseInt, BaseDouble {
    //using BaseInt::Func;
    //using BaseDouble::Func;
}
```

```cpp
int main() {
    Derived d;
    d.Func(10.0);
}
```

我们有两个实现了 `Func` 的基类。我们希望从派生对象调用该方法。

## GCC 报告了以下错误：

error: request for member 'Func' is ambiguous

查看 @Wandbox 上的演示

由于我们注释掉了 `using` 语句，`::Func()` 可能来自 `BaseInt` 或 `BaseDouble` 的作用域。编译器有两个作用域来搜索最佳候选者，根据标准，这是不允许的。

好了，让我们回到主要的用例：

`SimpleOver` 是一个基础类，尚未达到生产就绪。请查看 C++17 章节，我们在那里将讨论这种模式的进阶版本。得益于多个 C++17 特性，我们将能够继承多个 lambda（得益于变变模板）并利用更紧凑的语法！

## 在容器中存储 Lambda

作为本章的最后一个技术，让我们来看看在容器中存储闭包（closures）的问题。

但我不是写过 lambda 无法默认创建和赋值吗？

是的……不过我们这里可以采取一些技巧。

技巧之一是利用无状态 lambda（stateless lambdas）的属性，它可以转换为函数指针。虽然你不能直接存储闭包对象，但你可以保存从 lambda 表达式转换而来的函数指针。

例如：

将 Lambda 存储为函数指针。Wandbox 实时代码

```cpp
#include <iostream>
#include <vector>

int main () {
  using TFunc = void (*)(int &);
  std::vector<TFunc> ptrFuncVec;
  ptrFuncVec.push_back([](int &x) { std::cout << x << '\n'; });
  ptrFuncVec.push_back([](int &x) { x *= 2; });
  ptrFuncVec.push_back(ptrFuncVec[0]);
  int x = 10;
  for (const auto &entry : ptrFuncVec)
      entry(x);
}
```

在上面的示例中，我们创建了一个函数向量，这些函数将应用于变量。容器中有三个条目：

- 第一个打印输入参数的值。
- 第二个修改该值。
- 第三个是第一个的拷贝，所以它也会打印该值。

解决方案是有效的，但它仅限于无状态 lambda。如果我们想消除这个限制呢？

为了解决这个问题，我们可以求助于强大的辅助工具：`std::function`。为了让示例更有趣，我们从简单的整数切换到了使用 `std::string` 对象的 lambda：

将 Lambda 存储为 `std::function`。Wandbox 实时代码

```cpp
#include <algorithm>
#include <functional>
#include <iostream>
#include <string>
#include <vector>

int main() {
    std::vector<std::function<void(std::string&)>> funcVec;
    funcVec.push_back([](std::string& s) { std::cout << s << '\n'; });
    funcVec.push_back([](std::string& s) { s += " modified"; });
    std::string str = "hello";
    funcVec[0](str);
    funcVec[1](str);
    funcVec[0](str);
}
```

*(注：后续 OCR 文本存在大量重复和碎片，已根据题目提供的逻辑流进行处理。)*

函数签名和 C++ 包含了一些额外的头文件 `<functional>`。

如果你还记得 C++11 章节的内容，`std::function` 是一个沉重的对象（在 GCC 9 中 `sizeof` 显示为 32 字节），它需要一些高级的内部机制来处理任何可调用对象。

得益于 C++14 的改进，我们现在可以大幅简化代码：

```
Auto return type deduction for lambdas. Live code @Wandbox
#include <iostream>
auto CreateMullLambda(int x) noexcept {
    return [x](int param) noexcept { return x * param; };
}
int main() {
    const auto lam = CreateMullLambda(10);
    std::cout << sizeof(lam);
    return (2);
}
```

这次我们可以完全依赖编译时类型推导，不需要任何辅助类型。在 GCC 上，lambda 的 `sizeof(lam)` 仅为 4 字节，比使用 `std::function` 的解决方案便宜得多。请注意，我们也可以将 `CreateMullLambda` 标记为 `noexcept`，因为它没有可能抛出任何异常。这在返回 `std::function` 时是不可能的的。

## 带初始化器的捕获

现在是更多重大的更新！

正如你所记得，在 lambda 表达式中，你可以捕获外部作用域的变量。编译器会展开该捕获语法并在闭包类型中创建成员变量（非静态成员）。

现在，在 C++14 中，你可以在捕获句中创建新的成员变量并初始化它们。然后你可以在 lambda 内部访问这些变量。这被称为带初始化器的捕获，或者该功能的另一个名称是泛化 lambda 捕获（generalized lambda capture）。

## 例如：

带初始化器的捕获. Live code @Wandbox

```
#include <iostream>
int main () {
    int x = 30;
    int y = 12;
    const auto foo = [z = x + y]() { std::cout << z << '\n'; };
    x = 0;
    y = 0;
    foo();
}
```

## 输出：

42

在上面的示例中，编译器生成了一个新的成员变量并用 `x+y` 初始化它。如果你在该变量前面加上 `auto`，新变量的类型将以相同的方式推导。在我们的案例中：

```
auto z = x + y;
```

总结来说，上一个示例中的 lambda 解析为如下（简化）函数对象：

```
struct __unnamedLambda {
    void operator()() const {
        std::cout << z << '\n';
    }
    int z;
} someInstance;
```

当 lambda 表达式定义时，`z` 将被直接初始化（为 `x+y`）。

记住这句话。新变量是在定义 lambda 的地方初始化的，而不是调用它的地方。

这就是为什么如果你在创建 lambda 之后修改 x 或 y 变量，变量 z 将不会改变。在示例中，你可以看到在 lambda 定义之后我更改了 `x` 和 `y` 的值。输出仍然是 42，因为 `z` 在此之前初始化了。

通过初始化器创建变量也是灵活的，例如，你可以创建外部作用域变量的引用。

引用作为带初始化器的捕获. Live code @Wandbox

```cpp
#include <iostream>
int main() {
    int x = 30;
    const auto foo = [&z = x]() { std::cout << z << '\n'; };
    foo();
    x = 0;
    foo();
}
```

这次 `z` 变量是 `x` 的引用。它的创建方式就像你写的那样：

`auto & z = x;`

如果你运行该示例，你应该看到第一行打印 30，但第二行显示 0。这是因为我们捕获了一个引用，所以当你修改被引用的变量时，`z` 对象会改变。

## 局限性

请注意，你可以作为引用带初始化器捕获，但无法编写右值引用 `&&`。这就是为什么下面的代码是无效的：

```
[&& z = x] // 无效语法！
```

该功能的另一个限制是它不允许参数包（parameter packs）。让我们看看 [expr.prim.lambda] 的第 24 节：

> 简单捕获后跟省略号是包展开（见 [temp.variadic)）。一个初始化捕获后跟省略号是格式错误的（ill-formed）。

换句话说，在 C++14 中，你无法写：

```cpp
template <class... Args>
auto captureTest(Args... args) {
    return lambda = [...capturedArgs] = std::move(args)(){};
}
```

然而，这种语法在 C++20 中是可能的，参见本节。

## 对现有问题的改进

总而言之，新的 C++14 特性可以解决一些问题，例如对于仅可移动的类型或者允许额外的优化。

现在让我们回顾一下。

## 移动

以前，在 C++11 中，你不能按值捕获 `unique_ptr`。只能通过引用捕获。现在，从 C++14 开始，我们可以将对象移动到闭包类型的成员中：

捕获移动类型代码 @Wandbox

```cpp
#include <iostream>
#include <memory>
int main() {
    std::unique_ptr<int> p(new int{10});
    const auto bar = [ptr=move(p)] {
        std::cout << "pointer in lambda: " << ptr.get() << '\n';
    };
    std::cout << "pointer in main: " << p.get() << '\n';
}
```

输出：

```
pointer in lambda: 10
pointer in main: 0
```

得益于初始化捕获，你可以将所有权移动到 lambda。在闭包创建后，指针被设置为 `nullptr`。

## `std::function` 的陷阱

捕获移动的变量会导致闭包是可拷贝的。如果你想将这种 lambda 存储在 `std::function` 中就会出现问题，因为 `std::function` 只接受可拷贝的可调用对象。

简而言之，这无法编译：

```cpp
std::function<void()> fn = [ptr=move(p)] {};
```

## 优化

另一个主意是避免每次调用 lambda 时都计算某些值，我们可以计算一次。如果你想，也可以查看提案 P288，它处理了仅可移动类型。

为 lambda 创建字符串。Wandbox

```cpp
#include <algorithm>
#include <iostream>
#include <string>
#include <vector>
int main() {
  using namespace std::string_literals;
  std::vector<std::string> vs = {"apple", "orange", "foobar", "lemon"};
  const auto prefix = "foo" s;
  auto result = std::find_if(vs.begin(), vs.end(),
      [&prefix](const std::string& s) {
        return s == prefix + "bar" s;
      });
  if (result != vs.end()) {
    std::cout << prefix << "-found! \n";
  }
  result = std::find_if(vs.begin(), vs.end(),
    [savingString=prefix + "bar" s](const std::string& s) {
      return s == savingString;
    });
  if (result != vs.end()) {
    std::cout << prefix << "-found! \n";
  }
}
```

## 捕获成员变量

初始化器也用于捕获成员变量。我们可以捕获成员变量的副本而无需担心悬空引用。

例如：

```cpp
struct Baz {
  auto foo()const {
    return [s = s](){ std::cout << s << std::endl; }
  }
}
std::string s;
int main () {
  const auto f1 = Baz{"abc"}.foo();
  const auto f2 = Baz{"xyz"}.foo();
  f1();
  f2();
}
```

在 `foo()` 中，我们通过将其拷贝到闭包类型来捕获成员变量。此外，我们成员函数的返回类型使用了 `auto`。作为备注，在 C++11 中，我们必须使用 `std::function`。

当我们使用像 `[s = s]` 这样奇怪的语法时可能会令人惊讶，当声明 lambda。这段代码能够运行，是因为捕获的变量在闭包类型的范围内，而不是在外部范围内。这就是为什么这里没有冲突。

## 泛型 Lambda

这是一个大特性！

早期的 Lambda 规范允许我们创建匿名函数对象并传递给标准库中的各种泛型算法。然而，闭包本身并不是“泛型”的。例如，你不能将模板参数指定为 Lambda 参数。

幸运的是，从 C++14 开始，标准引入了泛型 Lambda（Generic Lambdas），现在我们可以这样写：

```cpp
const auto foo = [](auto x, int y) { std::cout << x << " " << y << '\n'; };
foo(10, 1);
foo(10.1234, 2);
foo("hello world", 3);
```

请注意 lambda 参数中的 `auto foo`。这等同于在闭包类型的调用运算符中使用模板声明：

```cpp
struct {
    template < typename T>
    void operator()(T x, int y) const {
        std::cout << x << " " << y << '\n';
    }
} someInstance;
```

如果有更多的 `auto` 参数，则代码会展开为独立的模板参数：

```cpp
const auto fooDouble = [](auto x, auto y) { /*...*/ };
```

展开为：

```cpp
struct {
    template < typename T, typename U>
    void operator()(T x, U y) const { /*...*/ }
} someOtherInstance;
```

## 变长泛型参数

```cpp
#include <iostream>
```
