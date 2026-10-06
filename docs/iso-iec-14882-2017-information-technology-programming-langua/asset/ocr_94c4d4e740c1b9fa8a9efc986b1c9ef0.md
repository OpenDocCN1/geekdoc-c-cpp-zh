# ISO/IEC 14882:2017(E)

template<class Alloc> stack(const Alloc& s, const Alloc& a);

Effects: Initializes c with std::move(s.c) as the first argument and as the second argument.

# 26.6.6.4 stack operators [stack.ops]

```
template<class T, class Container>
bool operator==(const stack<T, Container>& x, const stack<T, Container>& y);
Returns: x.c == y.c;
```

```
template<class T, class Container>
bool operator!=(const stack<T, Container>& x, const stack<T, Container>& y);
Returns: x.c != y.c;
```

```
template<class T, class Container>
bool operator<(const stack<T, Container>& x, const stack<T, Container>& y);
Returns: x.c < y.c;
```

```
template<class T, class Container>
bool operator<=(const stack<T, Container>& x, const stack<T, Container>& y);
Returns: x.c <= y.c;
```

```
template<class T, class Container>
bool operator>=(const stack<T, Container>& x, const stack<T, Container>& y);
Returns: x.c >= y.c;
```

# 26.6.6.5 stack specialized algorithms [stack.special]

```
template<class T, class Container>
void swap(stack<T, Container>& x, stack<Container>& y) noexcept(x.swap(y));
```

Remarks: This function shall not participate in overload resolution unless is_swappable_v<Container> is true.

Effects: As if by x.swap(y).