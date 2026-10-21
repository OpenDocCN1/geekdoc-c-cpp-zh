

根据单一定义规则（ODR），一个变量或实体必须在恰好一个翻译单元中被定义——除非该变量或实体被声明为内联。

即使使用包含保护也不起作用：

```
#ifndef MYHEADER_HPP
#define MYHEADER_HPP

class MyClass {
    static std::string msg;
    ...
};
std::string MyClass::msg{"OK"};    // Link ERROR if included by multiple CPP files

#endif
```

问题不在于头文件可能会被多次包含；问题在于两个不同的 CPP 文件都包含了该头文件，从而导致两者都定义了 MyClass::msg。

出于同样的原因，如果你在头文件中定义了类的对象，也会得到链接错误：

```
class MyClass {
    ...
};
MyClass myGlobalObject;            // Link ERROR if included by multiple CPP files
```

## Workarounds

对于某些情况，存在变通方法：

- 你可以在类/struct 中初始化整型和枚举类型的 static const 数据成员：

```
class MyClass {
    static const bool trace = false;  // OK, literal type
    ...
};
```

然而，这仅允许用于字面量类型，例如基本整型、浮点型或指针类型，或仅用常量表达式初始化非静态数据成员且没有用户定义或虚析构函数的类。此外，一旦你需要成员的位置（例如将其绑定到引用），你仍需要在一个翻译单元中提供定义。

- 你可以定义一个返回静态局部变量的内联函数：

```
inline std::string& getMsg() {
    static std::string msg{"OK"};
    return msg;
}
```

- 你可以定义一个返回值的静态成员函数：

```
class MyClass {
    static std::string& getMsg() {
        static std::string msg{"OK"};
        return msg;
    }
    ...
};
```

- 你可以使用变量模板（自 C++14 起）：

```
template<typename T = std::string>
T myGlobalMsg{"OK"};
```

- 你可以为静态成员定义一个类模板：

```
template<typename = void>
class MyClassStatics
{
    static std::string msg;
};

template<typename T>
std::string MyClassStatics<T>::msg{"OK"};
```

然后甚至可以从它派生：

```
class MyClass : public MyClassStatics<>
{
    ...
};
```

然而，所有这些方法都会导致显著的开销、可读性降低和/或使用全局变量的不同方式。此外，全局变量的初始化可能会推迟到首次使用时，这会禁用在程序启动时初始化对象的应用（例如使用对象来监控进程）。

## 3.2 Using Inline Variables

现在，有了 inline，你可以通过仅在头文件中定义它来拥有一个全局可用的对象，而该头文件可能会被多个 CPP 文件包含：

```
class MyClass {
    inline static std::string msg{"OK"};  // OK since C++17
    ...
};
```

```
inline MyClass myGlobalObj;  // OK even if included/defined by multiple CPP files
```

形式上，这里使用的 inline 与声明为 inline 的函数具有相同的语义：

- 它可以在多个翻译单元中被定义，前提是所有定义都相同。
- 它必须在每个使用它的翻译单元中被定义。

两者都通过从同一个头文件包含定义来实现。 resulting 程序的行为就好像只有一个变量一样。

## 3.3 constexpr Now Implies inline for Static Members

对于静态数据成员，constexpr 现在意味着 inline，因此自 C++17 起，以下声明定义了静态数据成员 n：

```
struct D {
    static constexpr int n = 5; // C++11/C++14: declaration
    // since C++17: definition
};
```

也就是说，它等同于：

```
struct D {
    inline static constexpr int n = 5;
};
```

请注意，在 C++17 之前，你通常只需要声明而不需要对应的定义。考虑以下声明：

```
struct D {
    static constexpr int n = 5;
};
```

如果不需要 D::n 的定义，这就足够了，而在 D::n 仅按值传递时就是这种情况：

```
std::cout << D::n; // OK (ostream::operator<<(int) gets D::n by value)
```

如果 D::n 按引用传递给非内联函数和/或调用未被优化掉，则这是无效的。例如：

```
int twice(const int& i);
std::cout << twice(D::n);    // was often an ERROR
```

此代码违反了单一定义规则（ODR）。使用优化编译器构建时，它可能按预期工作，也可能因缺少定义而给出链接错误。使用无优化构建时，它几乎肯定会被拒绝，因为缺少 D::n 的定义。¹ 创建指向静态成员的指针更可能导致因缺少定义而链接错误（但在某些编译器模式下仍可能工作）：

```
const int* p = &D::n;          // was usually an ERROR
```

因此，在 C++17 之前，你必须在恰好一个翻译单元中定义 D::n：

```
constexpr int D::n;            // C++11/C++14: definition
                               // since C++17: redundant declaration (deprecated)
```

现在，使用 C++17 构建时，类内部的声明本身就是一个定义，因此上述所有示例现在在没有前述定义的情况下都是有效的。前述定义仍然有效，但是一个已弃用的冗余声明。

## 3.4 Inline Variables and thread_local

通过使用 thread_local，你还可以使一个内联变量对每个线程唯一：

```
struct ThreadData {
    inline static thread_local std::string name;      // unique name per thread
    ...
};

inline thread_local std::vector<std::string> cache;   // one cache per thread
```

作为一个完整示例，考虑以下头文件：

`lang/inlinethreadlocal.hpp`

```
#include <string>
#include <iostream>

struct MyData {
    inline static std::string gName = "global";          // unique in program
    inline static thread_local std::string tName = "tls"; // unique per thread
    std::string lName = "local";                          // for each object
    ...
    void print(const std::string& msg) const {
        std::cout << msg << '\n';
        std::cout << "- gName: " << gName << '\n';
        std::cout << "- tName: " << tName << '\n';
        std::cout << "- lName: " << lName << '\n';
    }
};

inline thread_local MyData myThreadData;  // one object per thread
```

你可以在包含 main() 的翻译单元中使用它：

`lang/inlinethreadlocal1.cpp`

```
#include "inlinethreadlocal.hpp"
#include <thread>

void foo();

int main()
{
    myThreadData.print("main() begin:");

    myThreadData.gName = "thread1 name";
    myThreadData.tName = "thread1 name";
    myThreadData.lName = "thread1 name";
    myThreadData.print("main() later:");

    std::thread t(foo);
    t.join();
    myThreadData.print("main() end:");
}
```

你也可以在另一个定义 foo() 的翻译单元中使用头文件，该函数在不同的线程中被调用：

`lang/inlinethreadlocal2.cpp`

```
#include "inlinethreadlocal.hpp"

void foo()
{
    myThreadData.print("foo() begin:");

    myThreadData.gName = "thread2 name";
    myThreadData.tName = "thread2 name";
    myThreadData.lName = "thread2 name";
    myThreadData.print("foo() end:");
}
```

程序的输出如下：

```
main() begin:
```
