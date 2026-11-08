
## 4.7 Lambda 改进

![](img/c60a87adb7f61e2e82071d081bbb389a_204_0.png)

Cippi 从滑梯上滑下来

在 C++20 中，lambda 表达式支持模板参数，因而也支持概念。当 lambda 没有状态时，它们可以被默认构造并支持拷贝赋值。此外，一项语法限制被取消了：初始化捕获中的包展开。另外，lambda 表达式可以用于未求值上下文。在 C++20 中，它们会检测你何时隐式拷贝 `this` 指针。这意味着 lambda 中一个导致未定义行为的重要原因消失了。

让我们从 lambda 的模板参数开始。

### 4.7.1 Lambda 的模板参数

诚然，有类型 lambda（C++11）、泛型 lambda（C++14）和模板 lambda（C++20 中 lambda 的模板参数）之间的差异很细微。

#### 有类型 lambda、泛型 lambda 和模板 lambda

```cpp
// templateLambda.cpp

#include <iostream>
#include <string>
#include <vector>

auto sumInt = [](int fir, int sec) { return fir + sec; };
auto sumGen = [](auto fir, auto sec) { return fir + sec; };
auto sumDec = [](auto fir, decltype(fir) sec) { return fir + sec; };
auto sumTem = []<typename T>(T fir, T sec) { return fir + sec; };

int main() {

    std::cout << '\n';

    std::cout << "sumInt(2000, 11): " << sumInt(2000, 11) << '\n';
    std::cout << "sumGen(2000, 11): " << sumGen(2000, 11) << '\n';
    std::cout << "sumDec(2000, 11): " << sumDec(2000, 11) << '\n';
    std::cout << "sumTem(2000, 11): " << sumTem(2000, 11) << '\n';

    std::cout << '\n';

    std::string hello = "Hello";
    std::string world = "world";
    // std::cout << "sumInt(hello, world): " << sumInt(hello, world) << '\n';
    std::cout << "sumGen(hello, world): " << sumGen(hello, world) << '\n';
    std::cout << "sumDec(hello, world): " << sumDec(hello, world) << '\n';
    std::cout << "sumTem(hello, world): " << sumTem(hello, world) << '\n';

    std::cout << '\n';

    std::cout << "sumInt(true, 2010): " << sumInt(true, 2010) << '\n';
    std::cout << "sumGen(true, 2010): " << sumGen(true, 2010) << '\n';
    std::cout << "sumDec(true, 2010): " << sumDec(true, 2010) << '\n';
    // std::cout << "sumTem(true, 2010): " << sumTem(true, 2010) << '\n';

    std::cout << '\n';

}
```

在展示这个程序大概会令人惊讶的输出之前，我想先比较这四个 lambda。

- sumInt
  - C++11
    - 有类型 lambda
      - 仅接受可转换为 int 的类型
- sumGen
  - C++14
    - 泛型 lambda
      - 接受所有类型
- sumDec
  - C++14
    - 泛型 lambda
      - 第二个类型必须可转换为第一个类型
- sumTem
  - C++20
    - 模板 lambda
      - 第一个类型和第二个类型必须相同

这对具有不同类型的模板实参意味着什么？当然，每个 lambda 都接受 int（第 16～19 行），而有类型 lambda sumInt 不接受字符串（第 25 行）。

用 bool 值 true 和 int 值 2010 调用这些 lambda 可能会令人惊讶（第 33～36 行）。

- sumInt 返回 2011，因为 true 是整型，会被提升为 int。
- sumGen 返回 2011，因为 true 是整型，会被提升为 int。sumInt 和 sumGen 之间存在细微差别，我将在几行后说明。
- sumDec 返回 2。为什么？第二个参数 sec 的类型变成第一个参数 fir 的类型：借助 decltype(fir) sec，编译器推导出 fir 的类型，并把它作为 sec 的类型。因此，2010 被转换为 true。在表达式 fir + sec 中，fir 是整型，会被提升为 1。最终结果是 2。
- sumTem 无效。

```text
sumInt(2000, 11): 2011
sumGen(2000, 11): 2011
sumDec(2000, 11): 2011
sumTem(2000, 11): 2011

sumGen(hello, world): Hello world
sumDec(hello, world): Hello world
sumTem(hello, world): Hello world

sumInt(true, 2010): 2011
sumGen(true, 2010): 2011
sumDec(true, 2010): 2
```

#### 有类型 lambda、泛型 lambda 和模板 lambda 之间的细微差别

模板 lambda 更典型的用例是在 lambda 中使用容器。下面的程序展示了三个接受容器的 lambda。每个 lambda 返回容器的大小。

#### 三个接受容器的 lambda

```cpp
// templateLambdaVector.cpp

#include <concepts>
#include <deque>
#include <iostream>
#include <string>
#include <vector>

auto lambdaGeneric = [](const auto& container) { return container.size(); };
auto lambdaVector = []<typename T>(const std::vector<T>& vec) { return vec.size(); };
auto lambdaVectorIntegral = []<std::integral T>(const std::vector<T>& vec) {
    return vec.size();
};

int main() {

    std::cout << '\n';

    std::deque deq{1, 2, 3};
    std::vector vecDouble{1.1, 2.2, 3.3, 4.4};
    std::vector vecInt{1, 2, 3, 4, 5};

    std::cout << "lambdaGeneric(deq): " << lambdaGeneric(deq) << '\n';
    // std::cout << "lambdaVector(deq): " << lambdaVector(deq) << '\n';
    // std::cout << "lambdaVectorIntegral(deq): "
    //             << lambdaVectorIntegral(deq) << '\n';

    std::cout << '\n';

    std::cout << "lambdaGeneric(vecDouble): " << lambdaGeneric(vecDouble) << '\n';
    std::cout << "lambdaVector(vecDouble): " << lambdaVector(vecDouble) << '\n';
    // std::cout << "lambdaVectorIntegral(vecDouble): "
    //             << lambdaVectorIntegral(vecDouble) << '\n';

    std::cout << '\n';

    std::cout << "lambdaGeneric(vecInt): " << lambdaGeneric(vecInt) << '\n';
    std::cout << "lambdaVector(vecInt): " << lambdaVector(vecInt) << '\n';
    std::cout << "lambdaVectorIntegral(vecInt): "
              << lambdaVectorIntegral(vecInt) << '\n';

    std::cout << '\n';
}
```

函数 `lambdaGeneric`（第 9 行）可以用任何具有成员函数 `size()` 的数据类型调用。函数 `lambdaVector`（第 10 行）更具体：它只接受 `std::vector`。函数 `lambdaVectorIntegral`（第 11 行）使用 C++20 概念 `std::integral`。因此，它只接受使用整型（例如 `int`）的 `std::vector`。要使用概念 `std::integral`，我必须包含头文件 `<concepts>`。我认为这个小程序不言自明。

```text
lambdaGeneric(deq): 3

lambdaGeneric(vecDouble): 4
lambdaVector(vecDouble): 4

lambdaGeneric(vecInt): 5
lambdaVector(vecInt): 5
lambdaVectorIntegral(vecInt): 5
```

Lambda，接受一个容器和一个 `std::vector`

![](img/c60a87adb7f61e2e82071d081bbb389a_208_0.png)

#### 类模板实参推导

程序 `templateLambdaVector.cpp` 中有一个你很可能忽略的特性。自 C++17 起，编译器可以从实参推导类模板的类型（第 20～22 行）。因此，不必冗长地写 `std::vector<int> myVec{1, 2, 3}`，你可以简单地写 `std::vector myVec{1, 2, 3}`。

### 4.7.2 检测 `this` 指针的隐式拷贝

C++20 编译器会检测你何时隐式拷贝 `this` 指针。通过拷贝隐式捕获 `this` 指针可能导致未定义行为。未定义行为本质上意味着程序的行为没有任何保证，例如以下情况：

#### 通过拷贝隐式捕获 this 指针

```cpp
// lambdaCaptureThis.cpp

#include <iostream>
#include <string>

struct LambdaFactory {
    auto foo() const {
        return [=] { std::cout << s << '\n'; };
    }
    std::string s = "LambdaFactory";
    ~LambdaFactory() {
        std::cout << "Goodbye" << '\n';
    }
};

auto makeLambda() {
    LambdaFactory lambdaFactory;

    return lambdaFactory.foo();
}

int main() {

    std::cout << '\n';

    auto lam = makeLambda();
    lam();

    std::cout << '\n';


}
```

该程序的编译按预期工作，但程序的执行并非如此。

![](img/c60a87adb7f61e2e82071d081bbb389a_210_0.png)

未定义行为导致段错误

你发现程序 lambdaCaptureThis.cpp 中的问题了吗？成员函数 foo（第 7 行）返回 lambda `[=] { std::cout << s << '\n'; }`，它隐式拷贝了 this 指针。这个隐式拷贝在第 17 行不是问题，但到了作用域结束时就成了问题。作用域结束意味着局部 LambdaFactory 的生命周期结束（第 19 行）。因此，调用 lam()（第 28 行）会触发未定义行为。

在这种情况下，C++20 编译器必须发出警告。

```text
<source>:8:18: warning: implicit capture of 'this' via '[=]' is deprecated in C++20 [-Wdeprecated]
    8 |         return [=] { std::cout << s << std::endl; };
      |                 ^
<source>:8:18: note: add explicit 'this' or '*this' capture
Execution build compiler returned: 0
Program returned: 139

Goodbye
```

C++20 诊断出一条警告

C++20 最后两个 lambda 特性在结合使用时非常方便：C++20 中的 lambda 在无状态时可以默认构造并支持拷贝赋值。此外，lambda 可以用于未求值上下文。

### 4.7.3 未求值上下文中的 Lambda，以及无状态 Lambda 的默认构造与拷贝赋值

#### 4.7.3.1 未求值上下文

以下代码片段包含一个函数声明和一个函数定义。
