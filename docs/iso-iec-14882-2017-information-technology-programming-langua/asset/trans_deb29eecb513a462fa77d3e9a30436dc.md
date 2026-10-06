

# ISO/IEC 14882:2017(E)

```cpp
// 23.11.1. 类模板 unique_ptr
template <class T> struct default_delete<T>;
template <class T, class D = default_delete<T>> class unique_ptr;
template <class T, class D> class unique_ptr<T[], D>;

template <class T, class... Args>
unique_ptr<T> make_unique(Args&&... args);
template <class T>
unique_ptr<T> make_unique(size_t n);
template <class T, class... Args>
make_unique(Args&&... args) = delete;

template <class T, class D>
void swap(unique_ptr<T, D>& x, unique_ptr<T, D>& y) noexcept;

template <class T1, class D1, class T2, class D2>
bool operator==(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);
template <class T1, class D1, class T2, class D2>
bool operator!=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);
template <class T1, class D1, class T2, class D2>
bool operator<(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);
template <class T1, class D1, class T2, class D2>
bool operator<>(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);
template <class T1, class D1, class T2, class D2>
bool operator>(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);

template <class T, class D>
bool operator=(const unique_ptr<T, D>& x, const unique_ptr<T, D>& y) noexcept;
template <class T, class D>
bool operator=(nullptr_t, const unique_ptr<T, D>& x) noexcept;
template <class T, class D>
bool operator=(const unique_ptr<T, D>& x, nullptr_t) noexcept;
template <class T, class D>
bool operator!=(const unique_ptr<T, D>& x, nullptr_t);
template <class T, class D>
bool operator!=(nullptr_t, const unique_ptr<T, D>& x);
template <class T, class D>
bool operator!=(const unique_ptr<T, D>& x, const unique_ptr<T, D>& y);
template <class T, class D>
bool operator>(const unique_ptr<T, D>& x, nullptr_t);
template <class T, class D>
bool operator>(nullptr_t, const unique_ptr<T, D>& x);
template <class T, class D>
bool operator>(const unique_ptr<T, D>& x, const unique_ptr<T, D>& y);
template <class T, class D>
bool operator<=(const unique_ptr<T, D>& x, nullptr_t);
template <class T, class D>
bool operator<=(nullptr_t, const unique_ptr<T, D>& x);
template <class T, class D>
bool operator<=(const unique_ptr<T, D>& x, const unique_ptr<T, D>& y);
template <class T, class D>
bool operator>=(const unique_ptr<T, D>& x, nullptr_t);
template <class T, class D>
bool operator>=(nullptr_t, const unique_ptr<T, D>& x);
template <class T, class D>
bool operator>=(const unique_ptr<T, D>& x, const unique_ptr<T, D>& y);
template <class T, class D>
bool operator<(const unique_ptr<T, D>& x, nullptr_t);
template <class T, class D>
bool operator<(nullptr_t, const unique_ptr<T, D>& x);
template <class T, class D>
bool operator<(const unique_ptr<T, D>& x, const unique_ptr<T, D>& y);
template <class T, class D>
bool operator<=(const unique_ptr<T, D>& x, nullptr_t);
template <class T, class D>
bool operator<=(nullptr_t, const unique_ptr<T, D>& x);
template <class T, class D>
bool operator<=(const unique_ptr<T, D>& x, const unique_ptr<T, D>& y);

// 23.11.2. 类模板 shared_weak_ptr
class bad_weak_ptr;

// 23.11.2.2. 类模板 shared_ptr
template <class T>ptr_

// 23.11.2.6. shared_ptr 创建
template <class T, class... Args>
shared_ptr<T> make_shared(Args&&... args);
template <class T, class... Args>
shared_ptr<T> allocate(const T& a, Args&&... args) noexcept;

// 23.11.2.7. shared_ptr 比较
template <class T, class U>
bool operator=(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
template <class T, class U>
bool operator!=(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
template <class T, class U>
bool operator<(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
template <class T, class U>
bool operator>(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
template <class T, class U>
bool operator<=(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
template <class T, class U>
bool operator>=(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
template <class T>
bool operator==(nullptr_t, const shared_ptr<T>& x) noexcept;
template <class T>
bool operator==(const shared_ptr<T>& x, nullptr_t) noexcept;
template <class T>
bool operator==(nullptr_t, const shared_ptr<T>& x) noexcept;
template <class T>
bool operator!=(const shared_ptr<T>& x, nullptr_t);
template <class T>
bool operator!=(nullptr_t, const shared_ptr<T>& x);
template <class T, class U>
bool operator!=(const shared_ptr<T>& x, const shared_ptr<U>& y);
template <class T>
bool operator>(const shared_ptr<T>& x, nullptr_t);
template <class T>
bool operator>(nullptr_t, const shared_ptr<T>& x);
template <class T, class U>
bool operator>(const shared_ptr<T>& x, const shared_ptr<U>& y);
template <class T>
bool operator<=(const shared_ptr<T>& x, nullptr_t);
template <class T>
bool operator<=(nullptr_t, const shared_ptr<T>& x);
template <class T, class U>
bool operator<=(const shared_ptr<T>& x, const shared_ptr<U>& y);
template <class T>
bool operator>=(const shared_ptr<T>& x, nullptr_t);
template <class T>
bool operator>=(nullptr_t, const shared_ptr<T>& x);
template <class T, class U>
bool operator>=(const shared_ptr<T>& x, const shared_ptr<U>& y);
template <class T>
bool operator<(const shared_ptr<T>& x, nullptr_t);
template <class T>
bool operator<(nullptr_t, const shared_ptr<T>& x);
template <class T, class U>
bool operator<(const shared_ptr<T>& x, const shared_ptr<U>& y);
template <class T>
bool operator<=(const shared_ptr<T>& x, nullptr_t); // 此处原文重复，保留翻译逻辑

// 23.11.2.8. shared_ptr 算法
template <class T>
void swap(shared_ptr<T>& a, shared_ptr<T>& b) noexcept;

// 23.11.2.9. shared_ptr 转换
template <class T, class U>
shared_ptr<T> static_pointer_cast(const shared_ptr<U>& r);
template <class T, class U>
shared_ptr<T> dynamic_pointer_cast(const shared_ptr<U>& r);

template <class T, class U>
shared_ptr<T> const_pointer_cast(const shared_ptr<U>& r);
template <class T, class U>
shared_ptr<T> reinterpret_pointer_cast(const shared_ptr<U>& r);

// 23.11.2.10. shared_ptr 获取删除器
template <class D, class T>
D* delete_const(const shared_ptr<T>& p);

// 23.11.2.11. shared_ptr I/O
template <class E, class T>
basic_ostream<E>& operator<<(basic_ostream<E>& os, const shared_ptr<T>& p);

// 23.11.2.13. weak_ptr 创建
template <class T>
void swap(weak_ptr<T>& a, weak_ptr<T>& b) noexcept;

// 23.11.2.24. 类模板 owner_less
template <class T>
struct owner_less { void* =; };

// 23.11.2.25. 类模板 enable_shared_from_this
template <class T>
class enable_shared_from_this;

// 23.11.2.26. shared_ptr 原子访问
template <class T>
T atomic_load(const shared_ptr<T>& r);
template <class T>
T atomic_load_explicit(const shared_ptr<T>& r, memory_order order);
template <class T>
void atomic_store(shared_ptr<T>& r, const T& x);
template <class T>
void atomic_store_explicit(shared_ptr<T>& r, const T& x, memory_order order);
template <class T>
T atomic_exchange(shared_ptr<T>& r, const T& x);
template <class T>
T atomic_exchange_explicit(shared_ptr<T>& r, const T& x, memory_order order);
template <class T>
bool atomic_compare_exchange_weak(shared_ptr<T>& r, const T& expected, const T& x);
template <class T>
bool atomic_compare_exchange_weak(shared_ptr<T>& r, const T& expected, const T& x, memory_order order);
template <class T>
bool atomic_compare_exchange_strong(shared_ptr<T>& r, const T& expected, const T& x);
template <class T>
bool atomic_compare_exchange_strong(shared_ptr<T>& r, const T& expected, const T& x, memory_order order);

// 23.10.7, uses_allocator
template<class T, class Alloc>
inline constexpr bool uses_allocator<T, Alloc> = Alloc::value;

