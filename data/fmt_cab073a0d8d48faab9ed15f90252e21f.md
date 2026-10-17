
### 6.4.2 合规解决方案 (try/catch)

这一合规解决方案使用了 `std::basic_string::at()` 函数，它的行为与索引运算符 `[]` 相似，但在 `pos = size()` 时会抛出 `std::out_of_range` 异常。

```cpp
#include <stdexcept>
#include <string>
extern std::size_t get_index();
void f() {
    std::string s("012345678");
    try {
        s.at(get_index()) = '1';
    } catch (std::out_of_range &e) {
        // 处理错误
    }
}
```

### 6.4.3 合规解决方案 (范围检查)

这一合规解决方案在调用 `operator[]` 之前检查 `get_index()` 返回的值是否在有效范围内。

```cpp
#include <string>
extern std::size_t get_index();
void f() {
    std::string s("012345678");
    std::size_t i = get_index();
    if (i < s.length()) {
        s[i] = '1';
    } else {
        // 处理错误
    }
}
```

### 6.4.4 不合规代码示例

在这一不合规代码示例中尝试将字符串中的首字符替换为等效的大写字母。然而，如果字符串为空，则行为是未定义的。

```cpp
#include <string>
#include <locale>
void capitalize(std::string &s) {
    std::locale loc;
    s.front() = std::use_facet<std::ctype<char>>(loc).toupper(s.front());
}
```

### 6.4.5 合规解决方案

在这一合规解决方案中，指向 `exampleString` 内部缓冲器的指针直到 `replace()` 的修改完成后才会被生成。

```cpp
#include <string>
#include <locale>
void capitalize(std::string &s) {
    if (s.empty()) return;
    std::locale loc;
    s.front() = std::use_facet<std::ctype<char>>(loc).toupper(s.front());
}
```

### 6.4.6 风险评估

使用无效的字符串对象引用、指针或迭代器可能允许攻击者运行任意代码。

| 规则 | 严重性 | 可能性 | 修复成本 | 优先级 | 级别 |
|---|---|---|---|---|---|
| STR52-CPP | 高 | 可能 | 高 | P6 | L2 |

### 6.4.7 相关准则

| --- | --- |
| SEI CERT C++ 编码标准 | CTR51-CPP。使用有效的引用、指针和迭代器来引用容器的元素 |

### 6.4.8 参考文献

| --- | --- |
| [ISO/IEC 14882-2014] | 子章节 21.4.1，“basic_string 通用要求” |
| [Meyers 2001] | 项目 43，“优先使用算法调用而非手写循环” |

SEI CERT C++ 编码标准 (2016 年版) | V01
软件工程学院 | 卡内基梅隆大学
[分发声明 A] 批准公开发布和无限分发。

内存管理 (MEM)

### 7.1 不合规代码示例 (new and delete)

在这一不合规代码示例中，`s` 在被析构函数释放后仍被引用。这会导致悬指针。

```cpp
#include <new>
struct S {
    void f();
};
void g() noexcept(false) {
    S *s = new S;
    delete s;
    // ...
    s->f();
}
```

### 7.1.2 合规解决方案 (new and delete)

在这一合规解决方案中，动态分配的内存直到不再需要时才释放。

```cpp
#include <new>
struct S {
  void f();
};
void g() noexcept(false) {
  S *s = new S;
  // ...
  s->f();
  delete s;
}
```

### 7.1.3 合规解决方案 (自动存储期)

尽可能使用自动存储期而非动态存储期。由于 `s` 需要生存于 `g()` 的作用域，这一合规解决方案使用自动存储期将 `s` 的生命限制在 `g()` 的作用域内。

```cpp
struct S {
  void f();
};
void g() {
  S s;
  // ...
  s.f();
}
```

### 7.1.4 不合规代码示例 (std::unique_ptr)

在以下不合规代码示例中，由缓冲区对象管理的动态分配内存在析构函数释放后被访问了。

```cpp
#include <iostream>
#include <memory>
#include <cstring>
int main(int argc, const char *argv[]) {
    const char *s = "";
    if (argc > 1) {
        enum BufferSize = 32;
        try {
            std::unique_ptr<char[]> buff(new char[BufferSize]);
            std::memset(buff.get(), 0, BufferSize);
            // ...
            s = std::strncpy(buff.get(), argv[1], BufferSize - 1);
        } catch (std::bad_alloc&) {
            // 处理错误
        }
    }
    std::cout << s << std::endl;
}
```

这段代码始终创建一个空终止的字节字符串，尽管它使用了 `strncpy()`，因为它遗留了缓冲区中的最后一个字符设置为 0。

### 7.1.5 合规解决方案 (std::unique_ptr)

在此合规解决方案中，`buff` 对象的生命周期延伸到了访问该对象管理的内存点之后。

```cpp
#include <iostream>
#include <memory>
#include <cstring>
int main(int argc, const char *argv[]) {
    std::unique_ptr<char[]> buff;
    const char *s = "";
    if (argc > 1) {
        enum BufferSize = 32 };
        try {
            buff.reset(new char[BufferSize]);
            std::memset(buff.get(), 0, BufferSize);
            // ...
            s = std::strncpy(buff.get(), argv[1], BufferSize - 1);
        } catch (std::bad_alloc&) {
            // 处理错误
        }
    }
    std::cout << s << std::endl;
}
```

### 7.1.6 合规解决方案 std::string

在此合规解决方案中，使用了具有自动存储周期的 `std::string` 类型的变量来替代 `std::unique_ptr<char[]>`，这降低了解决方案的复杂性并提高了其安全性。

```cpp
#include <iostream>
#include <string>
int main(int argc, const char *argv[]) {
    std::string str;
    if (argc > 1) {
        str = argv[1];
    }
    std::cout << str << std::endl;
}
```

### 7.1.7 不合规代码示例 (std::string::c_str())

在此不合规示例中，对临时 `std::string` 对象调用了 `std::string::c_str()`。一旦 `std::string` 对象在赋值表达式结束时被销毁，生成的指针将指向已释放的内存，导致在访问该指针的元素时产生未定义行为。

```cpp
#include <string>
std::string str_func();
void display_string(const char *);
void f() {
    const char *str = str_func().c_str();
    display_string(str); /* 未定义行为 */
}
```

### 7.1.8 合规解决方案 (std::string::c_str())

在此合规解决方案中，对 `str_func()` 返回的字符串进行了局部拷贝，以确保在调用 `display_string()` 时 `str` 是有效的。

```cpp
#include <string>
std::string str_func();
void display_string(const char *s);
void f() {
    std::string str = str_func();
    const char *cstr = str.c_str();
    display_string(cstr); /* OK */
}
```

### 7.1.9 不合规代码示例

在此不合规代码示例中，尝试通过调用 `operator new()` 分配零字节内存。如果请求成功，`operator new()` 要求返回一个非空指针。然而，根据 C++ 标准 [basic.stc.dynamic.allocation] 第 2 段 [ISO/IEC 14882-2014]，尝试通过此类指针解引用内存会导致未定义行为。

```cpp
#include <new>
void f() noexcept(false) {
    unsigned char *ptr = static_cast<unsigned char *>::operator new(0);
    *ptr = 0;
    // ...
    ::operator delete(ptr);
}
```

### 7.1.10 合规解决方案

合规解决方案取决于程序员的意图。如果程序员意图分配单个 `unsigned char` 对象，则合规解决方案是使用 `new` 而不是直接调用 `operator new()`，正如此合规解决方案所示。

```cpp
void f() noexcept(false) {
    unsigned char *ptr = new unsigned char;
    *ptr = 0;
    // ...
    delete ptr;
}
```

### 7.2 合规解决方案

如果程序员意图通过调用 `operator new()` 分配零字节内存（以获取一个非空指针值），合规解决方案是将其声明为 `void *`，直到它被释放。

```cpp
#include <new>
void f() noexcept(false) {
    void *ptr = ::operator new(0);
    // ...
    ::operator delete(ptr);
}
```

### 7.12 风险评估

访问已释放的内存会导致未定义行为。写入已释放的内存会导致程序异常终止。

| 规则 | 严重性 | 可能性 | 优先级 | 级别 |
|---|---|---|---|---|
| MEM50-CPP | 高 | 中 | P18 | L1 |

### 7.12 相关漏洞

VU62332 描述了双重释放（double free）。

### 7.13 相关指南

| SEI CERT++ 标准 | 说明 |
|---|---|
| MEM54-CPP. 不要访问已释放的对象 | |
| MEM52-CPP. 检测并处理内存分配错误 | |
| MEM30-C. 不要释放内存 | |
| CWE-415 双重释放 | |
| CWE-416 释放后使用 |

### 7.14 参考文献

| 引用 | 详情 |
|---|---|
| [ISO/IEC 14882-2014] | 子句 3.7.1, “分配函数” 子句 3.7.2, “释放函数” |
| | 第 4 章，“动态内存管理” |

### 7.2 正确释放动态分配资源

C 语言提供了几种分配内存的方法，例如 `malloc()`、`calloc()`，这些方法可以被 C++ 程序使用。然而，C 语言只定义了一种释放分配内存的方法：`free()`。

C++ 语言增加了额外的分配内存方法，例如运算符 `new`、`new[]` 和 `placement new` 以及分配器对象。与 C 不同，C++ 提供了多种释放分配内存的方法，例如运算符 `delete` 和 `delete[]`。

释放未分配的指针（包括 `placement new()` 返回的指针）会导致未定义行为，因为该指针不是通过分配函数获得的。释放已经传递给释放函数的指针会导致未定义行为，因为该指针不再指向动态分配的内存。

| 分配器 | 释放器 |
|---|---|
| global `new()` | global `delete()` |
| global `new[]` | global `delete[]` |
| class-specific `new()` | class-specific `delete()` |
| class-specific `new[]` | class-specific `delete[]` |
| `placement new` | N/A |
| `allocator<T>::allocate()` | `allocator<T>::deallocate()` |
| `std::malloc()`, `std::calloc()` | `std::free()` |
| `std::realloc()` | N/A |
| `std::get_temporary_buffer()` | `std::return_temporary_buffer()` |

### 7.2.1 不合规代码示例 (placement new())

在此不合规代码中，局部变量 `s1` 被作为表达式传递给 `placement new` 运算符。该调用生成的指针被传递给 `::operator delete()`，由于 `::operator delete()` 尝试释放并非由 `::operator new()` 返回的内存，会导致未定义行为。

```cpp
#include <iostream>
struct S {
    S() { std::cout << "S::S" << std::endl; }
    -S(S) { std::cout << "S:-S" << std::endl; }
};
void f1() {
    S s1;
    S *s2 = new (&s1) S;
    // ...
    delete s2;
}
```

### 7.2.2 合规解决方案 (placement new())

此合规解决方案移除了对 `::operator delete()` 的调用，使其能够在正常对象生命周期结束时被销毁。

```cpp
#include <iostream>
struct S {
    S() { std::cout << "S::S()" << std::endl; }
    ~S() { std::cout << "S::~S()" << std::endl; }
};
void f() {
    S s1;
    S *s2 = new (&s1) S;
    // ...
}
```

### 7.2.3 不合规代码示例 (未初始化的 delete)

在这个不合规代码示例中，在同一个块内尝试了两次分配，如果其中任何一次失败，catch 处理器程序将尝试释放已分配的资源。然而，由于指针变量没有初始化为已知值，内存分配失败会导致向 `::operator delete()` 传递一个之前未通过 `::operator new()` 调用返回的值（在 `i2` 中），从而导致未定义行为。

```cpp
#include <new>
void f() {
    int *i1, *i2;
    try {
        i1 = new int;
        i2 = new int;
    } catch (std::bad_alloc &) {
        delete i1;
        delete i2;
    }
}
```

### 7.2.4 合规解决方案 (未初始化的 delete)

此合规解决方案将两个指针值初始化为 `nullptr`，这是传递给 `::operator delete()` 的有效值。

```cpp
```
