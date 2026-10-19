

## ISO/IEC 14882:2020(E)

```c
void* memcpy(void* s1, const void* s2, size_t n);
void* memmove(void* s1, const void* s2, size_t n);
char* strcpy(char* s1, const char* s2);
char* strncpy(char* s1, const char* s2, size_t n);
char* strcat(char* s1, const char* s2);
char* strncat(char* s1, const char* s2, size_t n);
int memcmp(const void* s1, const void* s2, size_t n);
int strcmp(const char* s1, const char* s2);
int strcoll(const char* s1, const char* s2);
int strncmp(const char* s1, const char* s2, size_t n);
size_t strxfrm(char* s1, const char* s2, size_t n);
const void* memchr(const void* s, int c, size_t n);    // see 16.2
void* memchr(void* s, int c, size_t n);                // see 16.2
const char* strchr(const char* s, int c);              // see 16.2
char* strchr(char* s, int c);                          // see 16.2
size_t strcspn(const char* s1, const char* s2);
const char* strpbrk(const char* s1, const char* s2);   // see 16.2
char* strpbrk(char* s1, const char* s2);               // see 16.2
const char* strrchr(const char* s, int c);             // see 16.2
char* strrchr(char* s, int c);                         // see 16.2
size_t strspn(const char* s1, const char* s2);
const char* strstr(const char* s1, const char* s2);    // see 16.2
char* strstr(char* s1, const char* s2);                // see 16.2
char* strtok(char* s1, const char* s2);
void* memset(void* s, int c, size_t n);
char* strerror(int errnum);
size_t strlen(const char* s);
}
```

```c
#define NULL see 17.2.3
```

1 <cstring> 头文件的内容和含义与 C 标准库头文件 <string.h> 相同。

2 函数 strerror 和 strtok 不要求避免数据竞争（16.4.6.10）。

3 函数 memcpy 和 memmove 是信号安全的（17.13.5）。这两个函数会在将字符序列复制到目标位置之前，立即在目标存储区域中隐式创建对象（6.7.2）。

4 [注 1：函数 strchr、strpbrk、strrchr、strstr 和 memchr 在本文件中的签名不同，但它们与 C 标准库中的行为相同（16.2）。—— 结束注]

另见：ISO C 7.24

### 21.5.4 头文件 <cwchar> 摘要

```c
namespace std {
    using size_t = see 17.2.4;
    using mbstate_t = see below;
    using wint_t = see below;

    struct tm;

    int fwprintf(FILE* stream, const wchar_t* format, ...);
    int fwscanf(FILE* stream, const wchar_t* format, ...);
    int swprintf(wchar_t* s, size_t n, const wchar_t* format, ...);
    int swscanf(const wchar_t* s, const wchar_t* format, ...);
    int vfwprintf(FILE* stream, const wchar_t* format, va_list arg);
    int vfwscanf(FILE* stream, const wchar_t* format, va_list arg);
    int vswprintf(wchar_t* s, size_t n, const wchar_t* format, va_list arg);
    int vswscanf(const wchar_t* s, const wchar_t* format, va_list arg);
    int vprintf(const wchar_t* format, va_list arg);
    int vwscanf(const wchar_t* format, va_list arg);
    int wprintf(const wchar_t* format, ...);
    int wscanf(const wchar_t* format, ...);
    wint_t fgetwc(FILE* stream);
    wchar_t* fgetws(wchar_t* s, int n, FILE* stream);
    wint_t fputwc(wchar_t c, FILE* stream);
}
```

- 0，如果接下来的 n 个或更少的字节完整构成了与 U+0000 Unicode 字符（即所存储的值）对应的多字节字符。
- 介于 1 和 n（含）之间，如果接下来的 n 个或更少的字节完整构成一个有效的多字节字符（即所存储的值）；返回的值为完整构成该多字节字符的字节数。
- (size_t)(-3)，如果先前调用产生的下一个字符已被存储（此调用未消耗输入中的任何字节）。
- (size_t)(-2)，如果接下来的 n 个字节构成一个不完整（但可能有效）的多字节字符，且所有 n 个字节均已被处理（未存储任何值）。
- (size_t)(-1)，如果发生编码错误，在这种情况下，接下来的 n 个或更少的字节不能构成完整且有效的多字节字符（未存储任何值）；宏 EILSEQ 的值被存储在 errno 中，且转换状态未指定。

size_t c8rtomb(char* s, char8_t c8, mbstate_t* ps);

效果：如果 s 是空指针，则等价于 c8rtomb(buf, u8'\0', ps)，其中 buf 是一个内部缓冲区。否则，如果 c8 完成了有效 UTF-8 代码单元的序列，则确定表示该多字节字符（包括任何移位序列）所需的字节数，并将该多字节字符表示存储在第一个元素由 s 指向的数组中。最多存储 MB_CUR_MAX 个字节。如果该多字节字符是空字符，则存储一个空字节，并在该空字节之前存储恢复初始移位状态所需的任何移位序列；所述结果状态为初始转换状态。

返回：存储在数组对象中的字节数（包括任何移位序列）。如果 c8 不能构成与有效多字节字符对应的 char8_t 序列，则宏 EILSEQ 的值被存储在 errno 中，返回 (size_t)(-1)，且转换状态未指定。

备注：以空指针作为 s 参数调用 c8rtomb 可能会与同样以空指针作为 s 参数调用 c8rtomb 的其他调用之间引入数据竞争（16.4.6.10）。

## 22 容器库

[containers]

### 22.1 概述

[containers.general]

1 本章描述了 C++ 程序可用于组织信息集合的组件。

2 以下子条款描述了容器要求，以及顺序容器和关联容器的组件，如表 72 所示。

表 72：容器库摘要 [tab:containers.summary]

| 子条款 | 头文件 |
|---|---|
| 22.2 要求 | |
| 22.3 顺序容器 | <array>, <deque>, <forward_list>, <list>, <vector> |
| 22.4 关联容器 | <map>, <set> |
| 22.5 无序关联容器 | <unordered_map>, <unordered_set> |
| 22.6 容器适配器 | <queue>, <stack> |
| 22.7 视图 | <span> |

### 22.2 容器要求

[container.requirements]

### 22.2.1 通用容器要求

[container.requirements.general]

1 容器是存储其他对象的对象。它们通过构造函数、析构函数、插入和擦除操作来控制这些对象的分配和释放。

2 本章中的所有复杂度要求仅以对所含对象执行的操作数量来陈述。

> [示例 1：类型 vector<vector<int>> 的复制构造函数具有线性复杂度，尽管复制每个所含 vector<int> 的复杂度本身也是线性的。—— 结束示例]

3 对于受本子条款影响且声明了 allocator_type 的组件，这些组件中存储的对象应使用函数 allocator_traits<allocator_type>::rebind_traits<U>::construct 构造，并使用函数 allocator_traits<allocator_type>::rebind_traits<U>::destroy 销毁（20.10.9.3），其中 U 是 allocator_type::value_type 或容器使用的内部类型。这些函数仅针对容器的元素类型调用，而不针对容器使用的内部类型调用。

> [注 1：这意味着，例如，基于节点的容器需要构造包含对齐缓冲区的节点，并调用 construct 将元素放入缓冲区。—— 结束注]

4 在表 73、表 74 和表 75 中，X 表示包含 T 类型对象的容器类，a 和 b 表示 X 类型的值，i 和 j 表示类型为（可能为 const）X::iterator 的值，u 表示标识符，r 表示 X 类型的非 const 值，rv 表示 X 类型的非 const 右值。

表 73：容器要求 [tab:container.req]

| 表达式 | 返回类型 | 操作语义 | 断言/注释 前置/后置条件 | 复杂度 |
|---|---|---|---|---|
| X::value_type | T |  | 前置条件：T 是 Cpp17Erasable，可以从 X 中擦除（参见下文 22.2.1） | 编译期 |
| X::reference | T& |  |  | 编译期 |
| X::const_reference | const T& |  |  | 编译期 |

