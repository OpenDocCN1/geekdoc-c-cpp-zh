# ISO/IEC 14882:2017(E)

```
pointer() const noexcept;
6   Returns: The stored pointer.

deleter_type& get_deleter() noexcept;
const deleter_type& get_deleter() const noexcept;
7   Returns: A reference to the stored pointer.
explicit operator bool() const noexcept;
8   Returns: get() != nullptr;
```

# 23.11.1.2 unique_ptr modifiers [unique.ptr.single.modifiers]

```
pointer release() noexcept;
1   Postconditions: get() == nullptr;
2   Returns: The value get() had at the start of the release.

void reset(pointer* p = nullptr) noexcept
3   Requires: The expression get_deleter()get() shall be formed, shall have well-defined behavior, and shall not throw exceptions.
4   Effects: Assigns to the stored pointer, and then if only the old value of the stored pointer, old_p, was not equal to nullptr, call get_deleter(old_p). [Note: The order of operations is significant because the call to get_deleter() may destroy this. -- end note];
5   Postconditions: get() == p. [Note: The postcondition does not hold if the call to get_deleter() destroys this-this-get() is no longer a valid expression. -- end note];

void swap(unique_ptr& u) noexcept
6   Requires: get_deleter() shall be swappable [20.5.3.2] and shall not throw an exception under swap.
7   Effects: Invokes swap on the stored pointers and on the stored deleters of *this and u.
```

# 23.11.1.3 unique_ptr for array objects with a runtime length [unique.ptr.runtime]

```
namespace std {
template<class T, class D> class unique_ptr<T[], D> = {
public:
    using see below;
    using element_type = T;
    using deleter_type = D;

// 23.11.1.3.1. constructors
constexpr unique_ptr() noexcept;
template<class U> constexpr unique_ptr(U p) noexcept;
template<class U> unique_ptr(U p, see below d) noexcept;
template<class U> unique_ptr(U p, see below d) noexcept;
unique_ptr(unique_ptr&& u, U p) noexcept;
template<class U, class E> constexpr unique_ptr(unique_ptr<U, E>, E&& u) noexcept;
constexpr unique_ptr(nullptr_t) noexcept;

    ~destructor();n    ~unique_ptr();
```