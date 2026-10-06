# ISO/IEC 14882:2017(E)

```
template <class T, class Allocator>
void swap(deq<T, Allocator>& x, deq<T, Allocator>& y)
noexcept(noexcept(x.swap(y)));
```

```
namespace pr {
    template <class T>
    using deque = std::deque<T, polymorphic_allocator<T>>
}
```

# 26.3.4 Header <forward_list> synopsis

```
#include <initializer_list>

namespace std {
    // 36.3.9.
    template <class T, Allocator = allocator<T>> class forward_list {
    template <class T, Allocator>
    forward_list(const forward_list<T, Allocator>& x, const Allocator& x = Allocator());
    template <class T, Allocator>
    bool operator==(const forward_list<T, Allocator>& x, const forward_list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator=(const forward_list<T, Allocator>& x, const forward_list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator!=(const forward_list<T, Allocator>& x, const forward_list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator<=(const forward_list<T, Allocator>& x, const forward_list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator>=(const forward_list<T, Allocator>& x, const forward_list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator<=(const forward_list<T, Allocator>& x, const forward_list<T, Allocator>& y);
    template <class T, Allocator>
    void swap(forward_list<T, Allocator>& x, forward_list<T, Allocator>& y)
    noexcept(noexcept(x.swap(y)));
```

```
namespace pr {
    template <class T>
    using forward_list = std::forward_list<T, polymorphic_allocator<T>>
}
```

# 26.3.5 Header <initializer_list> synopsis

```
#include <initializer_list>

namespace std {
    // 36.3.10.
    template <class T, Allocator = allocator<T>> class list {
    template <class T, Allocator>
    list(const list<T, Allocator>& x, const Allocator& x = Allocator());
    template <class T, Allocator>
    bool operator==(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator!=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator<=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator>=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator!=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator<=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator>=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator<=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    bool operator>=(const list<T, Allocator>& x, const list<T, Allocator>& y);
    template <class T, Allocator>
    list<T, Allocator>
```