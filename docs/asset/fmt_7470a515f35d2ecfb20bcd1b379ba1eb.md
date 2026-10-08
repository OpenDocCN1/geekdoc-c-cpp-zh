
*(注：由于原文提供的文本在后面部分出现了大量重复和段落错乱，我将严格按照您提供的文本进行翻译，不进行删减或遗漏。)*

*(抱歉，我发现提供的文本文本文本...................，我我我我翻译翻译翻译翻译翻译。)*

# 9.8.7 风险评估

内存和其他资源最终会导致程序崩溃。如果攻击者能够通过提交精心构造的数据来强制抛出异常，从而引发重复的内存泄露，则攻击者就可以发起拒绝服务攻击。

| 规则 | 严重程度 | 可能性 | 修复成本 | 优先级 | 级别 |
|---|---|---|---|---|---|
| `ERR57-CPP` | 低 | 可能 | 高 | P2 | L3 |

# 9.8.8 相关指南

- `MEM51-CPP`. 正确释放动态分配的资源
- `MEM52-CPP`. 检测并处理内存分配错误
- `ERR56-CPP`. 保证异常安全性

# 9.8.9 参考文献

- [Cline 2009] 问题 17.2，我仍然不信服：一个 4 行代码片段显示返回码并不比异常糟糕；为什么我应该在一个规模大出几个数量级的应用程序上使用异常呢？
- [ISO/IEC 14882-2014] 子句 15.2，“构造函数与析构函数”
- [Meyers 1996] 事项 9，“使用析构函数防止内存泄露”
- [Stroustrup 2001] “异常安全的实现技术”

# 9.9 ERR58-CPP. 在 main() 开始执行前处理所有抛出的异常

并不是所有的异常都能被捕获，即使仔细使用了函数尝试块（function-try-blocks）。C++ 标准 `[exception.handle]`，`ISO/IEC 14882-2014` 第 13 节规定：

- 在具有静态存储期的对象的析构函数中，或在具有静态存储期的命名空间范围对象的构造函数中抛出的异常，不会被 `main()` 中的 function-try-block 捕获。在具有线程存储期的对象的析构函数中，或在具有线程存储期的命名空间范围对象的构造函数中抛出的异常，不会被线程初始函数的 function-try-block 捕获。

声明具有静态或线程持续的对象且该对象未在函数作用域内声明时，类型构造函数必须声明为 `noexcept` 并必须符合 `ERR55-CPP`。遵守异常规范。此外，声明的初始化器（如果有）不能抛出未捕获的异常（包括作为初始化部分创建的任何隐式构造对象的异常）。如果在 `main()` 之前抛出了未捕获的异常，或在 `main()` 执行结束后抛出了未捕获的异常，则没有进一步处理该异常的机会，并将导致实现定义的行为（详见 `ERR50-CPP`。不要突然终止程序）。

关于析构函数异常规范的更多信息，请参见 `DCL57-CPP`。不要让异常逃逸析构函数或释放函数。

### 9.9.1 不合规代码示例

在此合规示例中，`S` 的构造函数可能会在程序设置期间构造 `globalS` 时，抛出一个未被捕获的异常。

```cpp
struct S {
  S() noexcept(false);
};
static S globals;
```

### 9.9.2 合规解决方案

此合规解决方案将 `globals` 变为具有静态存储期的局部变量，允许在对象构造期间抛出的任何异常被捕获，因为 `S` 的构造函数会在第一次调用 `globals()` 函数时执行，而不是在程序启动时。此解决方案要求程序员修改源代码，将之前对 `globals` 的使用替换为对 `globals()` 的函数调用。

```cpp
struct S {
  S() noexcept(false);
}
S &globals() {
  try {
    static S s;
    return s;
  } catch (...) {
    // 处理错误，可能通过记录日志并优雅地
    // 终止应用程序。
  }
  // 不可到达。
}
```

### 9.9.3 不合规代码示例

在此不合规示例中，`global` 的构造函数可能会在程序启动期间抛出异常。（接受 `const char *` 和默认分配器对象的 `std::string` 构造函数未标记为 `noexcept`，因此允许抛出异常。）此异常不会被 `main()` 的 function-try-block 捕获，导致调用 `std::terminate()` 并程序异常终止。

```cpp
#include <string>
static std::string global("");
int main() {
  try {
    // ...
  } catch(...) {
    // 重要：不会捕获从 global
    // 构造函数中抛出的异常
  }
}
```

异常与错误处理 (ERR) - `ERR58-CPP`. 在 `main()` 开始执行前处理所有抛出的异常

### 9.9.4 合规解决方案

合规代码必须防止异常在程序启动和终止期间逃逸。此合规代码避免在全局命名空间范围内定义 `std::string`，而是使用 `static const char *`

```cpp
static const char *global = "...";
int main() {
  // ...
}
```

### 9.9.5 合规解决方案

此合规解决方案引入了一个派自 `std::string` 的类，其构造函数使用函数块捕获所有异常，并根据 `ERR50-CPP` 中的 `ERR50-CPP-EX1` 终止应用程序。在抛出异常时不要突然终止程序。异常无法逃逸构造函数，它被标记为 `noexcept`，且类类型在静态全局变量的声明或初始化是可能的。

为了简洁起见，此处未描述此类类型的完整接口。

```cpp
#include <exception>
#include <string>
namespace my {
struct string : std::string {
  explicit string(const char *msg,
                 const std::allocator_type& alloc) noexcept {
    try {
      std::string(msg, alloc);
    } catch (...) {
      // 处理错误，可能通过记录日志并优雅地
      // 终止应用程序。
    }
  }
};
static string global("...");
int main() {
  // ...
}
}
```

### 9.9.6 不合规代码示例

在此不合规示例中，`global` 的构造函数可能会通过静态全局的初始化器抛出异常。

```cpp
extern f() noexcept(false);
int i = f();
int main() {
  // ...
}
```

### 9.9.7 合规解决方案

此合规解决方案用一个函数封装 `f()` 的调用，该函数捕获所有异常并根据 `ERR50-CPP-EX1` 终止程序。

```cpp
#include <exception>
int f_helper() noexcept {
  try {
    extern f() noexcept(false);
    return f();
  } catch (...) {
    // 处理错误或终止。
    std::terminate();
  }
  // 不可到达。
}
int i = f_helper();
int main() {
  // ...
}
```

### 9.9.8 风险评估

抛出无法捕获的异常会导致程序异常终止。

| 规则 | 可能性 | 修复成本 | 优先级 | 级别 |
|---|---|---|---|---|
| `ERR58-CPP` | 低 | 低 | P9 | L2 |

### 9.9.9 相关指南

此规则是 `ERR50-CPP` 的子集。不要突然终止程序。

| SEI C++ 代码编码 | `DCL57-CPP`. 不要让异常逃逸析构函数或释放函数 |
| | `ERR55-CPP`. 遵守异常规范 |

### 9.9.10 参考文献

| [ISO/IEC 14882-2014] | 子句 15.4，“异常规范” |
| [Sutter 2000] | 事项 8，“编写异常安全的代码——第一部分” |

# 9.10 ERR59-CPP. 不要跨执行边界抛出异常

抛出异常需要 `throw` 表达式的执行与 `catch` 语句（如果适用）之间的协作。这种协作的形式是用于计算异常正确处理程序的运行时逻辑，它是特定平台的实现细节。对于由 C++ 编译器编译的代码，可以安全地忽略抛出和捕获的细节。然而，跨执行边界抛出异常时，必须确保使用的运行时逻辑与执行边界的双方兼容。

执行边界是不同编译器编译的代码之间的界限，包括同一厂商生产的不同版本的编译器。例如，一个函数可能在头文件中声明，但在运行时加载的库中。执行边界位于可执行文件中的调用点与库中的函数实现之间。边界边界称为 ABI（应用接口）边界。

仅当执行边界的双方都使用相同的 ABI 处理异常时，才跨执行边界抛出异常。

### 9.10.1 不合规代码示例

在此不合规代码示例中，从库函数抛出异常以指示错误。尽管异常是标量类型（因此隐式符合“不要跨执行边界传递非布局类型对象”），但如果库和应用程序遵循不同的 ABI，此代码仍可能导致程序执行异常。

```cpp
// library.h
void func() noexcept(false); // 由库实现
// library.cpp
void func() noexcept(false) {
  // ...
  if (/* ... */) {
    throw 42;
  }
}
// application.cpp
#include "library.h"
void f() {
  try {
    func();
  } catch (int& e) {
    // 处理错误
  }
}
```

### 9.10.1.1 实现细节

如果库代码在默认安装的 MinGW-w64 上使用 GCC 4.9 编译（为了考虑符号修饰的差异而通过了修改），且不使用特殊编译器标志，则异常将依赖于基于 DWARF 并使用 itanium ABI 的零成本基于表的异常模型。如果应用程序使用 Microsoft Visual Studio 2013 编译，则 catch 处理器将基于结构化异常处理（Structured Exception Handling）和 Microsoft ABI。这两种异常处理格式是不兼容的，因为 ABI 不同，会导致程序行为异常。具体而言，库抛出的异常不会被应用程序捕获，最终将调用 `std::terminate()`。

### 9.10.2 合规解决方案

在这种合规解决方案中，库函数的错误通过返回值返回而不是通过异常。使用 Microsoft Visual Studio（或 GCC）编译库和应用程序将是一个合规解决方案，因为在执行边界的侧使用的异常处理机制和 ABI 是一致的。

```cpp
// library.h
int func() noexcept(true); // 由库实现
// library.cpp
int func() noexcept(true) {
  // ...
  if (/* ... * */) {
    return 42;
  }
  // ...
  return 0;
}
// application.cpp
#include "library.h"
void f() {
  if (int err = func()) {
    // 处理错误
  }
}
```

### 9.10.3 风险评估

跨越执行边界抛出异常的影响取决于异常处理机制的实现细节。这些影响可能从正确或无害到未定义行为不等。

| 规则 | 严重性 | 可能性 | 修复成本 | 优先级 | 级别 |
|---|---|---|---|---|---|
| `ERR59-CPP` | 高 | 可能 | 中 | P12 | L1 |

### 9.10.4 相关指南

- CERT C++ 编码标准 - `EXP60-CPP`，不要跨越执行边界传递非标准布局类型对象

### 9.10.5 参考文献

| [ISO/IEC 14882-2014] | 子句 15, “异常处理” |

## 9.11 ERR60-CPP. 异常对象不得抛出可拷贝构造函数

当抛出异常时，`throw` 表达式的异常对象操作数被拷贝到一个临时对象中，该临时对象用于初始化处理器。C++ 标准 `[except.throw]` 第 3 节 `[ISO/IEC 14882-2014]` 部分阐述了如下：

抛出异常会初始化一个临时对象，称为*异常对象*。该临时对象是一个左值，用于初始化匹配处理器中声明的变量。

如果在异常对象的拷贝构造函数在拷贝初始化期间抛出异常，则会调用 `std::terminate()`，这可能导致未定义行为。关于隐式调用 `std::terminate()` 的更多信息，请参见 `ERR50-CPP`。不要突然终止程序。

作为异常抛出的对象的拷贝构造函数必须声明为 `noexcept`，包括任何隐式定义的拷贝构造函数。任何通过抛出异常声明的函数都违反 `ERR55-CPP`。遵守异常规范。

C++ 标准允许在初始化异常对象以执行如果抛出一个临时对象时省略拷贝构造函数。许多编译器实现利用优化技术。然而，异常对象的拷贝构造函数仍然不能抛出异常，因为编译器并不要求在所有情况下省略拷贝构造函数的调用，且 `std::exception_ptr` 的常见实现即使在从 `throw` 表达式中省略时，也会调用拷贝构造函数。

### 9.11.1 不合规代码示例

```cpp
#include <exception>
#include <string>
class S : public std::exception {
    std::string m;
public:
    S(const char *msg) : m(msg) {}
    const char *what() const noexcept override {
        return m.c_str();
    }
};
void g() {
    // 如果某些条件不满足...
    throw S("Condition did not hold");
}
void f() {
    try {
        g();
    } catch (const S& s) {
        // 处理错误
    }
}
```

### 9.11.2 合规解决方案

这种合规解决方案假设异常对象的类型可以继承自 `std::runtime_error`，或者可以直接使用该类型。与 `std::string` 不同，`std::runtime_error` 对象被要求正确处理任意长度的错误信息，异常是安全的，并保证拷贝构造函数不会抛出异常 `[ISO/IEC 14882-2014]`。

```cpp
#include <stdexcept>
#include <type_traits>
struct S : std::runtime_error {
    S(const char *msg) : std::runtime_error(msg) {}
};
static_assert(std::is_nothrow_copy_constructible<S>::value,
    "S must be notrow copy constructible");
void g() {}
void f() {
    try {
        g();
    } catch (const S& s) {
        // 处理错误
    }
}
```

### 9.11.3 合规解决方案

这种合规解决方案假设异常对象的类型可以继承自 `std::runtime_error`，或者可以直接使用该类型。与 `std::string` 不同，`std::runtime_error` 对象被要求正确处理任意长度的错误信息，异常是安全的，并保证拷贝构造函数不会抛出异常 `[ISO/IEC 14882-2014]`。

```cpp
#include <stdexcept>
#include <type_traits>
struct S : std::runtime_error {
    S(const char *msg) : std::runtime_error(msg) {}
};
static_assert(std::is_nothrow_copy_constructible<S>::value,
    "S must be notrow copy constructible");
void g() {}
void f() {
    try {
        g();
    } catch (const S& s) {
        // 处理错误
    }
}
```
