

# ISO/IEC 14882:2017(E)

## 1 效果：等效于：

```
location->T();
```

```
template <class ForwardIterator>
void destroy(ForwardIterator first, ForwardIterator last);
```

## 2 效果：等效于：

```
for ( ; first=last; ++first)
destroy_at(address(+first));
```

```
template <class ForwardIterator, class Size>
Forwarditerator destroy_n(ForwardIterator first, Size n);
```

## 3 效果：等效于：

```
for ( ; n > 0; (void)++first, --n)
destroy_at(address(+first));
return first;
```

# 23.10.11 内存分配

> [注：头文件 <stdlib> (21.2.2) 声明了此子类中描述的函数。

- void* aligned_alloc(size_t alignment, size_t size)
- void* calloc(size_t nm, size_t size)
- void* malloc(size_t size)
- void* realloc(void* ptr, size_t size);

## 2 效果：这些函数具有 C 标准中指定的语义。

## 3 备注：这些函数不会尝试通过调用 ::operator new(21.6) 来分配存储空间，该空间可以在释放时被声明为可达的，且不需要被声明为 undeclared_reachable() 调用的结果时是可达的。[注：这允许 C 库不受指针限制的影响，代价是提供了较少的垃圾回收检测选项。] 它还允许 malloc() 使用独立的分配区域（arena）实现，从而绕过正常的 declare_reachable() 实现。上述函数永远不应刻意用作 declare_reachable() 的替代品，强烈建议新编写的代码将使用这些函数分配的内存视为通过 `operator new` 分配的内存。

## 5 效果：此函数具有 C 标准中指定的语义。

## 6 备注：此函数不会尝试通过调用 ::operator delete() 来分配存储空间。

参见：ISO C7.22.3

# 23.11 智能指针

## 23.11.1 类模板 unique_ptr

1 unique_ptr 是一个通过指针拥有并管理另一个对象的对象。更准确地说，智能指针是一个对象 u，它存储一个指向第二个对象 p 的指针，并在 u 自身被析构时释放 p（例如，当离开块作用域 (9.7) 时）。在此上下文中，称 u 拥有 p。

2 u 释放 p 的机制被称为 p 的关联删除器（associated deleter），这是一个函数对象，其正确调用会导致 p 的恰当释放（通常是 delete）。

3 令符号 u.p 表示 u 存储的指针，u.d 表示关联的删除器。根据请求，u 可以重置（替换）u.p 和 u.d 为另一个指针和删除器，并在替换操作被认为已完成后，通过关联删除器妥当地释放其拥有的对象。

4 此外，u 可以根据请求将所有权转移给另一个指针 u2。在完成此类转移后，满足以下后条件：

```
(4.1) u.p 等于转移的 u.p,
(4.2) u.p 等于 nullptr;
```

```
(4.3) 如果转移的 u.d 维持状态，转移前的关联所有权已转移到 u.d.
```

与结果的情况一样，u2 在转移被认为完成之前，通过预关联删除器妥当地释放其转移前的所有权。[注：删除器的状态永远不会复制，仅在所有权转移时进行移动或交换。] -- 注结束

5 从此子类中 unique_ptr 模板实例化的每个对象都具有上述智能指针的严格所有权语义。为了部分满足这些语义，u 是可移动构造的（MoveConstructible）且可移动的（Moveable），但不是可赋值的（CopyAssignable）。模板参数 T unique_ptr 可以是一个不完整类型。

6 [注：unique_ptr 的用包括动态分配内存的异常安全性、从函数传递动态分配内存的所有权以及从返回动态分配内存 -- 注结束

```
namespace std {
template<class T> struct default_delete<T>
template<class T> struct default_delete<T[]>;

template<class T, class D = default_delete<T>> class unique_ptr;
template<class T, class D> class unique_ptr<T[], D>;

template<class T, class... Args> unique_ptr<T> make_unique(Args&&... args) = delete;
template<class T> unique_ptr<T[], D> make_unique(size_t n) = ...;
template<class T, class... Args> unique_ptr<T[], D> make_unique(Args&&... args) = ...;

template<class T, class D> void swap(unique_ptr<T, D>& x, unique_ptr<T, D>& y) noexcept;
template<class T1, class D1> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);
tntemplate<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D11 x,, unique__ptrTT,,22,)) no;

template,class1,,,1,,,2,,,2221,,,___T1,,111,,,,__T2,,,,,,) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
template<class T1, class D1, class T2, class D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y) noexcept;
```
,,,,
)
template<class T, class D> bool operator=(const unique_ptr<T, D>& x, nullptr_t) noexcept;
template<class T, class D> bool operator=(unique_ptr<T, D>&& y);
template<class T, class D> bool operator=(nullptr_t, const unique_ptr<T, D>& y) noexcept;
template<class T, class D> bool operator!=(unique_ptr<T, D>);# 23.11.1 默认删除器 [unique_ptr.dltr]

## 23.11.1.1 通用 [unique_ptr.dltr.general]

1 类模板 default_delete 作为类模板 unique_ptr 的默认删除器（析构策略）。

2 default_delete 的模板参数 T 可以是一个不完整类型。

```
namespace std {
template <class U> struct default_delete {
    constexpr default_delete() noexcept = default;
    template <class V> default_delete(const default_delete<V>&) noexcept;
    void operator()(U* const) const;
};
```

```
template <class U> default_delete(const default_delete<U>& other) noexcept = default;
```

1 效果：从另一个 default_delete<U> 对象构造一个 default_delete 对象。

2 备注：此构造函数不应参与重载解析 U* 可以隐式转换为 T。

```
void operator() U*;
```

3 效果：在 ptr 上调用 delete。

4 备注：如果 U 是不完整类型，程序格式错误。此函数不应参与重载解析 U* 可以转换为 T。

# 23.11.1.3 default_delete<T[]> [unique_ptr.dltfr.nft]

```
namespace std {
template <class T> struct default_delete<T[]> {
    constexpr default_delete() noexcept = default;
template <class U> default_delete(const default_delete<U[]>&) noexcept = default;
template<class U> void operator()(U* ptr) const;
};
}
```

```
template <class U> default_delete(const default_delete<U[]>& other) noexcept;
```

1 效果：在另一个 default_delete<U[]> 对象之后构造一个 default_delete 对象。

2 备注：此构造函数不应参与重载解析 U* 可以转换为 T。

template <class U> void operator() U* const;

3 效果：在 ptr 上调用 delete()。

4 备注：如果 U 是不完整类型，程序格式错误。此函数不应参与重载解析 U*。

# 23.11.1.2 用于对象的 unique_ptr [unique.ptr.single]

```
namespace std {
    template <class T, class D = default_delete<T>> class unique_ptr {
public:
    using pointer = see below;
    using element_type = T;
    using deleter = D;

    // // 23.11.2.1 构造函数
    constexpr unique_ptr() noexcept;
    explicit unique_ptr(pointer p) noexcept;
    unique_ptr(pointer p, see below d1) noexcept;
    unique_ptr(pointer p, see below d2) noexcept;
    unique_ptr(const unique_ptr& u) noexcept;
    constexpr unique_ptr(const unique_ptr& u) noexcept;
    template <class U, class E> unique_ptr(unique_ptr<U, E>&& u) noexcept;

    // // 23.11.2.2 析构函数
    ~unique_ptr();

    // // 23.11.2.3 赋值
    unique_ptr& operator=(const unique_ptr& u) noexcept;
    template <class U, class E> unique_ptr& operator=(unique_ptr<U, E>&& u) noexcept;
    unique_ptr& operator=(nullptr_t) noexcept;

    // // 23.11.2.4 观察者
    add_value_reference<T_> operator*() const noexcept;
    pointer operator->() const noexcept;
    pointer get() const noexcept;
    deleter_type get_deleter() const noexcept;
    const deleter_type get_deleter() const noexcept;
    explicit operator bool() const noexcept;

    // // 23.11.2.5 修改符
    void release() noexcept;
    void reset(pointer p = nullptr) noexcept;
    void swap(unique_ptr&& u) noexcept;

    // 禁止从左值拷贝
    unique_ptr(const unique_ptr&) = delete;
    unique_ptr& operator=(const unique_ptr&) = delete;
};
};
```

