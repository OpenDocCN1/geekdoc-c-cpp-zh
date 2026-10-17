
返回值：如果实现具有严格安全 (`3.7.4.3`)，返回 `pointer_safety::strict`。如果实现具有松散安全，则由实现定义返回 `pointer_safety::relaxed` 还是 `pointer_safety::preferred`。

## 20.6.8 分配器特征

类模板 `allocator_traits` 为所有分配器类型提供统一的接口。然而，分配器不能是非类类型，尽管 `allocator_traits` 提供了所有所需的接口。[备注：因此，总是可以从分配器创建一个派生类。]

```
namespace std {
    template <class Alloc> struct allocator_traits {
        typedef Alloc allocator_type;

        typedef typename Alloc::value_type value_type;

        typedef typename Alloc::pointer pointer;
        typedef typename Alloc::const_pointer const_pointer;
        typedef typename Alloc::void_pointer void_pointer;
        typedef typename Alloc::const_void_pointer const_void_pointer;

        typedef typename Alloc::difference_type difference_type;
        typedef typename Alloc::size_type size_type;

        typedef typename Alloc::propagate_on_container_copy_assignment propagate_on_container_copy_assignment;
        typedef typename Alloc::propagate_on_container_move_assignment propagate_on_container_move_assignment;
        typedef typename Alloc::propagate_on_container_swap propagate_on_container_swap;

        template <class T> using rebind_alloc = typename Alloc::template rebind<T>::other;
        template <class T> using rebind_traits = allocator_traits<rebind_alloc<T>>;

        static pointer allocate(Alloc a, size_type n);
        static pointer deallocate(Alloc a, size_type n, const_void_pointer hint);

        static void deallocate(Alloc a, pointer p, size_type n);

        template <class T, class... Args>
        static void construct(Alloc a, T* p, Args&&... args);

        template <class T>
        static void destroy(Alloc a, T* p);

        size_type max_size(const Alloc a);

        static Alloc select_on_container_copy_construction(const Alloc rhs);
    }
}
```

### 20.6.8.1 分配器特征成员类型 [allocator.traits.types]

- `typedef typename Alloc::pointer pointer;`

  - 类型：如果存在该类型则为 `Alloc::pointer`；否则为 `value_type*`。

- `typedef typename Alloc::const_pointer const_pointer;`

  - 类型：如果存在该类型则为 `Alloc::const_pointer`；否则为 `pointer_traits<pointer>::rebind<const_type>`。

- `typedef typename Alloc::void_pointer void_pointer;`

  - 类型：如果存在该类型则为 `Alloc::void_pointer`；否则为 `pointer_traits<pointer>::rebind<void>`。

- `typedef typename Alloc::const_void_pointer const_void_pointer;`

  - 类型：如果存在该类型则为 `Alloc::const_void_pointer`；否则为 `pointer_traits<pointer>::rebind<const void>`。

- `typedef typename Alloc::difference_type difference_type;`

  - 类型：如果存在该类型则为 `Alloc::difference_type`；否则为 `pointer_traits<pointer>::difference_type`。

- `typedef typename Alloc::size_type size_type;`

  - 类型：如果存在该类型则为 `Alloc::size_type`；否则为 `make_unsigned<difference_type>::type`。

- `typedef typename Alloc::propagate_on_container_copy_assignment propagate_on_container_copy_assignment;`

  - 类型：如果存在该类型则为 `propagate_on_container_copy_assignment`；否则为 `false_type`。

- `typedef typename Alloc::propagate_on_container_move_assignment propagate_on_container_move_assignment;`

  - 类型：如果存在该类型则为 `propagate_on_container_move_assignment`；否则为 `false_type`。

- `typedef typename Alloc::propagate_on_container_swap propagate_on_container_swap;`

  - 类型：如果存在该类型则为 `propagate_on_container_swap`；否则为 `false_type`。

`template <class T> alias rebind_alloc = typename Alloc::template rebind<T>::other;`

### 20.6.8.2 分配器特征静态成员函数 [allocator.traits.members]

```cpp
static pointer allocate(Alloc& a, size_type n);
```

- 1 返回：如果该表达式形式良好，则返回 `a.allocate(n, hint)`；否则返回 `a.allocate(n)`。

```cpp
static void deallocate(Alloc& a, size_type n);
```

- 2 效果：调用 `a.deallocate(p, n)`。

- 3 抛出：无。

```cpp
template <class T, class Args>
static void construct(Alloc& a, T* p, Args&&... args);
```

```cpp
template <class T>
static void destroy(Alloc& a, T* p);
```

- 6 效果：如果该调用形式良好，则调用 `a.destroy(p)`；否则调用 `p->~T()`。

```cpp
static size_type max_size(Alloc& a);
```

- 7 返回：如果表达式形式良好，则返回 `a.max_size()`；否则返回 `numeric_limits<size_type>::max()`。

`static Alloc select_on_container_copy_construction(const Alloc& rhs);`

- 8 返回：如果该表达式形式良好，则返回 `rhs.select_on_container_copy_construction()`；否则返回 `rhs`。

## 20.6.9 默认分配器

[default.allocator]

```cpp
namespace std {
    template <class T> class allocator {

    // 针对 void 的特化：
    template <> class allocator<void> {
    public:
        typedef void* pointer;
        typedef const void* const_pointer;
        // 指向 void 的成员是不可能的。
        typedef void value_type;
        template <class U> struct rebind { typedef allocator<U> other; };
    };

    template <class T> class allocator {
    public:
        typedef size_t size_type;
        typedef ptrdiff_t difference_type;
        typedef T* pointer;
        typedef T* const_pointer;
        typedef T& reference;
        typedef const T& const_reference;
        typedef T value_type;
        template <class U> struct rebind { typedef allocator<U> other; };

        allocator() : noexcept;
        allocator(const allocator&) : noexcept;
        template <class U> allocator(const allocator<U>&) : noexcept;
        ~allocator();

        pointer address(const reference& x) const noexcept;
        const_pointer address(const reference& x) const noexcept;

        pointer allocate(size_type n, allocator<void>::const_pointer hint = 0);
        void deallocate(pointer p, size_type n);
        size_type max_size() const noexcept;

        template <class U, class... Args>
        construct(U* p, Args&&... args);
        template <class U>
        void destroy(U* p);
    };
}
```

### 20.6.9.1 分配器成员 [allocator.members]

析构函数外，默认分配器的成员函数不应由于不同线程并发调用这些成员函数而引入数据竞态（`1.10`）。分配特定存储单元的函数调用应在单一的全排序中发生，且每次释放都应发生在顺序中的下次分配（如果有）之前。

# ISO/IEC 14882:2011(E)

```cpp
template <T> void return_temporary_buffer(T* p);
```

**影响：** 释放 `p` 所指向的缓冲区。

**要求：** 该缓冲区必须在此之前通过 `get_temporary_buffer` 分配。

## 20.6.12 特殊化算法 [specialized.algorithms]

在以下算法中作为正向模板使用的所有迭代器都要求定义了 `operator*` 并返回一个指向 `T` 的指针。在算法 `uninitialized_copy` 中，正向模板 `InputIterator` 被要求满足输入迭代器的要求 (`24.2.5`)。在后续的所有算法中，正向模板 `ForwardIterator` 都要求满足正向迭代器的要求，并且要求具有在有效迭代器的递增、赋值、比较或解引用时不抛出异常的属性。如果此处抛出异常，则没有产生影响。

### 20.6.12.1 addressof [specialized.addressof]

```cpp
template <T> addressof(T& r) noexcept;
```

**返回：** 由 `r` 引用的对象或函数的实际地址，即使在存在重载运算符 `&` 的情况下也是。

### 20.6.12.2 uninitialized_copy [uninitialized.copy]

```cpp
template <class InputIterator, class ForwardIterator>
ForwardIterator uninitialized_copy(InputIterator first, InputIterator last,
ForwardIterator result);
```

**影响：**

```cpp
for (; first != last; ++result, ++first)
    ::new (static_cast<void*>(&result))
    typename iterator_traits<ForwardIterator>::value_type(first);
```

**返回：** `result`

```cpp
template <class InputIterator, class Size, class ForwardIterator>
ForwardIterator uninitialized_copy_n(InputIterator first, Size n,
ForwardIterator result);
```

**影响：**

```cpp
for (; n > 0; ++result, ++first, --n)
    ::new (static_cast<void*>(&result))
    typename iterator_traits<ForwardIterator>::value_type(first);
```

**返回：** `result`

### 20.6.12.3 uninitialized_fill [uninitialized.fill]

```cpp
template <class ForwardIterator, class T>
void uninitialized_fill(ForwardIterator first, ForwardIterator last,
const T& x);
```

**影响：**

```cpp
for (; first != last; ++first)
    new (static_cast<void*>(&*first))
    typename iterator_traits<ForwardIterator>::value_type(x);
```

### 20.6.12.4 uninitialized_fill_n

```cpp
template <class ForwardIterator, class Size, class T>
ForwardIterator uninitialized_fill_n(ForwardIterator first, Size n, const T& x);
```

**影响：**

```cpp
for (; first != last; ++first)
    new (static_cast<void*>(&*first))
    typename iterator_traits<ForwardIterator>::value_type(x);
    return first;
```

## 20.6.13 C 库

表 45 描述了头文件 `<cstdlib>`。

### 表 45 — 头文件 <cstdlib> 概要

| 类型 | 名称(s) |

|---|---|---|| 函数: | `calloc` `malloc` |

| | `realloc` |

其内容与标准 C 库头文件 `<cstdlib.h>` 相同，有以下变化：

函数 `calloc()`、`malloc()` 和 `realloc()` 不尝试通过调用 `::operator new()` 来分配存储 (`18.6`)。

`free()` 不尝试通过调用 `::operator delete()` 来释放存储。

**另见：** ISO C 第 7.11.2 条。
