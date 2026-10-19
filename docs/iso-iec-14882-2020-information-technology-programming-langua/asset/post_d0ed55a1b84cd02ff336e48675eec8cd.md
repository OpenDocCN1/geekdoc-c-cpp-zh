
```cpp
void notify_all() const noexcept;
```

Effects: Unblocks the execution of all atomic waiting operations on *ptr that are eligible to be unblocked (31.6) by this call.

Remarks: This function is an atomic notifying operation (31.6) on atomic object *ptr.

## 31.7.3 Specializations for integral types [atomics.ref.int]

There are specializations of the atomic_ref class template for the integral types char, signed char, unsigned char, short, unsigned short, int, unsigned int, long, unsigned long, long long, unsigned long long, char8_t, char16_t, char32_t, wchar_t, and any other types needed by the typedefs in the header <cstdint> (17.4.2). For each such type integral, the specialization atomic_ref<integral> provides additional atomic operations appropriate to integral types.

> [Note 1: The specialization atomic_ref<bool> uses the primary template (31.7). — end note]

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

Descriptions are provided below only for members that differ from the primary template.

The following operations perform arithmetic computations. The key, operator, and computation correspondence are identified in Table 144.

```cpp
floating-point fetch_key(floating-point operand,
    memory_order order = memory_order::seq_cst) const noexcept;
```

Effects: Atomically replaces the value referenced by *ptr with the result of the computation applied to the value referenced by *ptr and the given operand. Memory is affected according to the value of order. These operations are atomic read-modify-write operations (6.9.2.2).

Returns: Atomically, the value referenced by *ptr immediately before the effects.

Remarks: If the result is not a representable value for its type (7.1), the result is unspecified, but the operations otherwise have no undefined behavior. Atomic arithmetic operations on floating-point should conform to the std::numeric_limits<floating-point> traits associated with the floating-point type (17.3.3). The floating-point environment (26.3) for atomic arithmetic operations on floating-point may be different than the calling thread’s floating-point environment.

```cpp
floating-point operator op=(floating-point operand) const noexcept;
```

Effects: Equivalent to: return fetch_key(operand) op operand;

## 31.7.5 Partial specialization for pointers [atomics.ref.pointer]

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

1 The template argument for T shall meet the Cpp17CopyConstructible and Cpp17CopyAssignable requirements. The program is ill-formed if any of

- (1.1) — is_trivially_copyable_v\<T\>,
- (1.2) — is_copy_constructible_v\<T\>,
- (1.3) — is_move_constructible_v\<T\>,
- (1.4) — is_copy_assignable_v\<T\>, or
- (1.5) — is_move_assignable_v\<T\>

is false.

[Note 1: Type arguments that are not also statically initializable can be difficult to use. — end note]

2 The specialization atomic\<bool\> is a standard-layout struct.

3 [Note 2: The representation of an atomic specialization need not have the same size and alignment requirement as its corresponding argument type. — end note]

## 31.8.2 Operations on atomic types [atomics.types.operations]

```cpp
constexpr atomic() noexcept(is_nothrow_default_constructible_v<T>);
```

1 Mandates: is_default_constructible_v\<T\> is true.

2 Effects: Initializes the atomic object with the value of T(). Initialization is not an atomic operation (6.9.2).
