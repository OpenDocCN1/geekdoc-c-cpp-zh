

系统，或者指向一个源自其他处的实现定义的 `error_category` 对象的引用。
实现应当为这些错误类别中的每一个类别定义 `value()` 的可能值。[示例：
对于基于 POSIX 的操作系统，实现应当定义的 `std::system_category()` 的值应与 POSIX `errno` 值相同，并包含由操作系统文档定义的额外值。对于不基于 POSIX 的操作系统，实现定义的数值应与操作系统的值相同。对于并非源自操作系统的错误，实现可以为关联值提供枚举（enums）。—— 示例结束]

## 20.5.5.15 库类型的被移出状态 [lib.types.movedfrom]

- 1 在 C++ 标准库中定义的类型1对象可以被移出 (15.8)。移动操作可以显式指定，也可以隐式生成。除非另有规定，否则此类被移出的对象应处于一个有效但未指定的状态。

## 21 语言支持库 [language.support]

### 21.1 通用 [support.general]

- 1 此类描述了在 C++ 程序执行期间隐式调用的函数签名，以及隐式生成的对象类型。它还描述了声明这些函数签名并定义任何相关类型的头文件。

- 2 下述类描述了整个库中使用的常用类型定义、预定义类型的特征、C++ 程序的启动和终止、动态内存管理的支持、异常处理的支持、初始化列表的支持以及其他运行时支持，如表 32 所示。

表 32 — 语言支持库摘要
| 子类 | 头文件(s) |
| :--- | :--- |
| 21.2 | 通用定义 | <cstddef>, <cstdlib> |
| 21.3 | 实现属性 | <limits>, <cfloat> |
| 21.4 | 整数类型 | <cctype> |
| 21.5 | 启动与终止 | <cstdlib> |
| 21.6 | 动态内存管理 | <new> |
| 21.7 | 类型识别 | <typeinfo> |
| 21.8 | 异常处理 | <exception> |
| 21.9 | 初始化列表 | <initializer_list> |
| 21.10 | 其他运行时支持 | <csignal>, <ctimearg>, <cstdlib> |

## 21.2 通用定义 [support.types]

### 21.2.1 头文件 <cstddef> 概要 [cstddef.syn]

```cpp
namespace std {
    using ptrdiff_t = see below;
    using size_t = see below;
    using max_align_t = see below;
    using nullptr_t = decltype(nullptr);

    enum class byte : unsigned char {};
    // 21.2.5. byte 类型操作
    template <class IntType>
    constexpr byte& operator<<=(byte b, IntType type) noexcept;
```

```cpp
template <class IntType>
constexpr byte operator<<(byte b, IntType shift) noexcept;
template <class IntType>
constexpr byte operator>>=(byte&, IntType shift) noexcept;
template <class IntType>
constexpr byte operator|=(byte b, IntType shift) noexcept;
constexpr byte operator|=(byte b1, byte b1, r) noexcept;
constexpr byte operator*=(byte b1, byte b1, r) noexcept;
constexpr byte operator/=(byte b1, byte b1, r) noexcept;
constexpr byte operator-=(byte b1, byte b1, r) noexcept;
constexpr byte operator=(byte b1, byte b1, r) noexcept;
constexpr byte operator=(byte b) noexcept;
template <class IntType>
constexpr IntType_to_integer(byte b) noexcept;
}
```

```cpp
#define NULL see below
#define offset(P, D) see below
```

1 头文件 <stddef> 的内容和含义与 C 标准库头文件 <stddef.h> 相同，但它没有声明 `char_` 类型，而是声明了 `byte` 类型及其关联操作 (21.2.5)，并在 21.2.3 和 21.2.4 中也有备注。

另另：ISO C 7.19

## 21.2.2 头文件 <stdlib.h> 概要 [stdlib.bin]

```cpp
namespace std {
    using size_t = see below;
    using div_t = see below;
    using ldiv_t = see below;
    using uint_t = see below;
}
```

```cpp
#define NULL see below
#define EXIT_FAILURE see below
#define EXIT_SUCCESS see below
#define RAND_MAX see below
#define MB_CUR_MAX see below
```

namespace std

```cpp
// 仅供说明的类型别名
    extern "C" c_exit_handler = void(void); // 仅供说明
    extern "C" atexit_handler = void(void); // 仅供说明
    extern "C" c_compare_int = int(const void*, const void*); // 仅供说明
    extern "C" c_compare_ptr = int(const void*, const void*); // 仅供说明
```

21.2.5, 启动与终止

```cpp
[[noreturn]] void abort(int status);
    int atexit(c_exit_handler* func) noexcept;
    int atexit(c_atexit_handler* func) noexcept;
    int_quick_exit(c_atexit_handler* func) noexcept;
    [[noreturn]] void exit(int status);
    [[noreturn]] Exit_int(int status) noexcept;
    [[noreturn]] quick_exit(int status) noexcept;
```

char* getenv(const char* name);
int system(const char* string);

### 23 语言支持

### 21.10 内存分配
void* malloc(size_t size);
void* calloc(size_t nm, size_t size);
void* realloc(void* ptr, size_t size);
void free(void* ptr);

### 21.11 字符串转换
double atof(const char* string);
long atol(const char* string);
long long stroll(const char* string);
double strtod(const char* string);
float strtof(const char* string);
long strtol(const char* string);
long long strtoll(const char* string);

### 24.5 多字节字符串
size_t mbsen(const char* s);
int mbst(const char* s);
size_t mbstlen(const char* s);
size_t mbstcs(char* s, const char* src, size_t n);
size_t mbstowcs(char* s, const char* src, size_t n);
size_t mtowcs(char* s, const char* src, size_t n);
size_t mbstowcs(char* s, const char* src, size_t n);

### 25.8 算法
void* bsearch(const void* key, const void* base, size_t nm, size_t size, int (*compar)(const void*, const void*));
void qsort(void* base, size_t nm, size_t size, int (*compar)(const void*, const void*));

### 29.9 随机数生成
int rand();
void srand(unsigned int seed);

