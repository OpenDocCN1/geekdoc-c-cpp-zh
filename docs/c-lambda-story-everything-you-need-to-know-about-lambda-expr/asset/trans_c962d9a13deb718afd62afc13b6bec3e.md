
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
#include <iostream>
#include <vector>

int main () {
  using TFunc = void (*)(int &);
  std::vector<TFunc> ptrFuncVec;

  ptrFuncVec.push_back([](int &x) { std::cout << x << '\n'; });
  ptrFuncVec.push_back([](int &x) { x *= 2; });
  ptrFuncVec.push_back(ptrFuncVec[0]); // 再次打印；

```cpp
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

将 Lambda 存储为 std::function。Wandbox 实时代码

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
