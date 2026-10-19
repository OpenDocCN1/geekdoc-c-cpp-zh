```
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

```
floating-point fetch_key(floating-point operand,
    memory_order order = memory_order::seq_cst) const noexcept;
```

Effects: Atomically replaces the value referenced by *ptr with the result of the computation applied to the value referenced by *ptr and the given operand. Memory is affected according to the value of order. These operations are atomic read-modify-write operations (6.9.2.2).

Returns: Atomically, the value referenced by *ptr immediately before the effects.

Remarks: If the result is not a representable value for its type (7.1), the result is unspecified, but the operations otherwise have no undefined behavior. Atomic arithmetic operations on floating-point should conform to the std::numeric_limits<floating-point> traits associated with the floating-point type (17.3.3). The floating-point environment (26.3) for atomic arithmetic operations on floating-point may be different than the calling thread’s floating-point environment.

```
floating-point operator op=(floating-point operand) const noexcept;
```

Effects: Equivalent to: return fetch_key(operand) op operand;

# 31.7.5 Partial specialization for pointers [atomics.ref.pointer]

```
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