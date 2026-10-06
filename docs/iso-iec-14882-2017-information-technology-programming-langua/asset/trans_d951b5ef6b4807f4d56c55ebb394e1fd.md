

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

# 21.6.1 头文件 <new> 概要 [new.syn]

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

10 效果：对应的释放函数 (6.7.4.2) 被 delete 表达式 (8.3.5) 调用，以使 ptr 的值无效。

11 可替换：C++ 程序可以定义这些函数签名之一，从而替换 C++ 标准库定义的默认版本。如果定义了没有大小参数的函数，程序也应该定义对应的带大小参数的函数。如果定义了带大小参数的函数，程序应当定义对应的版本。

§ 21.6.2.1

©ISO/IEC 2017 - 保留所有 494

