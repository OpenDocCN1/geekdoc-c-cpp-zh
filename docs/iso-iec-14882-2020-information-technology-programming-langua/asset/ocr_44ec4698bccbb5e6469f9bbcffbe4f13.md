# 22.6.6.5 Operators [stack.ops]

```
template<class Alloc> stack(container_type&& cont, const Alloc& a);
```

Effects: Initializes c with std::move(cont) as the first argument and a as the second argument.

```
template<class Alloc> stack(const stack& s, const Alloc& a);
```

Effects: Initializes c with s.c as the first argument and a as the second argument.

```
template<class Alloc> stack(stack&& s, const Alloc& a);
```

Effects: Initializes c with std::move(s.c) as the first argument and a as the second argument.

```
template<class T, class Container>
  bool operator==(const stack<T, Container>& x, const stack<T, Container>& y);
```

Returns: x.c == y.c.

```
template<class T, class Container>
  bool operator!=(const stack<T, Container>& x, const stack<T, Container>& y);
```

Returns: x.c != y.c.

```
template<class T, class Container>
  bool operator< (const stack<T, Container>& x, const stack<T, Container>& y);
```

Returns: x.c < y.c.

```
template<class T, class Container>
  bool operator> (const stack<T, Container>& x, const stack<T, Container>& y);
```

Returns: x.c > y.c.

```
template<class T, class Container>
  bool operator<=(const stack<T, Container>& x, const stack<T, Container>& y);
```

Returns: x.c <= y.c.

```
template<class T, class Container>
  bool operator>=(const stack<T, Container>& x, const stack<T, Container>& y);
```

Returns: x.c >= y.c.

```
template<class T, three_way_comparable Container>
  compare_three_way_result_t<Container>
    operator<=>(const stack<T, Container>& x, const stack<T, Container>& y);
```

Returns: x.c <=> y.c.

# 22.6.6.6 Specialized algorithms [stack.special]

```
template<class T, class Container>
  void swap(stack<T, Container>& x, stack<T, Container>& y) noexcept(noexcept(x.swap(y)));
```

Constraints: is_swappable_v<Container> is true.

Effects: As if by x.swap(y).

# 22.7 Views [views]

# 22.7.1 General [views.general]

The header <span> defines the view span.

# 22.7.2 Header <span> synopsis [span.syn]

```
namespace std {
  // constants
  inline constexpr size_t dynamic_extent = numeric_limits<size_t>::max();

  // 22.7.3, class template span
  template<class ElementType, size_t Extent = dynamic_extent>
    class span;
```