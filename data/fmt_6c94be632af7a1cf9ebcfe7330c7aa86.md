
- 16 效果：等同于：

```cpp
return make_from_tuple<T>(use_allocator_construction_args<T>(
alloc, std::forward<Args>(args)...));
```

```cpp
template<class T, class Alloc, typename... Args>
constexpr T* uninitialized_construct_using_allocator(T* p, const Alloc& alloc, Args&... args);
```

- 效果：等同于：

```cpp
return apply([&]<class... Us>(U&&... xs) {
  construct_at(p, std::forward<Us>(xs)...);
  use_allocator_construction_args<T>(alloc, std::forward<Args>(args)...);
};
```

# 20.10.9 分配器特性 (Allocator traits)

## 20.10.9.1 General [allocator.traits]

- 分配器特性为所有分配器提供了一个统一的接口。如果 `allocator_traits` 提供了所有需要的内容，则分配器不能是非类类型。[注：因此，始终可以从分配器创建派生类。]

```cpp
namespace std {
template<class Alloc> struct allocator_traits {
    using allocator = Alloc;
    using value_type = typename Alloc::value_type;
    using pointer = see below;
    using const_pointer = see below;
    using void_pointer = see below;
    using const_void_pointer = see below;
    using difference_type = see below;
    using size_type = see below;
    using propagate_on_assignment = see below;
    using propagate_on_move = see below;
    using propagate_on_swap = see below;
    using is_always_equal = see below;
    [[nodiscard]] static constexpr const_pointer allocate(Alloc& a, size_type n);
    [[nodiscard]] static constexpr const_pointer deallocate(Alloc& a, size_type n);
    static constexpr void deallocate(Alloc& a, pointer p, size_type n);
    template<class T, typename... Args>
    static constexpr void construct(Alloc& a, T* p, Args&... args);
    template<class T>
    static constexpr void destroy(Alloc& a, T* p);
    static constexpr size_type max_size(const Alloc& a) noexcept;
    static constexpr select_on_construction(const Alloc& rhs);
};
```

## 20.10.9.2 Member types [allocator.traits.types]

```cpp
using pointer = see below;
```

- 类型：如果 qualified-id `Alloc::pointer` 有效且表示一个类型 (13.10.3)，否则为 `value_type*`。

```cpp
using const_pointer = see below;
```

- 类型：如果 qualified-id `Alloc::const_pointer` 有效且表示一个类型 (13.10.3)，否则为 `pointer_traits::rebind<const_type>`。

```cpp
using void_pointer = see below;
```

- 类型：如果 qualified-id `Alloc::void_pointer` 有效且表示一个类型 (13.10.3)，否则为 `pointer_traits::rebind<void>`。

```cpp
using const_void_pointer = see below;
```

- 类型：如果 qualified-id `Alloc::const_void_pointer` 有效且表示一个类型 (13.10.3)，否则为 `pointer_traits::rebind<const_type>`。

```cpp
using difference_type = see below;
```

- 类型：如果 qualified-id `Alloc::difference_type` 有效且表示一个类型 (13.10.3)，否则为 `pointer_traits::difference_type`。

```cpp
using size_type = see below;
```

- 类型：如果 qualified-id `Alloc::size_type` 有效且表示一个类型 (13.10.3)，否则为 `make_unsigned_t<difference_type>`。

```cpp
using propagate_on_assignment = see below;
```

- 类型：如果 qualified-id `Alloc::propagate_on_assignment` 有效且表示一个类型 (13.10.3)，否则为 `false_type`。

```cpp
using propagate_on_move = see below;
```

- 类型：如果 qualified-id `Alloc::propagate_on_move` 有效且表示一个类型 (13.10.3)，否则为 `false_type`。

```cpp
using is_always_equal = see below;
```

- 类型：如果 qualified-id `Alloc::is_always_equal` 有效且表示一个类型 (13.10.3)，否则为 `empty_type`。

```cpp
template<class T> rebind<T> = see below;
```

- 别名：如果 qualified-id `Alloc::rebind<T>` 有效且表示一个类型 (13.10.3)，否则为 `Alloc<T, Args>`，其中 `Alloc` 是 `rebind<U, Args>` 的实例化，`Args` 为零或多个参数；`rebind_alloc` 是非法的。

## 20.10.9.3 Static member functions [allocator.traits::members]

```cpp
[[nodiscard]] static const pointer allocate(Alloc& a, size_type n);
```

- 1. 返回 `allocate(n)`。

```cpp
[[nodiscard]] static const pointer allocate(Alloc& a, size_type n, const void_pointer* hint);
```

- 2. 如果异常是合法的，返回 `a.allocate(n)`，否则返回 `a.allocate(n)`。

```cpp
static const void deallocate(Alloc& a, pointer p, size_type n);
```

- 3. 效果：调用 `deallocate(p, n)`。
- 4. 抛出：无。

```cpp
template<class T, class... Args>
static const void construct(Alloc& a, T* p, Args&&... args);
```

- 5. 效果：如果调用是合法的，调用 `construct(p, std::forward<Args>(args)...)`；否则调用 `construct_at(p, std::forward<Args>(args)...)`。

```cpp
template<class T>
static constexpr void destroy(Alloc& a, T* p);
```

```cpp
static constexpr size_type max_size(const Alloc& a) noexcept;
```

```cpp
static constexpr select_on_container_construction(const Alloc& rhs);
```

# 20.10 默认分配器 (The default allocator)

## 20.10.1 General [allocator.traits]

- 1. 除了析构函数外，默认分配器的成员函数不会由于不同线程并发调用这些成员函数而引入数据态。调用这些分配或释放特定存储单元的函数是单次整体操作，且每次释放调用应在下一次分配（如果有）之前发生。

```cpp
namespace std {
    template<class T> class allocator {
public:
        using value_type = T;
        using size_type = size_t;
        using difference_type = ptrdiff_t;
        using propagate_on_container_move = true;
        using is_always_equal = true;
        constexpr allocator() noexcept;
        allocator(const allocator& other) noexcept;
        template<class U> allocator(const allocator<U>&) noexcept;
        constexpr allocator() = default;
        allocator& operator=(const allocator&) = default;
        [[nodiscard]] constexpr T* allocate(size_t n);
        void deallocate(T* p, size_t n);
    };
}
```

## 20.10.2 Members [allocator.traits.types]

- 2. 强制：`T` 不是不完整类型 (6.8)。
- 3. 返回：指向 `n` 个元素数组的首元素的指针。
- 4. 备注：数组的存储通过调用 `::operator new` (17.6.3) 分配，但未规定何时或如何调用此函数。此函数返回对象的大小，而不是任何元素的大小。
- 5. 抛出：如果 `numeric_limits<size_t>::max() / sizeof(T) < n`，则抛出 `bad_array_length`；如果无法获取存储，则抛出 `bad_alloc`。
- 6. 前提：`p` 是从 `allocate()` 获取的指针。`n` 等于调用 `allocate` 时作为第一个参数的值。
- 7. 效果：释放 `p` 所引的存储。
- 8. 备注：使用 `::operator delete` (17.6.3)，但未规定何时调用此函数。

# ISO/IEC 14882:2020(E)

## 20.10.10.3 运算符

[allocator.globals]

```cpp
template<class T, class U>
constexpr bool operator==(const allocator<T>&, const allocator<U>&) noexcept;
```
返回：`true`。

## 20.10.11 addressof

[specialized.addressof]

```cpp
template<class T> constexpr T addressof(T& r) noexcept;
```
返回：由 `r` 引用的对象或函数的地址，即使在存在重载运算符 `&` 的情况下也是如此。

备注：如果 `E` 是左值常量表达式 (3.13)，则 `addressof(E)` 是一个常量子表达式。

## 20.10.12 C 库内存分配

[c.malloc]

> [注 1：头文件 `<cstdlib>` (17.2) 声明了在此子句中定义的函数。—— 注结束]

```cpp
void* alloc(size_t alignment, size_t size);
void* calloc(size_t nmemb, size_t size);
void* malloc(size_t size);
void* realloc(void* ptr, size_t size);
```
影响：这些函数具有 C 标准库中的语义。

备注：这些函数不会尝试通过调用 `::operator new()` (17.6.3) 来分配存储。用这些函数分配的存储在释放时隐式声明释放（参见 6.7.5.5），未能声明释放将导致未定义行为的结果。

> [注 2：这允许现有的 C 库倾向于对无法安全删除的指针进行限制，代价是为 malloc 分配的对象提供更宽松的垃圾回收和泄漏选项。它还允许 `malloc()` 使用分配区域（arena）来实现，从而绕过普通的 `realloc` 实现。—— 注结束]

这些函数在返回的存储中隐式创建对象 (6.7.2) 并返回指向合适对象的指针。在 `calloc` 和 `realloc` 的情况下，对象在存储清零或拷贝之前创建。

```cpp
void free(void* ptr);
```
影响：此函数具有 C 标准库中的语义。

备注：此函数不会尝试通过调用 `::operator delete()` 来释放存储。

另请参见：ISO 7.2.3

## 20.11 智能指针

[smart.ptr]

## 20.11.1.1 类模板 unique_ptr

[unique.ptr]

`unique_ptr` 是一个拥有另一个对象并通过指针管理该对象的类型。更准确地说，`unique_ptr u` 是一个指向对象 `p` 指针的指针，并在 `u` 自身被销毁时删除 `p`（例如当离开块作用域 (8.8)）。在此上下文中，称 `u` 拥有 `p`。

`u` 删除 `p` 的机制被称为 `u` 的删除器（deleter），这是一个函数对象，其调用会导致 `p` 的适当释放。

假设符号 `u deletes the pointer pointed to by u`，令 `d` 表示关联的删除器。根据请求，`u` 可以用另一个指针替换（replace）`p.u` 和 `u`，并在认为完成之前通过关联的删除器正确删除其拥有的对象。

由 20.11.1 指定的 `unique_ptr` 模板实例化的每个类型 `U` 对象都具有严格的所有权语义，这是 `unique_ptr` 特有的。为了部分满足这些语义，`U` 满足 `Cpp17MoveConstructible` 和 `Cpp17MoveAssignable`，但不是 `Cpp17CopyCopyable` 也不是 `Cpp17Assignable`。`unique_ptr` 的模板 `T` 可以是一个不完整类型。

[注 1：`unique_ptr` 的用途包括为动态分配的内存提供异常安全性、将动态分配内存的所有权传递给函数，以及从函数返回动态分配内存—— 注结束]

## 20.11.1.2 默认删除器 [unique_ptr.dltr]

### 20.11.1.2.1 一般地 [unique_ptr.dltr.general]

`default_delete` 的模板 `T` 作为类模板 `unique_ptr` 的默认删除器（析构策略）。

## 20.11.1.2.2 default_delete [unique_ptr.dltr.dft]

```cpp
namespace std {
  template<class T> struct default_delete {
    const default_delete() noexcept = default;
    template<class U> default_delete(const default_delete<U>&);
    void operator()(T*) const;
  };
}
```
`template<class U> default_delete(const default_delete<U>& other);`
- 约束：`U*` 可隐式转换为 `T*`。
- 影响：从另一个 `default_delete<U>` 对象构造一个 `default_delete` 对象。

`void operator()(T*) const;`
- 强制：`T` 是完整类型。
- 影响：对 `ptr` 调用 `delete`。

## 20.11.1.2.3 default_delete<T[]> [unique_ptr.dltr.dft]

```cpp
namespace std {
```
