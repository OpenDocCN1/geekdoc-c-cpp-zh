
析构函数、`operator delete` 或 `operator delete []` 在抛出异常时终止会导致正常终止。

C++ 标准 `[except.handle]` 第 15 节指出：

> 如果在处理另一个异常期间析构对象时抛出异常，程序将终止。

### 2.8.1 不合规代码示例

在这个不合规的代码示例中，类析构函数可能会抛出异常，因为它不满足 `noexcept` 保证。

```cpp
#include <stdexcept>

class S {
    bool has_error() const;
public:
    ~S() {
        // 异常
        if (has_error()) {
            throw std::logic_error("Something bad");
        }
    }
};
```

## 2.8.2 不合规代码示例 (std::uncaught_exception())

在析构函数中使用 `std::uncaught_exception()` 可以解决不合规代码示例所示的终止问题。然而，通过绕过正常的析构处理，这种方法可能会导致资源泄漏。

```cpp
#include <stdexcept>
#include <stdexcept>

class S {
    bool has_error() const;
public:
    ~S() noexcept(false) {
        // 正常处理
        if (has_error() && !std::uncaught_exception()) {
            throw std::logic_error("Something bad");
        }
    }
};
```

## 2.8.3 不合规代码示例 (函数异常块)

这个不合规代码示例以及后面的合规解决方案假设一个析构函数可以抛出异常的 `Bad` 类。尽管该类违反了此规则，但假设该类无法被修改。

```cpp
// 假设该类由第三方提供，用户无法对其进行修改。
class Bad {
    ~Bad() noexcept(false);
};
```

为了安全地使用 `Bad` 类，`SomeClass` 析构函数尝试通过吸收异常来处理来自 `Bad` 的异常。

```cpp
class SomeClass {
    Bad bad_member;
public:
    ~SomeClass() {
        try {
            // ...
        } catch(...) {
            // 处理来自 Bad 析构函数的异常。
        }
    }
};
```

然而，C++ 标准 `[except.handle]` 第 15 节指出：

> 如果控制到达构造函数或析构函数的函数异常块处理程序的末尾，当前处理的异常将被重新抛出。

因此，捕获的异常将不可避免地从 `SomeClass` 析构函数逃逸，因为它在到达函数异常块的末尾时会被隐式重新抛出。

### 2.8.4 合规解决方案

析构函数无论是否存在活动异常都应该表现相同。通常这意味着它应该只调用不会抛出异常的操作，或者它应该处理所有异常且不抛出（隐式地）。该合规解决方案与之前的不合规代码示例的区别在于，`SomeClass` 析构函数有一个显式的 `return` 语句。该语句阻止了控制到达异常处理程序的末尾。

## 声明与初始化 (DCL) - DCL57-CPP. 不要让异常从析构函数或释放内存函数逃逸

`bad_member` 被销毁。它也会捕获函数-try-block 复合语句中抛出的任何异常，但 `SomeClass` 析构函数不会通过抛出异常来终止。

```cpp
class SomeClass {
  Bad bad_member;
public:
  ~SomeClass()
  try {
    // ...
  } catch(...) {
    // 捕获从不规范的成员对象
    // 基类子类的析构函数抛出的异常。

    // 注意：运行到析构函数-try-block 的末尾会导致
    // 被捕获的异常隐式重新抛出，但显式的
    // 返回语句将防止这种情况发生。
    return;
  }
};
```

## 2.8.5 不规范代码示例

在此不规范代码中，全局释放内存函数被声明为 `noexcept(false)`，并在某些条件未恰当满足时抛出异常。然而，从释放内存函数中抛出异常会导致未定义行为。

```cpp
#include <stdexcept>

void operator delete(void*ptr) noexcept(false) {
  if (perform_dealloc(ptr)) {
    throw std::logic_error("Something bad");
  }
}
```

### 2.8.6 合规解决方案

合规解决方案在释放内存失败时不抛出异常，而是尽可能优雅地失败。

```cpp
#include <cstdlib>
#include <stdexcept>

bool perform_dealloc(void *);
void log_failure(const char *);

void operator delete(void *ptr) noexcept(true) {
    if (perform_dealloc(ptr)) {
        log_failure("Deallocation of pointer failed");
        std::exit(1); // 失败，但仍调用析构函数
    }
}
```

### 2.8.7 风险评估

尝试从析构函数或释放内存函数中抛出异常会导致未定义行为，导致资源泄漏或拒绝服务攻击。

| 规则 | 严重性 | 可能性 | 修复成本 | 优先级 | 级别 |
| --- | --- | --- | --- | --- | --- |
| DCL57-CPP | 低 | Likely | Medium | P6 | L3 |

### 2.8.8 相关指南

| SEI CERT C++ 编码标准 | 规则描述 |
| --- | --- |
| | ERR55-CPP. 遵守异常规范 |
| | ERR50-CPP. 不要强制终止程序 |
| MISRA C++:2008 | Rule 15-5-1 (强制性) |

## 2.8.9 参考文献

| | |
| --- | --- |
| [Henricson 1997] | 建议 12.5，不要让在堆栈回溯期间调用的析构函数抛出异常 |
| [ISO/IEC 14882-2014] | 子句 3.4.7.2，“释放内存函数”、子句 15.2，“构造函数与析构函数”、子句 15.3，“处理异常”、子句 15.4，“异常规范” |
| [Meyers 2005] | 事项 8，“防止异常从析构函数中” |
| [Sutter 2000] | “永远不允许异常从析构函数或重载的 `operator delete()` 中逃逸”（第 29 页） |

## 2.9 DCL58-CPP. 不要修改标准命名空间

命名空间为声明引入了新的声明区域，减少了与其他声明区域发生标识冲突的可能性。命名空间的一个特性是它们可以进一步扩展，即使在不同的编译单元中。例如，以下声明是良好的。

```cpp
namespace MyNamespace {
int i;
}

namespace MyNamespace {
int i;
}

void f() {
  MyNamespace::i = MyNamespace::i = 12;
}
```

标准库引入了 `std` 命名空间用于标准提供的声明，如 `std::string`、`std::vector` 和 `std::for_each`。然而，除非在特殊情况下否则在 `std` 命名空间中引入新声明是未定义行为。C++ 标准第 1 和第 2 段 `[ISO/IEC 14882-2014]` 规定如下：

+ 1 如果 C++ 程序向 `std` 命名空间或名为 `std` 的命名空间添加声明或定义，除非另有规定，否则行为是未定义的。只有当声明依赖于用户定义类型且该特化符合标准库对原始模板的要求且未被显式禁止时，程序才允许向 `std` 命名空间添加任何标准库模板的模板特化。

2 如果 C++ 程序声明了以下内容，行为是未定义的：

* 标准库类模板的任何成员函数的显式特化，

* 标准库类或类模板的任何成员函数模板的显式特化，

* 标准库类或类模板的任何成员类模板的显式或部分特化。

除了限制对 `std` 命名空间的扩展外，C++ 标准 `[namespace.posix]` 第 1 段进一步阐述了以下内容：

> 如果 C++ 程序向 `posix` 命名空间或 `posix` 命名空间内的命名空间添加声明或定义，除非另有规定，否则行为是未定义的。`posix` 命名空间是保留供使用的。

### 2.9.5 合规解决方案

在此合规解决方案中，`std` 命名空间添加了 `std::plus` 的特化，但该特化依赖于用户定义的类型，并满足标准模板库对原始模板的要求，因此符合此规则。然而，由于 `MyString` 是由 `std::string` 构建的，此合规解决方案调用了转换构造函数，而上一个合规解决方案则没有。

```cpp
#include <functional>
#include <iostream>
#include <string>

class MyString {
    std::string data;
public:
    MyString(const std::string &data) : data(data) {}

    const std::string &get_data() const { return data; }
};

namespace std {
template <> struct plus<MyString> {
    MyString operator(const MyString &lhs, const MyString &rhs)
    const {
        return lhs.get_data() + rhs.get_data();
    }
};
}

void f() {
    std::string s1("My String");
    MyString s2(" + Your String");
    std::plus<MyString> p;

    std::cout << p(s1, s2).get_data() << std::endl;
}
```

### 2.9.6 风险评估

修改标准命名空间会导致 C++ 标准库中出现未定义行为。

| 规则 | 严重性 | 可能性 | 修复成本 | 优先级 | 级别 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| DCL58-CPP | 高 | 不可能 | 中 | P6 | L2 |

### 2.9.7 相关指南

| SEI CERT C++ 编码标准 | 描述 |
| :--- | :--- |
| DCL51-CPP | 不要声明或定义保留标识符 |

### 2.9.8 参考文献

| 参考文献 | 详情 |
| :--- | :--- |
| [INCITS 2014] | Issue 2139, "什么是用户定义类型?" |
| [ISO/IEC 14882-2014] | 子条款 17.6.4.2.1, "Namespace std", 子条款 17.6.4.2.2, "Namespace posix" |

## 2.10 DCL59-CPP. 不要在头文件中定义匿名命名空间

匿名命名空间（Unnamed namespaces）用于定义一个对编译单元是唯一的命名空间，其中包含的名称默认具有内部链接性。C++ 标准 `[namespace.unnamed]` [ISO/IEC 14882-2014] 第 1 节规定：

```cpp
一个匿名命名空间定义的行为等同于被替换为：
inline namespace unique (/* 空正体 */)
using namespace unique;
namespace unique { namespace-body }
```

其中当且仅当 `inline` 出现在匿名命名空间定义中时，编译单元中所有 `unique` 的出现处都被替换为同一个标识符，且该标识符与整个程序中的所有其他标识符都不同。

生产级 C++ 代码经常使用头文件作为编译单元间共享代码的。头文件是任何通过 `#include` 指令插入到编译单元中的文件。不要在头文件中定义匿名命名空间。当在头文件中定义匿名命名空间时，可能会导致意外的结果。由于默认的内部链接，每个编译单元都将定义其在在该编译单元内被 ODR 使用的命名空间成员的唯一实例。这可能导致意外的结果、导致生成的可执行文件膨胀，或者由于违反定义规则（ODR）而无意中触发未定义行为。

### 2.10.1 不合规代码示例

在此不合规代码示例中，变量 `v` 定义在头文件的匿名命名空间中，并在两个独立的编译单元中访问。每个编译单元都会打印 `v` 的当前值并为其赋新值。然而，由于 `v` 定义在匿名命名空间内，每个编译单元都在操作其自己的 `v` 实例，导致了意外的输出。

```cpp
// a.h
#ifndef A_HEADER_FILE
#define A_HEADER_FILE

namespace {
int v;
}

#endif // A_HEADER_FILE

// a.cpp
#include "a.h"
#include <iostream>

void f() {
    std::cout << "f(): " << v << std::endl;
    v = 42;
    // ...
}

// b.cpp
#include "a.h"
#include <iostream>

void g() {
    std::cout << "g(): " << v << std::endl;
    v = 100;
}

int main() {
    extern void v;
    f(); // 打印 v，将其设置为 42
    g(); // 打印 v，将其设置为 100
    f();
    g();
    return 0;
}
```

声明与初始化 (DCL) - DCL59-CPP. 不要在头文件中定义匿名命名空间

执行该程序时，它会打印以下内容：

```
f(): 0
g(): 0
f(): 42
g(): 100
```

### 2.10.2 合规解决方案

在此合规解决方案中，`v` 只在一个编译单元中定义，但对所有编译单元外部可见，从而实现了预期的行为。

```cpp
// a.h
#ifndef A_HEADER_FILE
#define A_HEADER_FILE

extern int v;

#endif // A_HEADER_FILE

// a.cpp
#include "a.h"
#include <iostream>

// 定义变量 v
void f() {
    std::cout << "f(): " << v << std::endl;
    v = 42;
// ...
}

// b.cpp
#include "a.h"
#include <iostream>

void g() {
    std::cout << "g(): " << v << std::endl;
    v = 100;
}

int main() {
    extern void f();
    f(); // 打印 v，将其设置为 42
    g(); // 打印 v，将其设置为 100
    f(); // 打印 v，将其设回 42
    g(); // 打印 v，将其设回 100
}
```

SEI CERT C++ 编码标准 (2016版) | V01

工程研究所 | 卡内基梅隆大学

[声明] 公开发发布且不受限制。

声明与初始化 (DCL) - DCL59-CPP. 不要在头文件中定义匿名命名空间

执行该程序时，它打印以下内容：

```
f(): 0
g(): 42
f(): 100
g(): 42
```

### 2.10.3 不合规代码示例

在此不合规示例中，变量 `v` 定义在头文件的匿名命名空间中，并且定义的内联函数 `get_v()`。从多个编译单元（如 `f()` 和 `g()` 的实现所示）访问该变量违反了定义规则，因为 `get_v()` 的定义在每个单元中是不相同的。

```cpp
// a.h
#ifndef A_HEADER_FILE
#define A_HEADER_FILE

namespace {
int v;
}

inline int get_v() { return v; }

#endif // A_HEADER_FILE

// a.cpp
#include "a.h"
void f() {
    get_v();
// ...
}

// b.cpp
#include "a.h"
void g() {
    get_v();
// ...
}
```

关于违反定义规则的更多信息，请参见 DCL60-CPP。

### 2.10.4 合规解决方案

在此合规解决方案中，`v` 只在一个编译单元中定义，但对所有编译单元可见，并可以通过内联函数 `get_v()` 访问。

```cpp
// a.h
#ifndef A_HEADER_FILE
#define A_HEADER_FILE

extern int v;

inline int get_v() {
    return v;
}

#endif // A_HEADER_FILE

// a.cpp
#include "a.h"
// 被 get_v() 外部使用
int v;

void f() {
    get_v();
// ...
}

// b.cpp
#include "a.h"
void g() {
    get_v();
// ...
}
```
