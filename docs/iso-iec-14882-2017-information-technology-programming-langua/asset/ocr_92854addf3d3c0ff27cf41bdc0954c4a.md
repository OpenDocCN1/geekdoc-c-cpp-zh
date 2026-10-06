# ISO/IEC 14882:2017(E)

```
template <class T, class U> constexpr bool operator=(const optional<T>&, const U);
template <class T, class U> constexpr bool operator=(const U, const optional<T>);
template <class T, class U> constexpr bool operator<(const optional<U>, const optional<T>);
template <class T, class U> constexpr bool operator>(const optional<T>, const U&);
template <class T, class U> constexpr bool operator>(const U, const optional<T>&);
template <class T, class U> constexpr bool operator>(const optional<T>&, const U&);
```

```
// 23.6.9. specialized algorithms
```

```
template <class T>
void swap(optional<T>&, optional<T>&) noexcept(see below);

template <class T>
constexpr optional<T> <see below> make_optional(T&&);
template <class T, class Args...>
constexpr optional<T> make_optional(Args&&... args);
template <class T, class U, class Args...>
template <class T, class U, class Args...>
 make_optional(initializer_list<U>&&, Args&&... args);
```

```
// 23.6.10. hash support
```

```
template <class T>
template <class T> struct hash<optional<T>>
}
```

+   1 A program that necessitates the instantiation of optional for a reference type, or possibly cv-qualified types in_place_t or null_t is ill-formed.

# 23.6.3 Class template optional [optional|optional]

```
template <class T>
class optional {
public:
    using value_type = T;

    // 23.6.3.1, constructor
    constexpr optional() noexcept;
    constexpr optional(null_t) noexcept;
    constexpr optional(const optional<T>&);
    constexpr optional(optional<T>&&) noexcept(see below);
    template <class... class Args...>
    constexpr explicit optional(in_place_t, Args&&...);
t    template <class U, class Args...>
    constexpr explicit optional(in_place_t, initializer_list<U>&&, Args&&...);
    EXPLICIT constexpr optional(const U&);
    template <class U>
    EXPLICIT optional(const optional<U>&);
    template <class U>
    EXPLICIT optional(optional<U>&&);

    // 23.6.3.2, destructor
    ~optional();

    // 23.6.3.3, assignment
    optional& operator=(null_t) noexcept;
    optional& operator=(const optional<T>&);
```

§ 23.6.3

©ISO/IEC 2017 – All rights reserved

554