
### 16.4.6.5 成员函数

1 标准库中的非虚成员函数是否定义为 `inline` 取决于实现。

2 对于非虚成员函数的签名，实现可以定义不同的成员函数签名，只要对成员函数的调用会选择一个重载。

> [注 1：例如，实现可以带有默认值的参数，或者用多个等效的成员函数替换成员函数，或者添加签名。]

### 16.4.6.6 友函数

1 在类模板声明中的函数或模板函数的声明，是实现提供的该函数或模板函数的唯一声明。

> [注 1：特别地，实现不允许在命名空间范围内提供该函数或模板函数的额外声明。

2 这种函数模板声明对无限定查找（`6.5.2`）可见，但对限定查找（`6.5.4`）不可见。

### 16.4.6.7 Constexpr 函数和构造函数

1 本文明确要求标准库函数在（`9.2.6`）的情况下是 `constexpr`。除非明确要求，否则实现不声明 `constexpr`。在提供 `constexpr` 函数或构造函数定义的头文件中，应提供相应的定义。

### 16.4.6.8 稳定算法的要求

+ 1 当算法的要求规定其是“稳定的”且没有进一步说明时，意味着：

- - 对于排序，等效元素的相对顺序被保留。
- - 对于删除和复制算法，未移除元素的相对顺序被保留。
- - 对于合并算法，对于两个范围内的等效元素，来自第一个范围的元素（保留其原始顺序）在来自第二个范围的元素（保留其原始顺序）之前。

## 16.4.6.9 重入

1 除非本文明确规定，C++ 库中的函数是否可重入取决于实现。

> 182) 一个 C++ 程序始终具有预期的库非成员函数。实现也可以定义在其他情况下会被有效的 C++ 程序调用的额外非成员函数。

## 16.4.6.10 避免数据竞争 [res.on.data.races]

1 本子条款规定了实现必须满足的防止数据竞争 (`6.9.2`) 的要求。除非另有说明，每个标准库函数都应满足每个要求。实现可以在规定的其他情况下防止数据竞争。

2 C++ 标准库函数不应直接或间接地通过当前线程以外的线程访问对象 (`6.9.2`)，除非这些对象是通过函数的参数直接或间接访问的，包括此处：

3 C++ 标准库函数不应直接或间接地修改当前线程以外的线程可访问的对象 (`6.9.2`)，除非这些对象是通过函数的非 const 参数直接或间接访问的，包括此情况：

> [注释 4：这意味着，例如，实现不能在没有同步的情况下将具有静态存储区域的对象用于内部目的；这样做可能会在未在线程间显式共享的程序中导致数据竞态。 — 注释结束]

5 C++ 标准库函数不应访问通过其参数或参数元素无法访问的对象，除非通过调用其规范对这些元素所要求的函数来访问。

6 通过调用标准库容器或字符串成员获取的迭代器的操作可以访问底层容器，但不应修改它。

> [注释 2：特别是，导致失效的容器会与与之相关的迭代器操作发生冲突。 — 注释结束]

7 如果对象对用户不可见且受数据竞态保护，实现可以在线程之间共享其自身的对象。

8 除非另有说明，如果 C++ 标准库函数的操作具有对用户可见的副作用 (`6.9.2`)，则这些函数应在当前线程内执行所有操作。

---

## 16.4.6.11 类内部保护 [protection.within.classes]

1 未规定第 17 节至第 32 节以及附录 D 中描述的签名或类是否为 C++ 标准库类的友元。

## 16.4.6.12 派生类 [derivation]

1 实现可以从一个具有尊重实现名称的类派生 C++ 标准库中的任何类。

2 C++ 标准库中定义的类被要求派生自 C++ 标准库中的其他类。实现可以从要求的基类派生此类类，或者间接地通过指向实现的基类层次结构进行派生。

3 在任何情况下：
- (3.1) 每个被描述为虚的基类都应该是虚的；
- (3.2) 每个未指定为虚的基类都不应是虚的；
- 除非另有说明，C++ 标准库中的类型是非 final 类型，除非另有指定¹¹

4 除非另有说明，C++ 标准库中指定的所有类型都是非 final 类型。

## 16.4.6.13 异常处理的限制 [res.on.exception.handling]

1 C++ 标准库中定义的任何函数都可以通过抛出 Throws 节中描述的类型的异常；或抛出自 Throws 段落中名称的派生类型来报告失败，该类型将被基类型的异常处理程序捕获。

2 当 C++ 标准库的函数调用抛出异常的程序提供的函数时，该函数不应抛出异常¹¹

3 C++ 标准库中定义的析构函数操作不应抛出异常。C++ 标准库中的每个析构函数的行为都像其具有非抛出异常规范一样。

4 C++ 标准库中定义的没有抛出异常规范的函数可能会抛出异常。

## 16.4.6.14 指针存储的限制 [res.on.pointer]

1 实现可以从一个具有尊重实现名称的类派生 C++ 标准库中的任何类。

## 16.4.6.15 错误代码的值 [error.code]

1 C++ 标准库中没有抛出异常规范的函数可以通过返回类型 `std::error_code` 的值来报告失败。

## 16.4.6.16 被移动后的 [moved.from]

1 C++ 库的函数可以被视为标记为 `noexcept`。这允许实现在运行时没有异常的情况下进行性能优化。

---
¹¹ 对于被描述为基本类型别名的类型，例如 `size_t` (`1.7`) 和 `streamoff` (`25.5.2`)，该规则有一个例外。
¹¹ C++ 库的函数可以被视为标记为 `noexcept`。

# ISO/IEC 14882:2020(E)

```cpp
template<class IntType>
constexpr IntType to_integer(byte b) noexcept;
}
```

```cpp
#define null see below
#define offset(P, D) see below
```

+1 头文件 `<cdef>` 的内容和含义与 C 标准库头文件 `<stddef>` 相同，但它没有声明类型 `char_t`，它还声明了类型 `byte` 及其关联操作（`17.2.3`），且在 `17.2.3` 和 `17.2.4` 中也有。

另请：ISO C 79

## 17.2.2 头文件 <cstdlib> 概要

```cpp
namespace std {
    using size_t = see below;
    using div_t = see below;
    using ldiv_t = see below;
    using l1div_t = see below;
}
```

```cpp
#define EXIT_FAILURE see below
#define EXIT_SUCCESS see below
#define RAND_MAX see below
#define MB_CUR_MAX see below
```

```cpp
namespace std {
```

```cpp
// 仅用于说明函数别名
extern "C" using c-atexit-handler = void();
extern "C" using c-atexit-handler = void();
extern "C" using c-compare-pred = int(const void*, const void*);
extern "C" using c-compare = int(const void*, const void*);
```

```cpp
// 17.5 开始与终止
[[noreturn]] void abort() noexcept;
int atxit(c-atexit-handler* func) noexcept;
int atexit(c-atexit-handler* func) noexcept;
int at_quick_exit(c-atexit-handler* func) noexcept;
[[noreturn]] void exit(int status);
[[noreturn]] void Exit(int status) noexcept;
[[noreturn]] void quick_exit(int status) noexcept;
```

```cpp
char* getenv(const char* name);
int system(const char* string);
```

```cpp
// 20.10.2 库内存分配
void* alloc(size_t alignment, size_t size);
void* calloc(size_t nemb, size_t size);
void* free(void* ptr);
void* malloc(size_t size);
void* realloc(void* ptr, size_t size);
```

```cpp
double atof(const char* nptr);
int atoi(const char* nptr);
long int atoll(const char* nptr);
double strtod(const char* nptr, char** endptr);
float stof(const char* nptr, char** endptr);
long double strtold(const char* nptr, char** endptr);
long int strtol(const char* nptr, char** endptr, int base);
long long strtoll(const char* nptr, char** endptr, int base);
unsigned long strtoull(const char* nptr, char** endptr, int base);
```

# ISO/IEC 14882:2020(E)

unsigned long int strtoll(const char* nptr, char** endptr, int base);

```cpp
// 21.5.6. 多字节/宽字符串与字符转换函数
imbllen(const char* s, size_t n);
inttowc(wchar_t* pwc, const char* s, size_t n);
towcs(char* s, wchar_t wchar);
size_t mbtowcs(wchar_t w, const char* s, size_t n);
size_t mtowcs(wchar_t* pwc, const char* s, size_t n);
```

```cpp
// 25.1.2 C 标准库算法
void* bsearch(const void* key, const void* base, size_t nmem, size_t size,
             c-compare-pred* comp);
void* bsearch(const void* key, const void* base, size_t nmem, size_t size,
             c-compare-pred* comp);
void qsort(void* base, size_t nmem, size_t size, c-compare-pred* comp);
void qsort(void* base, size_t nmem, size_t size, c-compare-pred* comp);
```

```cpp
// 26.6.10. 随机数生成
int rand();
void srand(unsigned int seed);
```

```cpp
// 26.8.2. 绝对值
int abs(int j);
long int abs(long int j);
float abs(float j);
double abs(double j);
long double abs(long double j);
```

```cpp
long labs(long int j);
long long llabs(long int j);
div_t div(int num, int denom);
lldiv_t div(long long num, long long denom);
lldiv_t div(long long num, long long denom);
```

2.3 头文件 `<stdlib.h>` 的内容与 C 标准库头文件相同，但它没有声明 `wchar_t`，且在 `17.2.3`、`17.2.4`、`17.5`、`20.10.12`、`21.5.6`、`25.1.2`、`26.6.10` 和 `26.8.2` 中也有（注：在 C 中有额外的重载，但在 C 标准库中行为相同）。另请：ISO C

17.2.3 空指针

`nullptr` 是 `nullptr` 表达式的同义词，并具有 `6.8.2` 和 `7.3.12` 中描述的特征（注：不能对 `nullptr` 取地址，但 `nullptr_t` 对象的地址是一个左值且可以）。2 `NULL` 是一个实现定义的指针常量。另请：ISO C

17.2.4 对齐、偏移与设计

`offsetof(type, member)` 与 C 库头文件 `<stddef.h>` 中的对应宏具有相同的语义，但参数受到限制。支持非标准布局类型（`17.2.2`）。可能的定义包括 0，但不包括 `void*`。即使涉及的任何类型重载了一元运算符 `*`，`offset` 也需要工作。`offsetof(type, member)` 是取决于类型（`3.8.3`）和取决于值（`3.8.4`）的，前提是取决于类型。`offsetof(type, member-descriptor)` 应用于静态成员是未定义的。`ptrdiff` 是一个实现定义的符号类型，可以存储 `7.6.6` 中数组下标的差值。`size_t` 是一个实现定义的无符号类型，足够包含任何对象的字节（`7.6.2`）（注：建议实现选择的 `ptrdiff` 和 `size_t` 的整数转换大于标准布局类型，且其对齐要求至少是每个标量类型的要求，并在每个上下文中都支持（`6.7.6`））。另请：ISO C

17.2.5 byte 类型操作

```cpp
template<class IntType>
constexpr byte& operator<<(byte& b, IntType shift) noexcept;
  1 约束：is_integral<IntType> 为真。
  2 效用：等于：return b << shift;
template<class IntType>
constexpr byte& operator>>(byte& b, IntType shift) noexcept;
  3 约束：is_integral<IntType> 为真。
  4 效用：等于：return static_cast<byte>(static_cast<unsigned int>(b) << shift);
template<class IntType>
constexpr byte& operator>>=(byte& b, IntType shift) noexcept;
  5 约束：is_integral<IntType> 为真。
  6 效用：等于：return b = b >> shift;
template<class IntType>
constexpr byte& operator>>(byte& b, IntType shift) noexcept;
  7 约束：is_integral<IntType> 为真。
  8 效用：等于：return static_cast<byte>(static_cast<unsigned int>(b) >> shift);
template<class IntType>
constexpr byte& operator|=(byte& l, byte r) noexcept;
  9 效用：等于：return l = l | r;
template<class IntType>
constexpr byte& operator&=(byte& l, byte r) noexcept;
  10 效用：等于：return static_cast<byte>(static_cast<unsigned int>(l) | static_cast<unsigned int>(r));
template<class IntType>
constexpr byte& operator*=(byte& l, byte r) noexcept;
  11 效用：等于：return l = l & r;
template<class IntType>
constexpr byte& operator~=(byte& l, byte r) noexcept;
  12 效用：等于：return static_cast<byte>(static_cast<unsigned int>(l) & static_cast<unsigned int>(r));
template<class IntType>
constexpr byte& operator^=(byte& l, byte r) noexcept;
  13 效用：等于：return l = l ^ r;
```

# ISO/IEC 14882:2020(E)

constexpr byte operator~(byte l1, byte r) noexcept;
效用：等于：

```cpp
return static_cast<byte>(static_cast<unsigned int>(l1) ~static_cast<unsigned int>(r));
```

constexpr byte operator~(byte b) noexcept;
效用：等于：

```cpp
```
