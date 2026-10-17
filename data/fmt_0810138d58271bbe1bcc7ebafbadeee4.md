
```cpp
using int8_t = 符号整数类型;
using int16_t = 符号整数类型;
using int32_t = 符号整数类型;
using int64_t = 符号整数类型;
using uint8_t = 无符号整数类型;
using uint16_t = 无符号整数类型;
using uint32_t = 无符号整数类型;
using uint64_t = 无符号整数类型;
```

1 该头文件定义了大量的宏：

- `INT_FAST_LEAST(8 32 64)_MIN`
- `INT_FAST_LEAST(8 32 64)_MAX`
- `INTMAX_PTR_MIN`
- `INTMAX_PTR_MAX`
- `PTRDIFF_SIZE_MAX`
- `SIZE_MAX`

以及以下形式的：

- `INT(8 32 64)_MIN`
- `INT(8 32 64)_MAX`
- `UINTMAX_C`
- `UINTMAX_C`

2 该头文件将所有类型和宏定义为与 C 标准库头文件 `<stdlib.h>` 相同。

另参见：ISO C 7:20

## 21.5 开始与终止

> [注：头文件 `<stdlib.h>` (21.2.2) 了本子类中的函数。--- 注释结束]

```cpp
[[return]] void exit(int status) noexcept;
```

2 效果：该函数具有标准库语义。

3 备注：程序终止时不会析构自动、线程或静态存储周期的对象，也不会调用传递给 `exit(it)` 的句 (6.6.4)。`_Exit` 是信号安全的21.10.4。

```cpp
[[return]] void abort() noexcept;
```

4 效果：该函数具有标准库语义。

5 备注：程序终止时不会析构自动、线程或静态存储周期的对象，也不会调用传递给 `exit(it)` 的句 (6.6.4)。`abort` 是信号安全的21.10.4。

```cpp
int atexit(void (*handler)(void)) noexcept;
int atexit_s(void (*handler)(void)) noexcept;
```

6 效果：该函数注册由 `f` 指向的函数以便在正常程序持续期间无参数调用。在调用 `exit(it)` 之前 (4.7) 调用 `axit()` 是否成功是不确定的。[注：`atexit()` 函数不会引入数据竞态 (20.5.5)。--- 注释结束]

7 实现限制：实现应能够处理至少 32 个函数的注册。

8 返回：`exit()` 函数在注册时返回零，失败返回非零。

```cpp
[[return]] void exit(int status);
```

9 效果：

— 首先，析构具有线程持续且与当前线程相关的对象。

接下来，析构静态存储周期的对象并调用通过调用 `exit` 注册的函数¹215 参见 6.6.4 关于析构和调用顺序。（调用 `exit(it)` 不导致自动对象的析构。²216

215 一个函数每次被注册时都会调用一次。在主函数 (6.6.1) 不包含自动对象的程序中，所有函数都会被析构。

216 自动存储周期的对象被析构

# ISO/IEC 14882:2017(E)

如果一个注册的函数通过退出而离开，原因是因为该函数没有为抛出的异常提供处理程序，则应调用 `std::terminate()` (18.5.1)。

(9.2) 接下来，所有带有未写入缓冲区数据的打开的 C 流（通过 `<cstdio>` 中声明的函数签名进行调停）将被刷新，所有打开的 C 流将被关闭，并删除通过调用 `tmpfile()` 创建的所有文件。

(9.3) 最后，控制权返回给主环境。如果状态为 0 或 `EXIT_SUCCESS`，则返回一个实现定义的成功终止状态。如果状态为 `EXIT_FAILURE`，则返回一个实现定义的非成功终止状态。否则，返回一个实现定义的状态。¹

```
int quick_exit(std::exit_handler* f) noexcept;
int quick_exit(std::exit_handler* f) noexcept;
```

10 效果：`at_exit()` 函数注册由 `f` 指向的函数，以便在调用 `quick_exit` 时被调用。规定在 (4.7) 所有的对 `quick_exit` 的调用之前的 `at_exit()` 调用将成功。 [注：`at_exit()` 函数不会引入竞态 (20.5.9) — 结束][注：如果多次调用 `at_exit()`，可能无法实现任何注册顺序][注：注册项将从退出注册中删除，应用程序可能需要使用相同的参数调用所有注册函数。 — 结束]

11 实现：实现应当支持至少 32 个函数的注册。

12 返回：用 `quick_exit(int status)` 注册的状态，如果为非零，则返回该值。

```cpp
[[noreexcept]] void quick_exit(int status) noexcept;
```

13 效果：用 `quick_exit` 注册的函数按照其注册的反向顺序调用。

14 备注：当调用通过 `at_exit` 和 `quick_exit` 注册的函数时，函数 `quick_exit` 是信号安全的 (21.10.4)。

另另：ISO C 7.22.4

# 2.1 动态内存管理 [support.dynamic]

1 头文件 `<new>` 定义了几个管理程序中动态存储分配的函数。它定义了报告内存分配错误的概念。

## 21.6.1 头文件 <new> 概要 [new.syn]

```cpp
namespace std {
  class bad_alloc;
  class bad_array_length;

  enum align_val_t : size_t ();
```

对象并执行对 `exit()` 的调用。控制可以通过抛出一个在 `main` 中被捕获的异常转移到此主函数。

27 宏 `EXIT_FAILURE` 和 `EXIT_SUCCESS` 定义在 `<cstdlib>` 中。

§ 21.6.1 ©/IEC 2017 - 保留所有 492

# ISO/IEC 14882:2017(E)

```
struct notrow_t { explicit notrow_t() = default; };
extern const notrow_t notrow;

handler operator new()();
```

```cpp
using new_handler = void (*)(();)
new_handler get_new_handler() noexcept;
new_handler set_new_handler(new_handler new_p) noexcept;
```

```cpp
// 21.6.4. 指针优化屏
template <class T> const T* launcher(T* p) noexcept
```

```cpp
// 21.6.5. 硬件干扰大小
inline const_t std::hardware_destructive_interference_size = defined;
inline const_t std::hardware_destructive_interference_size = defined;
```

```cpp
void* operator new(size_t size);
void* operator new(size_t size, std::align_val_t alignment);
void* operator new(size_t size, const std::size_t size) noexcept;
void* operator new(size_t size, std::align_val_t alignment, const std::size_t size) noexcept;
```

```cpp
void delete(void* ptr) noexcept;
void delete(void* ptr, size_t size) noexcept;
void delete(void* ptr, std::align_val_t alignment) noexcept;
void delete(void* ptr, size_t size, std::align_val_t alignment) noexcept;
void delete(void* ptr, const std::size_t size) noexcept;
void delete(void* ptr, std::align_val_t alignment, const std::size_t size) noexcept;
```

```cpp
void* operator new(size_t size);
void* operator new(size_t size, std::align_val_t alignment);
void* operator new(size_t size, const std::size_t size) noexcept;
void* operator new(size_t size, std::align_val_t alignment, const std::size_t size) noexcept;
```

```cpp
void* operator new(size_t size);
void* operator new(size_t size, std::align_val_t alignment);
void* operator new(size_t size, const std::size_t size) noexcept;
void* operator new(size_t size, std::align_val_t alignment, const std::size_t size) noexcept;
```cpp

void delete(void* ptr) noexcept;

void delete(void* ptr, size_t size) noexcept;

void delete(void* ptr, std::align_val_t alignment) noexcept;

void delete(void* ptr, size_t size, std::align_val_t alignment) noexcept;

void delete(void* ptr, const std::size_t size) noexcept;

void delete(void* ptr, std::align_val_t alignment, const std::size_t size) noexcept;

```cpp
void* operator new(size_t size);
void* operator new(size_t size, std::align_val_t alignment);
void* operator new(size_t size, const std::size_t size) noexcept;
void* operator new(size_t size, std::align_val_t alignment, const std::size_t size) noexcept;
```cpp

# 2....2 的分配与释放**

10 效果：对应的释放函数 (6.7.4.2) 被 `delete` 表达式 (8.3.5) 调用，以使 `ptr` 的值无效。

11 可替换：C++ 程序可以定义这些函数签名之一，从而替换 C++ 标准库定义的默认版本。如果定义了没有大小参数的函数，程序也应该定义对应的带大小参数的函数。如果定义了带大小参数的函数，程序应当定义对应的版本。

§ 21.6.2.1

©ISO/IEC 2017 - 保留所有 494

# ISO/IEC 14882:2017(E)

不带大小参数。[注：以下行为在未来可能会发生变化，这将导致替换分配函数时需要两个解释放函数。-- 备注结束 --]

要求：`ptr` 应该为空指针，或其值应该表示由调用者向（可能被替换的）`operator new(std::size_t t, 或 operator new(std::size_t t, std::align_val t)` 分配的内存块的地址，且该内存块未被中间插入的 `operator delete` 调用而失效。

要求：如果实现具有更严格的指针对齐 (6.7.4.3)，则 `ptr` 必须是一个安全派生指针（safety-derived pointer）。

要求：如果对齐参数不存在，`ptr` 必须由不带对齐参数的分配函数返回。如果存在，对齐参数应与返回 `ptr` 的分配函数所传递的对齐参数相等。如果存在，大小参数应与返回 `ptr` 的分配函数所传递的大小参数相等。

强制：带有大小参数的 `operator delete` 调用可以更改为不带大小参数的相应 `operator delete`，且不影响内存。[注：对于 `operator delete(void* ptr, std::size_t size)` 的符合实现应提供 `operator delete(ptr)`。-- 备注结束 --]

默认：带有大小参数的函数将其其他参数传递给不带大小参数的相应函数。[注：参见上文“可替换”段落。--]

默认：如果 `ptr` 为空，则不发生任何操作。否则，回收调用者为 `operator delete` 分配的存储。

备注：不确定回收的存储的某部分或全部是否将由后续调用 `operator new` 或 `<cstdlib>` 中的任何一个 `alloc, malloc, calloc` 或 `realloc` 返回。

```
void delete(void* ptr, const std::size_t) noexcept;
void delete(void* ptr, const std::size_t, const std::align_val alignment) noexcept;
```

影响：实现调用的删除 (6.7.4.2) 在从新表达式（new-expression）的新位置调用的构造函数抛出异常时，可能会导致 `ptr` 值失效。

可替换：C++ 程序可以定义具有这两种函数签名之一的函数，它们将取代 C++ 标准库定义的默认版本。

要求：`ptr` 应该为空指针，或其值应该表示由调用者向（可能被替换的）`operator new(std::size_t t, 或 operator new(std::size_t t, std::align_val t)` 分配的内存块的地址，且该内存块未被中间插入的 `operator delete` 调用而失效。

要求：如果实现具有更严格的指针对齐 (6.7.4.3)，则 `ptr` 必须是一个安全派生指针。

要求：如果对齐参数不存在，`ptr` 必须由不带对齐参数的分配函数返回。如果存在，对齐参数应与返回 `ptr` 的分配函数所传递的对齐参数相等。

默认：分别调用 `operator delete(ptr)` 或 `operator delete(ptr, alignment)`。

## 21.6.2.2 数组形式

```
void* operator new[](std::size_t size);
void* operator new[](std::size_t size, std::align_val alignment);
```

影响：新表达式 (8.3.4) 调用分配函数 (6.7.4.1) 来分配存储字节。对于具有扩展对齐（extended-alignment）的类型，调用第二形式，并分配具有指定对齐的存储。在其他情况下调用第一形式，只要对象的类型没有扩展对齐，它将分配适当对齐的存储，以表示任何大小相等或更小的对象。²¹⁸

2 可替换：C++ 程序可以定义具有这两种函数之一的函数，从而取代 C++ 标准库定义的版本。

3 强制：行为与单对象形式定义的行为相同。此要求对这些函数的任何替换版本具有约束力。

4 默认：行为分别返回 `operator new(size)` 或 `operator new(size, alignment)`。

```
void operator new[](std::size_t size, const std::nothrow& noexcept);
void operator new[](std::size_t size, std::align_val alignment, const std::nothrow& noexcept);
```

5 影响：同上，不同在于当由新表达式的放置版本（placement version）时，C++ 程序可能返回空指针作为错误指示或抛出 `bad_alloc` 异常。

6 强制：C++ 程序可以定义具有这两种函数之一的函数，从而取代 C++ 标准库定义的版本。

7 强制：返回指向适当对齐存储 (6.7.4) 的指针，或返回空指针。`operator new[]` 的这些其他版本分别按照从（可能替换的）非放置函数获取的方式返回指针。此要求对这些函数的任何替换版本具有约束力。

8 默认：行为分别调用 `operator new[](size)` 或 `operator new[](size, alignment)`。如果调用返回空，则该调用的结果为空。否则，返回空指针。

```
void operator delete(void* ptr);
void operator delete(std::size_t size) noexcept;
void operator delete(std::size_t size, std::align_val alignment) noexcept;
void operator delete(std::size_t size, std::align_val alignment) noexcept;
```

9 影响：新表达式实现调用的删除 (6.7.4.2) 返回 `ptr` 值。

10 强制：C++ 程序可以定义具有这两种函数之一的函数，从而取代 C++ 标准库定义的版本。6.7.4 的规定不适用于这些 new 和 delete 的放置形式。
