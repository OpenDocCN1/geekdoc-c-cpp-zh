

```cpp
void notify_all() const noexcept;
```

Effects: 通过此调用解除对 *ptr 的所有符合解除阻塞条件的原子等待操作的执行阻塞（31.6）。

Remarks: 此函数是对原子对象 *ptr 的原子通知操作（31.6）。

## 31.7.3 针对整型类型的特化 [atomics.ref.int]

`atomic_ref` 类模板针对整型类型 char、signed char、unsigned char、short、unsigned short、int、unsigned int、long、unsigned long、long long、unsigned long long、char8_t、char16_t、char32_t、wchar_t 以及头文件 <cstdint>（17.4.2）中 typedef 所需的任何其他类型提供了特化。对于每种此类类型 integral，特化 `atomic_ref<integral>` 提供了适用于整型类型的额外原子操作。

> [Note 1: 特化 `atomic_ref<bool>` 使用主模板（31.7）。 — end note]

```cpp
namespace std {
  template<> struct atomic_ref<integral> {
  private:
    integral* ptr;            // exposition only
  public:
    using value_type = integral;
    using difference_type = value_type;
    static constexpr size_t required_alignment = implementation-defined;

    static constexpr bool is_always_lock_free = implementation-defined;
    bool is_lock_free() const noexcept;

    explicit atomic_ref(integral&);
    atomic_ref(const atomic_ref&) noexcept;
    atomic_ref& operator=(const atomic_ref&) = delete;

    void store(integral, memory_order = memory_order::seq_cst) const noexcept;
    integral operator=(integral) const noexcept;
    integral load(memory_order = memory_order::seq_cst) const noexcept;
    operator integral() const noexcept;

    integral exchange(integral,
                    memory_order = memory_order::seq_cst) const noexcept;
    bool compare_exchange_weak(integral&, integral,
                               memory_order, memory_order) const noexcept;
    bool compare_exchange_strong(integral&, integral,
                                 memory_order, memory_order) const noexcept;
    bool compare_exchange_weak(integral&, integral,
                               memory_order = memory_order::seq_cst) const noexcept;
    bool compare_exchange_strong(integral&, integral,
                                 memory_order = memory_order::seq_cst) const noexcept;

    integral fetch_add(integral,
                       memory_order = memory_order::seq_cst) const noexcept;
    integral fetch_sub(integral,
                       memory_order = memory_order::seq_cst) const noexcept;
    integral fetch_and(integral,
                       memory_order = memory_order::seq_cst) const noexcept;
    integral fetch_or(integral,
                      memory_order = memory_order::seq_cst) const noexcept;
    integral fetch_xor(integral,
                       memory_order = memory_order::seq_cst) const noexcept;

    integral operator++(int) const noexcept;
    integral operator--(int) const noexcept;
    integral operator++() const noexcept;
    integral operator--() const noexcept;
    integral operator+=(integral) const noexcept;
    integral operator-=(integral) const noexcept;
  };
}
```

```cpp
bool compare_exchange_strong(floating-point&, floating-point,
    memory_order = memory_order::seq_cst) const noexcept;

floating-point fetch_add(floating-point,
    memory_order = memory_order::seq_cst) const noexcept;
floating-point fetch_sub(floating-point,
    memory_order = memory_order::seq_cst) const noexcept;

floating-point operator+=(floating-point) const noexcept;
floating-point operator-=(floating-point) const noexcept;

void wait(floating-point, memory_order = memory_order::seq_cst) const noexcept;
void notify_one() const noexcept;
void notify_all() const noexcept;
};
}
```

仅对与主模板不同的成员提供描述。

以下操作执行算术计算。键、运算符和计算的对应关系在表 144 中标识。

```cpp
floating-point fetch_key(floating-point operand,
    memory_order order = memory_order::seq_cst) const noexcept;
```

Effects: 原子地用 *ptr 引用的值与给定操作数应用计算得到的结果替换 *ptr 引用的值。内存受 order 值的影响。这些操作是原子读写修改操作（6.9.2.2）。

Returns: 原子地，在效果发生前 *ptr 引用的值。

Remarks: 如果结果不是其类型的可表示值（7.1），结果是不确定的，但操作本身没有未定义行为。对浮点数的原子算术操作应符合与浮点类型关联的 `std::numeric_limits<floating-point>` 特征（17.3.3）。对浮点数的原子算术操作的浮点环境（26.3）可能与调用线程的浮点环境不同。

```cpp
floating-point operator op=(floating-point operand) const noexcept;
```

Effects: 等价于：return fetch_key(operand) op operand;

## 31.7.5 指针的部分特化 [atomics.ref.pointer]

```cpp
namespace std {
template<class T> struct atomic_ref<T*> {
private:
    T** ptr;            // exposition only
public:
    using value_type = T*;
    using difference_type = ptrdiff_t;
    static constexpr size_t required_alignment = implementation-defined;

    static constexpr bool is_always_lock_free = implementation-defined;
    bool is_lock_free() const noexcept;

    explicit atomic_ref(T*&);
    atomic_ref(const atomic_ref&) noexcept;
    atomic_ref& operator=(const atomic_ref&) = delete;

    void store(T*, memory_order = memory_order::seq_cst) const noexcept;
    T* operator=(T*) const noexcept;
    T* load(memory_order = memory_order::seq_cst) const noexcept;
    operator T*() const noexcept;

    T* exchange(T*, memory_order = memory_order::seq_cst) const noexcept;
    bool compare_exchange_weak(T*&, T*,
        memory_order, memory_order) const noexcept;
```

```cpp
static constexpr bool is_always_lock_free = implementation-defined;
bool is_lock_free() const volatile noexcept;
bool is_lock_free() const noexcept;

// 31.8.2, operations on atomic types
constexpr atomic() noexcept(is_nothrow_default_constructible_v<T>);
constexpr atomic(T) noexcept;
atomic(const atomic&) = delete;
atomic& operator=(const atomic&) = delete;
atomic& operator=(const atomic&) volatile = delete;

T load(memory_order = memory_order::seq_cst) const volatile noexcept;
T load(memory_order = memory_order::seq_cst) const noexcept;
operator T() const volatile noexcept;
operator T() const noexcept;
void store(T, memory_order = memory_order::seq_cst) volatile noexcept;
void store(T, memory_order = memory_order::seq_cst) noexcept;
T operator=(T) volatile noexcept;
T operator=(T) noexcept;

T exchange(T, memory_order = memory_order::seq_cst) volatile noexcept;
T exchange(T, memory_order = memory_order::seq_cst) noexcept;
bool compare_exchange_weak(T&, T, memory_order, memory_order) volatile noexcept;
bool compare_exchange_weak(T&, T, memory_order, memory_order) noexcept;
bool compare_exchange_strong(T&, T, memory_order, memory_order) volatile noexcept;
bool compare_exchange_strong(T&, T, memory_order, memory_order) noexcept;
bool compare_exchange_weak(T&, T, memory_order = memory_order::seq_cst) volatile noexcept;
bool compare_exchange_weak(T&, T, memory_order = memory_order::seq_cst) noexcept;
bool compare_exchange_strong(T&, T, memory_order = memory_order::seq_cst) volatile noexcept;
bool compare_exchange_strong(T&, T, memory_order = memory_order::seq_cst) noexcept;

void wait(T, memory_order = memory_order::seq_cst) const volatile noexcept;
void wait(T, memory_order = memory_order::seq_cst) const noexcept;
void notify_one() volatile noexcept;
void notify_one() noexcept;
void notify_all() volatile noexcept;
void notify_all() noexcept;
};
}
```

1 模板参数 T 必须满足 Cpp17CopyConstructible 和 Cpp17CopyAssignable 要求。如果以下任一条件为假，程序即为格式错误：

- (1.1) — is_trivially_copyable_v\<T\>,
- (1.2) — is_copy_constructible_v\<T\>,
- (1.3) — is_move_constructible_v\<T\>,
- (1.4) — is_copy_assignable_v\<T\>, 或
- (1.5) — is_move_assignable_v\<T\>

[Note 1: 不是静态可初始化的类型参数可能难以使用。 — end note]

2 特化 `atomic<bool>` 是一个标准布局结构体。

3 [Note 2: 原子特化的表示不必与其对应参数类型具有相同的大小和对齐要求。 — end note]

## 31.8.2 原子类型上的操作 [atomics.types.operations]

```cpp
constexpr atomic() noexcept(is_nothrow_default_constructible_v<T>);
```

1 Mandates: is_default_constructible_v\<T\> 为 true。

2 Effects: 使用 T() 的值初始化原子对象。初始化不是原子操作（6.9.2）。

