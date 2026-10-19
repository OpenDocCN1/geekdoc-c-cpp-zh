
# 22.6.5.4 Members [priqueue.members]

```
void push(const value_type& x);
```

Effects: As if by:
    c.push_back(x);
    push_heap(c.begin(), c.end(), comp);

```
void push(value_type&& x);
```

Effects: As if by:
    c.push_back(std::move(x));
    push_heap(c.begin(), c.end(), comp);

```
template<class... Args> void emplace(Args&&... args);
```

Effects: As if by:
    c.emplace_back(std::forward<Args>(args)...);
    push_heap(c.begin(), c.end(), comp);

```
void pop();
```

Effects: As if by:
    pop_heap(c.begin(), c.end(), comp);
    c.pop_back();

# 22.6.5.5 Specialized algorithms [priqueue.special]

```
template<class T, class Container, class Compare>
    void swap(priority_queue<T, Container, Compare>& x,
              priority_queue<T, Container, Compare>& y) noexcept(noexcept(x.swap(y)));
```

Constraints: is_swappable_v<Container> is true and is_swappable_v<Compare> is true.

Effects: As if by x.swap(y).

# 22.6.6 Class template stack [stack]

# 22.6.6.1 General [stack.general]

Any sequence container supporting operations back(), push_back() and pop_back() can be used to instantiate stack. In particular, vector (22.3.11), list (22.3.10) and deque (22.3.8) can be used.

# 22.6.6.2 Definition [stack.defn]

```
namespace std {
    template<class T, class Container = deque<T>>
    class stack {
    public:
```

```
using value_type       = typename Container::value_type;
using reference        = typename Container::reference;
using const_reference  = typename Container::const_reference;
using size_type        = typename Container::size_type;
using container_type   = Container;

protected:
    Container c;

public:
    stack() : stack(Container()) {}
    explicit stack(const Container&);
    explicit stack(Container&&);
    template<class Alloc> explicit stack(const Alloc&);
    template<class Alloc> stack(const Container&, const Alloc&);
    template<class Alloc> stack(Container&&, const Alloc&);
    template<class Alloc> stack(const stack&, const Alloc&);
    template<class Alloc> stack(stack&&, const Alloc&);

    [[nodiscard]] bool empty() const       { return c.empty(); }
    size_type size() const                 { return c.size(); }
    reference top()                        { return c.back(); }
    const_reference top() const            { return c.back(); }
    void push(const value_type& x)         { c.push_back(x); }
    void push(value_type&& x)              { c.push_back(std::move(x)); }
    template<class... Args>
      decltype(auto) emplace(Args&&... args)
        { return c.emplace_back(std::forward<Args>(args)...); }
    void pop()                             { c.pop_back(); }
    void swap(stack& s) noexcept(is_nothrow_swappable_v<Container>)
        { using std::swap; swap(c, s.c); }
};

template<class Container>
stack(Container) -> stack<typename Container::value_type, Container>;

template<class Container, class Allocator>
stack(Container, Allocator) -> stack<typename Container::value_type, Container>;

template<class T, class Container, class Alloc>
struct uses_allocator<stack<T, Container>, Alloc>
    : uses_allocator<Container, Alloc>::type { };
```

# 22.6.6.3 Constructors

explicit stack(const Container& cont);

1  *Effects:* Initializes c with cont.

explicit stack(Container&& cont);

2  *Effects:* Initializes c with std::move(cont).

# 22.6.6.4 Constructors with allocators

1  If uses_allocator_v<container_type, Alloc> is false the constructors in this subclause shall not participate in overload resolution.

template<class Alloc> explicit stack(const Alloc& a);

2  *Effects:* Initializes c with a.

template<class Alloc> stack(const container_type& cont, const Alloc& a);

3  *Effects:* Initializes c with cont as the first argument and a as the second argument.

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

```
template<class ElementType, size_t Extent>
    inline constexpr bool ranges::enable_view<span<ElementType, Extent>> =
        Extent == 0 || Extent == dynamic_extent;
template<class ElementType, size_t Extent>
    inline constexpr bool ranges::enable_borrowed_range<span<ElementType, Extent>> = true;
```

```
// 22.7.3.8, views of object representation
```

```
template<class ElementType, size_t Extent>
    span<const byte, Extent == dynamic_extent ? dynamic_extent : sizeof(ElementType) * Extent>
        as_bytes(span<ElementType, Extent> s) noexcept;
```

```
template<class ElementType, size_t Extent>
    span<byte, Extent == dynamic_extent ? dynamic_extent : sizeof(ElementType) * Extent>
        as_writable_bytes(span<ElementType, Extent> s) noexcept;
}
```

# 22.7.3 Class template span [views.span]

# 22.7.3.1 Overview [span.overview]

1 A span is a view over a contiguous sequence of objects, the storage of which is owned by some other object.

2 All member functions of span have constant time complexity.

```
namespace std {
template<class ElementType, size_t Extent = dynamic_extent>
class span {
public:
    // constants and types
    using element_type = ElementType;
    using value_type = remove_cv_t<ElementType>;
    using size_type = size_t;
    using difference_type = ptrdiff_t;
    using pointer = element_type*;
    using const_pointer = const element_type*;
    using reference = element_type&;
    using const_reference = const element_type&;
    using iterator = implementation-defined;        // see 22.7.3.7
    using reverse_iterator = std::reverse_iterator<iterator>;
    static constexpr size_type extent = Extent;
```

```
// 22.7.3.2, constructors, copy, and assignment
```

```
constexpr span() noexcept;
template<class It>
    constexpr explicit(extent != dynamic_extent) span(It first, size_type count);
template<class It, class End>
    constexpr explicit(extent != dynamic_extent) span(It first, End last);
template<size_t N>
    constexpr span(type_identity_t<element_type> (&arr)[N]) noexcept;
template<class T, size_t N>
    constexpr span(array<T, N>& arr) noexcept;
template<class T, size_t N>
    constexpr span(const array<T, N>& arr) noexcept;
template<class R>
    constexpr explicit(extent != dynamic_extent) span(R&& r);
constexpr span(const span& other) noexcept = default;
template<class OtherElementType, size_t OtherExtent>
    constexpr explicit(see below) span(const span<OtherElementType, OtherExtent>& s) noexcept;

~span() noexcept = default;

constexpr span& operator=(const span& other) noexcept = default;
```

```
// 22.7.3.4, subviews
template<size_t Count>
    constexpr span<element_type, Count> first() const;
```
