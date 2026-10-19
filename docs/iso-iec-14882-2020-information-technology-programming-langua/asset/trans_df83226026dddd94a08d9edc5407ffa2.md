
## 20.10.3.3 成员函数 [pointer.traits.functions]

```cpp
static pointer pointer_traits::pointer_to(see below r);
static constexpr pointer pointer_traits<T*>::pointer_to(see below r) noexcept;
```

强制要求：对于第一个成员函数，`Ptr::pointer_to(r)` 是良构的。

前提条件：对于第一个成员函数，`Ptr::pointer_to(r)` 返回一个指向 `r` 的指针，通过该指针进行解引用是有效的。

返回：第一个成员函数返回 `Ptr::pointer_to(r)`。第二个成员函数返回 `addressof(r)`。

备注：如果 `element_type` 是 `cv void`，则 `r` 的类型未指定；否则，它是 `element_type&`。

## 20.10.3.4 可选成员 [pointer.traits.optmem]

`pointer_traits` 的特化可以定义本子条款中声明的成员，以定制标准库的行为。

```cpp
static element_type* to_address(pointer p) noexcept;
```

返回：一个类型为 `element_type*` 的指针，该指针引用与参数 `p` 相同的位置。

[注 1：本函数旨在作为 `pointer_to` 的逆操作。如果定义了本函数，它将定制非成员函数 `to_address`（20.10.4）的行为。— 结束注]

## 20.10.4 指针转换 [pointer.conversion]

```cpp
template<class T> constexpr T* to_address(T* p) noexcept;
```

强制要求：`T` 不是函数类型。

返回：`p`。

```cpp
template<class Ptr> constexpr auto to_address(const Ptr& p) noexcept;
```

返回：如果表达式 `pointer_traits<Ptr>::to_address(p)` 良构（见 20.10.3.4），则返回该表达式的结果；否则返回 `to_address(p.operator->())`。

## 20.10.5 指针安全 [util.dynamic.safety]

当以引用该对象的参数调用 `declare_reachable` 的次数超过以引用该对象的参数调用 `undeclare_reachable` 的次数时，该完整对象被声明为可到达的。

```cpp
void declare_reachable(void* p);
```

前提条件：`p` 是安全派生指针（6.7.5.5.4）或空指针值。

效果：如果 `p` 不为空，则由 `p` 引用的完整对象随后被声明为可到达的（6.7.5.5.4）。

抛出：如果系统无法分配跟踪声明为可到达的对象可能需要的额外内存，则可能抛出 `bad_alloc`。

```cpp
template<class T> T* undeclare_reachable(T* p);
```

前提条件：如果 `p` 不为空，则由 `p` 引用的完整对象先前已被声明为可到达的，并且从调用时起到对该对象的最后一次 `undeclare_reachable(p)` 调用为止，该对象处于存活状态（6.7.3）。

返回：`p` 的一个安全派生副本，该副本与 `p` 比较相等。

抛出：无。

[注 1：预期在遇到匹配的 `undeclare_reachable(p)` 调用之前，对 `declare_reachable(p)` 的调用除了占用被引用对象所占用的内存外，还会消耗少量内存。因此，在长时间运行且调用不匹配的程序中可能会出现内存泄漏。— 结束注]

```cpp
void declare_no_pointers(char* p, size_t n);
```

前提条件：指定范围内的任何字节当前均未通过 `declare_no_pointers()` 注册。如果指定范围位于某个已分配对象中，则它必须完全位于该单个已分配对象内。在相应的 `undeclare_no_pointers()` 调用之前，该对象处于存活状态。

[注 2：在采用垃圾回收的实现中，对象中的某个区域通过 `declare_no_pointers()` 注册这一事实并不妨碍该对象被回收。— 结束注]

效果：从 `p` 开始的 `n` 个字节不再包含可跟踪的指针位置，无论其类型如何。因此，如果位于该处的指针所指向的对象是由全局 `operator new` 创建的且先前未被声明为可到达的，那么通过该指针进行解引用是未定义的。

[注 3：这可用于通知垃圾回收器或泄漏检测器，此内存区域无需被跟踪。— 结束注]

抛出：无。

[注 4：如果实现所需的内存分配失败，可以忽略该请求。— 结束注]

```cpp
void undeclare_no_pointers(char* p, size_t n);
```

前提条件：之前已将相同的范围传递给 `declare_no_pointers()`。

效果：为销毁而取消注册先前通过 `declare_no_pointers()` 注册的范围。它必须在对象生命周期结束之前调用。

抛出：无。

```cpp
pointer_safety get_pointer_safety() noexcept;
```

返回：如果实现具有严格的指针安全（6.7.5.5.4），则返回 `pointer_safety::strict`。如果实现具有宽松的指针安全，则 `get_pointer_safety` 返回 `pointer_safety::relaxed` 还是 `pointer_safety::preferred` 由实现定义。224

224) 可以返回 `pointer_safety::preferred` 以表明泄漏检测器正在运行，从而使程序避免出现虚假的泄漏报告。

## 20.10.6 指针对齐 [ptr.align]

```cpp
void* align(size_t alignment, size_t size, void*& ptr, size_t& space);
```

前提条件：

- alignment 是 2 的幂
- ptr 表示至少 space 字节的连续存储的地址

效果：如果可以将按 `alignment` 对齐的 `size` 字节存储放入由 `ptr` 指向且长度为 `space` 的缓冲区中，则该函数更新 `ptr` 以表示此类存储的第一个可能地址，并将 `space` 减少用于对齐的字节数。否则，该函数不执行任何操作。

返回：如果所请求的对齐缓冲区无法放入可用空间，则返回空指针；否则返回调整后的 `ptr` 值。

[注 1：该函数会更新其 `ptr` 和 `space` 参数，以便可以针对同一缓冲区以可能不同的 `alignment` 和 `size` 参数重复调用。— 结束注]

```cpp
template<size_t N, class T>
[[nodiscard]] constexpr T* assume_aligned(T* ptr);
```

强制要求：`N` 是 2 的幂。

前提条件：`ptr` 指向与 `T` 类型相似（7.3.6）的对象 `X`，且 `X` 的对齐要求为 `N`（6.7.6）。

返回：`ptr`。

抛出：无。

[注 2：通过调用 `assume_aligned` 对对象 `X` 所表达的对齐假设可以生成更高效的代码。程序有责任确保该假设确实成立。该调用不会导致编译器验证或强制执行此假设。实现只能对通过 `assume_aligned` 返回的指针访问 `X` 的那些操作做出该假设。— 结束注]

## 20.10.7 分配器实参标签 [allocator.tag]

```cpp
namespace std {
  struct allocator_arg_t { explicit allocator_arg_t() = default; };
  inline constexpr allocator_arg_t allocator_arg{};
}
```

## 管理者辅导计划

第二个问题——与当今办公实践的碎片化以及管理者往往无法为下属提供指导这一事实有关。

辅导方法需要时间、耐心，并愿意通过引导式发现来培养人，而不是简单地给出答案。

## 20.11.1.3.6 修改器 [unique.ptr.single.modifiers]

```cpp
pointer operator->() const noexcept;
```

前提条件：`get() != nullptr`。

返回：`get()`。

[注 1：使用此函数通常要求 `T` 是完整类型。— 结束注]

```cpp
pointer get() const noexcept;
```

返回：存储的指针。

```cpp
deleter_type& get_deleter() noexcept;
const deleter_type& get_deleter() const noexcept;
```

返回：对存储的删除器的引用。

```cpp
explicit operator bool() const noexcept;
```

返回：`get() != nullptr`。

```cpp
pointer release() noexcept;
```

后置条件：`get() == nullptr`。

返回：调用 `release` 开始时 `get()` 所具有的值。

```cpp
void reset(pointer p = pointer()) noexcept;
```

前提条件：表达式 `get_deleter()(get())` 是良构的，具有良好定义的行为，并且不会抛出异常。

效果：将 `p` 赋给存储的指针，然后当且仅当存储指针的旧值 `old_p` 不等于 `nullptr` 时，调用 `get_deleter()(old_p)`。

[注 1：这些操作的顺序很重要，因为调用 `get_deleter()` 可能会销毁 `*this`。— 结束注]

后置条件：`get() == p`。

[注 2：如果调用 `get_deleter()` 销毁了 `*this`，则该后置条件不成立，因为 `this->get()` 不再是有效表达式。— 结束注]

```cpp
void swap(unique_ptr& u) noexcept;
```

前提条件：`get_deleter()` 可交换（16.4.4.3）并且在交换过程中不会抛出异常。

效果：对 `*this` 和 `u` 的存储指针以及存储的删除器调用 `swap`。

## 20.11.1.4 用于具有运行时长度的数组对象的 unique_ptr [unique.ptr.runtime]

### 20.11.1.4.1 概述 [unique.ptr.runtime.general]

```cpp
namespace std {
  template<class T, class D> class unique_ptr<T[], D> {
  public:
    using pointer = see below;
    using element_type = T;
    using deleter_type = D;

    // 20.11.1.4.2, constructors
    constexpr unique_ptr() noexcept;
    template<class U> explicit unique_ptr(U p) noexcept;
    template<class U> unique_ptr(U p, see below d) noexcept;
    template<class U> unique_ptr(U p, see below d) noexcept;
    unique_ptr(unique_ptr&& u) noexcept;
    template<class U, class E> unique_ptr(unique_ptr<U, E>&& u) noexcept;
    constexpr unique_ptr(nullptr_t) noexcept;

    // destructor
    ~unique_ptr();
```

