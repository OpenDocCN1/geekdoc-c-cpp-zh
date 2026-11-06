

## 消除副作用

由于这种语言的性质，你没有什么灵丹妙药可以消除 C++ 中的副作用。不过，通过有纪律的编码，你可以遵循一些基本规则来消除副作用：

-   绝不修改传入的数据。
-   绝不依赖外部数据，也不修改函数外部的任何数据。
-   确保每次提供特定输入时，函数都产生完全相同的结果。
-   让函数目标明确，做好一件事，而不是勉强做好多件事。
-   让函数保持小巧。
-   绝不重复代码或使用样板代码。
-   使用 switch 语句而不是 if...then 语句。
-   只使用不可变数据。

清单 1-5 中展示的 NoSideEffects 示例演示了这些原则。无论你在函数外部做什么，对于特定输入，结果都不会改变。

### 清单 1-5：生成无副作用的代码

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int AddIt(const vector<int> Input,
          const int Start, const int End) {

    int Accumulate = 0;

    // Copy the full vector to a vector of the
    // correct size.
    vector<int> Process(End - Start);
    copy(&Input[Start], &Input[End], Process.begin());

    // Create a sum using a foreach loop.
    for (int Element : Process)
        Accumulate += Element;
    return Accumulate;
}

int main() {
    const vector<int> ThisVector = {12, 2, 4, 18, 7, 2};

    cout << "Sum of All Elements: " <<
        AddIt(ThisVector, 0, ThisVector.size()) << endl;
    cout << "Sum of Elements 1 through 4: " <<
        AddIt(ThisVector, 1, 5) << endl;
    return 0;
}
```

在这个示例中，除了 `AddIt()` 函数内部的 `Accumulate` 和 `Process` 变量之外，所有内容都按常量处理。因此，不存在副作用。任何变化都只发生在 `AddIt()` 内部，并且对于给定输入，`AddIt()` 将始终产生相同的输出。

为了只处理求和所需的 `ThisVector` 元素，`AddIt()` 使用 `copy()` 函数创建 `Input` 向量的副本。（现在不必担心向量的使用；你会在第5册第6章看到它们的详细解释。）请注意，通过使用标准库功能，你可以在很大程度上避免在这个函数中出现状态。甚至 `foreach` 循环（作为 `for` 循环的一种特殊情况实现）：

```cpp
for (int Element : Process)
    Accumulate += Element;
```

也避免了驱动循环通常所需的状态信息。理论上，你可以为这个问题创建一个完全不使用状态的递归解决方案。以下是该示例的输出：

```
Sum of All Elements: 45
Sum of Elements 1 through 4: 31
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_405_0.png)

你可能会想，为什么这个示例不使用数组而不是向量。`std::array` 的问题在于，你必须提供数组大小，例如 `array<int, 6> ThisVector = {12, 2, 4, 18, 7, 2};`，以便数组大小在编译时已知。然而，你在编译时并不知道 `Process` 数组的大小，因为对 `AddIt()` 的调用提供了可变的起始点和结束点。绕过这个问题的一种方法是使用 `constexpr` 设置，如前面清单 1-3 所示。

## 创建声明式 C++ 示例

尽管清单 1-5 在让 C++ 代码易于理解方面已经做了很多，并且比你原本可能预想的要可靠得多，但你还可以在不采用任何奇怪编码方式的情况下更进一步。清单 1-6 中展示的 Declarative 示例进一步依赖标准库，从而消除了对单独函数的需要。

### 清单 1-6：使用声明式编程技术

```cpp
#include <iostream>
#include <array>
#include <numeric>

using namespace std;

int main() {
  array<int, 6> ThisArray = {12, 2, 4, 18, 7, 2};
  cout << "Sum of All Elements: " <<
    accumulate(ThisArray.begin(), ThisArray.end(), 0)
    << endl;
  cout << "Sum of Elements 1 through 4: " <<
    accumulate(&ThisArray[1], &ThisArray[5], 0) << endl;
  return 0;
}
```

这个示例使用 `std::accumulate()` 函数来完成所需的工作。numeric 头文件中还有许多这类有趣的函数，你可以在 https://en.cppreference.com/w/cpp/header/numeric 查看。请注意，这些函数中的大多数需要 C++11、C++17 甚至 C++20 才能使用，因此它们更适合新开发。这个示例的输出与清单 1-5 的输出完全相同；只是技术发生了变化。

![](img/128ab511de4e7360e167e3b15cdd5dd0_406_0.png)

这个示例更有趣的方面之一是，你使用数组并让底层代码处理如何创建求和结果。这段代码完全不关心任何过程；它只是告诉标准库将这些值累加（求和）在一起。

还要注意用于提供计算起始点和结束点的两种方法。你需要的是一个地址。第一次调用使用 begin() 和 end() 函数来提供地址，第二次调用则依赖 [] 运算符提供的地址。

## 理解 auto 的作用

从 C++11 开始，你可以使用 auto 关键字来代替具体类型声明。当你事先不知道期望什么数据类型时，使用 auto 关键字会很方便。运行应用程序时，运行时会推断变量的类型，以便你可以正确地使用它。使用这种技术有助于你创建灵活的代码，即使它确实会稍微降低代码的清晰度。清单 1-7 中展示的 Auto 示例展示了如何使用这个关键字来执行各种任务。

### 清单 1-7：使用 auto 关键字

```cpp
#include <iostream>
#include <typeinfo>

using namespace std;

void DisplayIt(auto Value) {
    cout << Value << " is of the " <<
        typeid(Value).name() << " type." << endl;
}

int main() {
    auto Hello1 = "Hello There!";
    string Hello2 = "Hello Again!";
    auto Number1 = 1234;
    int Number2 = 5678;
    auto Float1 = 12.34;
    float Float2 = 56.78;
    auto Boolean1 = true;
    bool Boolean2 = false;

    DisplayIt(Hello1);
    DisplayIt(Hello2);
    DisplayIt(Number1);
    DisplayIt(Number2);
    DisplayIt(Float1);
    DisplayIt(Float2);
    DisplayIt(Boolean1);
    DisplayIt(Boolean2);

    return 0;
}
```

代码首先创建若干变量——一半使用标准声明，一半使用 auto 关键字。然后它调用 `DisplayIt()` 来显示变量值和类型。通过使用 auto 关键字，`DisplayIt()` 可以接受所有这些输入并适当地与它们交互。

尽管这段代码可以工作，但它有一个问题。`typeid()` 函数通常会根据你使用的编译器返回经过修饰的结果。下面是一个示例：

![](img/128ab511de4e7360e167e3b15cdd5dd0_408_0.png)

```
Hello There! is of the PKc type.
Hello Again! is of the NSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEE type.
1234 is of the i type.
5678 is of the i type.
12.34 is of the d type.
56.78 is of the f type.
1 is of the b type.
0 is of the b type.
```

尽管你大概能弄明白 i、d、f 和 b 这些条目，但 PKc 条目却是个谜，更别提尝试确定以 NSt7 开头的下一行的类型了。你很可能希望输出采用人类可读的形式，这需要几个额外步骤，首先添加两个新的 `#include` 条目。

```cpp
#include <memory>
#include <cxxabi.h>
```

`DemangleIt()` 函数接收来自 `DisplayIt()` 的经过修饰的输入，并将其转换为人类可读的字符串，如下所示：

```cpp
string DemangleIt(const char* Mangled) {
    int Status;
    unique_ptr<char[], void(*)(void*)> Result(
        abi::__cxa_demangle(Mangled, 0, 0, &Status), free);
    return Result.get() ? string(Result.get()) : "Error";
}
```

