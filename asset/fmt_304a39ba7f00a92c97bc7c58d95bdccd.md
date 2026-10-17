
该解决方案产生以下输出。

| Before throw: Instances: 0 |
| f(): Instances: 1 |
| From catch: Instances: 0 |
| After catch: Instances: 0 |

## 9.3.3 风险评估

使用 `setjmp()` 和 `longjmp()` 可能会由于资源未被妥善销而导致拒绝服务攻击。

| 规则 | 严重性 | 可能性 | 修复成本 | 优先级 | 级别 |
| --- | --- | --- | --- | --- | --- |
| ERR52-CPP | 低 | 可能 | 中 | P4 | L3 |

## 9.3.4 参考文献

| [Henricson 1997] | 规则 13.3, 不要使用 setjmp() 和 longjmp() |
| --- | --- |
| [ISO/IEC 14882-2014] | 子句 18.10, “其他运行时支持” |

## 9.4 ERR53-CPP. 不要在构造函数或析构函数的函数-try-block 处理器中引用基类或类数据成员

当异常被构造函数中的函数-try-block 处理器捕获时，对象的任何完全构造的类和类成员在进入处理器之前都会被销毁 [ISO/IEC 14882-2014]。同样，当异常被析构函数中的函数-try-block 处理器捕获时，对象的所有基类和非变体成员在进入处理器之前都会被销毁。由于这种行为，C++ 标准 [except.handle] 第 10 段规定如下：

- 在该对象的构造函数或析构函数的函数-try-block 处理器中引用对象的任何非静态成员或基类将导致未定义行为。

不要在构造函数或析构函数的函数-try-block 处理器中引用基类或类数据成员。这样做会导致未定义行为。

### 9.4.1 不合规代码示例

在不合规代码示例中，类 `C` 的构造函数使用函数-try-block 处理异常。它通过检查其成员字段 `str` 产生了未定义行为。

```cpp
#include <string>

class C {
  std::string str;
public:
  C(const std::string &s) : str(s) (
    // ...
  ) catch (...) {
    if (!str.empty()) {
      // ...
    }
  }
}
```

![](img/03d7c1b3f34ef4416e38a33cdad88644_285_0.png)

### 9.4.2 合规解决方案

在此解决方案中，处理器检查构造函数参数而非类数据成员，从而避免了未定义行为。

```cpp
#include <string>

class C {
    std::string str;
public:
    C(const std::string & s) : str(s) (
        // ...
    ) catch (...) {
        if (!s.empty()) {
            // ...
        }
    }
};
```

### 9.4.3 风险评估

在构造函数的异常处理器或析构函数的异常处理器中访问非静态数据会导致未定义行为。

| 规则 | 严重性 | 可能性 | 修复成本 | 优先级 | 级别 |
|---|---|---|---|---|---|
| ERR53-CPP | 低 | 不可能 | 中 | P2 | L3 |

## 9.4.4 相关指南

| MISRA 2008 | 规则 15-3-3 (强制) |
|---|---|

## 9.4.5 参考文献

| ISO/IEC 14882-2014 | 子句 15.3, “处理异常” |
|---|---|

## 9.5 ERR54-CPP. 捕获处理器的参数类型应按从最派生到最少派生的排序

C++ 标准 [except.handle] 第 4 段 [ISO/IEC 14882-2014] 规定如下：

> try 块的处理器按出现顺序进行尝试。这使得编写永远无法执行的处理器成为可能，例如通过放置一个对应基类的处理器。

因此，如果两个处理器捕获自同一基类的异常，则最派生的异常必须排在前。

### 9.5.1 不合规代码示例

在不合规代码示例中，第一个处理器捕获所有 `B` 类异常，以及 `D` 类的异常，因为它们也是 `B` 类。因此，第二个处理器没有捕获任何异常。

```cpp
// 用于异常的类
class B { };
class D : public B {};

void f() {
  try {
    // ...
  } catch (B& b) {
    // ...
  } catch (D& d) {
    // ...
  }
}
```

### 9.5.2 合规解决方案

合规解决方案中，第一个处理器捕获所有 `D` 类异常，第二个处理器捕获所有其他 `B` 类异常。

```cpp
// 用于异常的类
class B {};
class D : public B {};

void f() {
  try {
    // ...
  } catch (D &d) {
    // ...
  } catch (B &b) {
    // ...
  }
}
```

### 9.5.3 风险评估

优先级反倒的异常处理器会在发生派生类型异常时导致意外的控制流。

| 规则 | 可能性 | 修复成本 | 优先级 | 级别 |
| ERR54-CPP | 中 | 可能 | 低 | P18 | L1 |

## 9.5.4 相关指南

- MISRA 2008 规则 15-3-6 (强制)
- 15-3-7 (强制)

## 9.5.5 参考文献

| ISO/IEC 14882-2014 | 子句 15.3, “处理异常” |
|---|---|

# 9.6 ERR55-CPP. 异常规范的合规性

C++ 标准 [except.spec] 第 8 节 [ISO/IEC 14882-2014] 规定如下：

> 如果说一个函数允许类型为 E 的异常，如果其 noexcept 规范中的常量表达式求为假，或者其动态异常规范包含一个类型 T，使得类型为 T 的处理器可以与异常 E 匹配 (15.3)。

如果一个函数抛出的异常超出了其异常规范允许的范围，则可能导致程序由实现定义的终止（[except.spec]，第 9 节）。

如果一个使用动态异常规范声明的函数抛出了与异常规范不匹配的异常类型，则会调用 `std::unexpected()` 函数。该函数的行为可以被重写；默认情况下，它会抛出一个列在异常规范中的 `std::bad_exception` 异常；随后将调用 `std::terminate()` 函数。

同样地，如果一个使用 noexcept 规范声明的函数抛出了一个会导致 noexcept 规范求为假的异常类型，则会调用 `std::terminate()` 函数。

调用 `std::terminate()` 会导致程序实现定义的终止。为了防止程序异常终止，任何声明异常规范的函数都应该尊重自身以及其调用的所有函数，只抛出允许的异常。

### 9.6.1 不合规代码示例

在这个不合规代码示例中，第二个函数声称只抛出 `Exception1`，但它可能会抛出 `Exception2`。

```cpp
#include <exception>

class Exception1 : public std::exception {};
class Exception2 : public std::exception {};

void foo() {
    throw Exception2();
    // 因为 foo() 对异常没有做任何承诺
}

void bar() throw (Exception1) {
    foo();
    // 因为 foo() 可能会抛出 Exception2
}
```

### 9.6.2 合规解决方案

此合规解决方案捕获了 `foo()` 抛出的异常。

```cpp
#include <exception>

class Exception1 : public std::exception {};
class Exception2 : public std::exception {};

void foo() {
    throw Exception2();
    // 因为 foo() 对异常没有做任何承诺
}

void bar() throw (Exception1) {
    try {
        foo();
    } catch (Exception2 e) {
        // 处理错误而不重新抛出它
    }
}
```

# 9.6.3 合规解决方案

此合规解决方案为 `bar()` 声明了动态异常规范，涵盖了所有可能从从中抛出的异常。

```cpp
#include <exception>

class Exception1 : public std::exception {};
class Exception2 : public std::exception {};

void foo() {
    throw Exception2();
    // 因为 foo() 对异常没有做任何承诺
}

void bar() throw (Exception1, Exception2) {
    foo();
}
```

# 9.6.4 不合规代码示例

在这个不合规代码示例中，一个函数被声明为非抛出（nonthrow），但在无法分配请求的内存时，`std::vector::resize()` 可能会抛出异常。

```cpp
#include <cdef>
#include <vector>

void f(std::vector<int> &v, size_t s) noexcept(true) {
    v.resize(s); // 可能会抛出异常
}
```

# 9.6.5 合规解决方案

在此合规解决方案中，删除了函数的 noexcept 规范，意味着该函数允许所有异常。

```cpp
#include <cdef>
#include <vector>

void f(std::vector<int> &v, size_t s) {
    v.resize(s); // 可能会抛出异常，但没关系
}
```

# 9.6.5.1 实现细节

某些供应商提供了语言扩展来指定函数是否抛出异常。例如，Microsoft Visual Studio 提供了 `_declspec((nothrow))`，而 Clang 支持 `__attribute((nothrow))`。目前，供应商尚未记录使用这些扩展指定非抛出函数的行为。对于使用其中一种语言扩展声明的函数，其行为被假设是未定义的。

# 9.6.6 风险评估

抛出意外异常会破坏控制流，并可能导致过早终止和拒绝服务。

| 规则 | 可能性 | 修复成本 | 优先级 | 级别 |
| ERR55-CPP | 可能 | 低 | P9 | L2 |

# 9.6.7 相关指南

| SEI CERT C++ 编码标准 | ERR50-CPP. 不要突然终止程序 |
|---|---|

# 9.6.8 参考文献

| [GNU 2016] | "Declaring Attributes of Functions" |
| [ISO/IEC 14882-2014] | 子节 15.4, "Exception Specifications" |
| [MSDN 2016] | "nothrow (C++)" |

# 9.7 ERR56-CPP. 保证异常安全

妥善处理错误和异常情况对于软件的持续正确运行至关重要。C++ 程序中报告错误的优选机制是异常，而不是错误码。`dynamic_cast`、`operator new` 和 `typeid` 通过抛出异常来报告失败。此外，C++ 标准库利用异常来报告各种失败。很少有 C++ 程序能够避免使用这些设施。此外，C++ 标准库利用异常来报告各种失败。很少有 C++ 程序能够避免使用这些设施。此外，C++ 标准库利用异常来报告各种失败。很少有 C++ 程序能够避免使用这些设施。此外，C++ 标准库利用异常来报告各种失败。（注：原文此处存在重复文本，已按要求完成翻译并保持逻辑）

根据前述影响，下表区分了三种异常安全类型（从强到最弱）：

| 保证 | 说明 | 示例 |
|---|---|---|
| 强保证 | 异常安全是一种操作属性，在满足基本保证的基础上，如果操作因异常终止，对程序状态没有可见影响。 | 异常安全 |
| 基本保证 | 异常安全是一种操作属性，如果操作因异常终止，它能保持程序不变性并防止内存泄漏。 | 基本异常安全 |
| 无 | 既提供强保证也不提供基本保证的代码。 | 无异常安全 |

保证异常安全的代码也保证基本安全。

应用程序中的所有异常必须处理，遵守 ERR50-CPP。关键是异常不能让程序处于违反不变性的确定状态。也就是说，程序必须为所有不变性提供基本保证，并可能为某些不变性提供强保证。

# 9.7.1 不合规代码示例（无异常安全）

以下不合规代码示例展示了一个错误的拷贝赋值运算符。该类的隐含不变性是 `nElems` 存储 `array` 指向数组的元素数量。该函数在为拷贝分配新内存之前，释放了 `array` 并分配了计数器 `nElems`。结果，如果 `new` 表达式抛出异常，函数已经修改了违反类隐含不变性的状态。因此，此类对象处于不确定状态，对其进行任何操作（包括析构）都会导致未定义行为。

```cpp
#include <cstring>

class IntArray {
    int *array;
    std::size_t nElems;
public:
    // ...
    ~IntArray() {
        delete[] array;
    }
    IntArray(const IntArray& that); // 非平凡拷贝构造
    IntArray& operator=(const IntArray& rhs) {
        if (this != &rhs) {
            delete[] array;
            array = nullptr;
            nElems = rhs.nElems;
            if (nElems) {
                array = new int[nElems];
                std::memcpy(array, rhs.array, nElems * sizeof(*array));
            }
        }
        return *this;
    }
    // ...
};
```

## 9.7.2 符合规范的解决方案（强异常安全）

在这个符合规范的解决方案中，拷贝赋值运算符提供了强异常安全保证。函数在更改对象状态之前会先为拷贝分配新的存储空间。只有在分配成功后，函数才会继续更改对象的状态。此外，通过在释放现有数组之前拷贝新分配的数组，函数测试了自赋值情况，这提高了了代码在常见情况下的性能 [Sutter 2004]。

```cpp
#include <cstring>

class IntArray {
    int *array;
    std::size_t nElems;
public:
    // ...
    ~IntArray() {
        delete[] array;
    }
    IntArray(const IntArray& that); // 非平凡的拷贝构造函数
    IntArray& operator=(const IntArray& rhs) {
        int *tmp = nullptr;
        if (rhs.nElems) {
            tmp = new int[rhs.nElems];
            std::memcpy(tmp, rhs.array, rhs.nElems * sizeof(*array));
        }
        delete[] array;
        array = tmp;
        nElems = rhs.nElems;
        return *this;
    }
    // ...
};
```
