# ISO/IEC 14882:2017(E)

```
template <class T>
bool atomic_compare_exchange_strong_explicit(
shared_ptr<T>* p, shared_ptr<T>* v, shared_ptr<T>* w,
memory_order success, memory_order failure);
```

+   31 Requires: p shall not be null and shall not be null. The failure shall not be memory_order_release not memory_order_ac_rel.

+   32 Effects: If p is equivalent to v, assigns v to *p and synchronization semantics corresponding to the value of success, otherwise assigns v to *p and synchronization semantics corresponding to the value of failure.

+   33 Returns: true if p was equivalent to v, false otherwise.

+   34 Throws: Nothing.
35 Remarks: Two shared_ptr objects are equivalent if they share the same pointer value and ownership. The weak from may fail spuriously. See 32.6.1.

# 23.11.2.7 Smart pointer hash support

```
template <class T, class D> struct hash_unique_ptr<T, D>;nLet UP be unique_ptr<T>; the specialization hash<UP> is enabled (23.14.15) if and only hasype UP = UP::pointer is enabled. For an object p of type UP, hash<UP>(p) shall evaluate to the same value as hash<typename UP::pointer>(p.get()). The member functions of UP are not guaranteed to be noexcept.
template <class T, class D> struct hash_shared_ptr<T>>;
```

+   2 For an object p of shared_ptr<T>, hash<shared_ptr<T>>(p) shall evaluate to the same value as hash<typename T::element_type>(p.get()).

# 23.12 Memory resources

# 23.12.1 Header <memory_resource> synopsis

```
namespace std::{
// 23.12.1 class memory_resource
class memory_resource;

bool operator===(const memory_resource& a, const memory_resource& b) noexcept;
bool operator!=(const memory_resource& a, const memory_resource& b) noexcept;
```

```
// 23.12.3 class polymorphic_allocator
template <class T1, class T2>
bool operator===(const polymorphic_allocator<T1>& a,
               const polymorphic_allocator<T2>& b) noexcept;
template <class T1, class T2>
bool operator!=(const polymorphic_allocator<T1>& a,
               const polymorphic_allocator<T2>& b) noexcept;
```

```
// 23.12.4. global memory resources
memory_resource* new_delete_resource() noexcept;
memory_resource* new_memory_resource() noexcept;
memory_resource* set_default_resource(memory_resource* r) noexcept;
memory_resource* get_default_resource() noexcept;
```