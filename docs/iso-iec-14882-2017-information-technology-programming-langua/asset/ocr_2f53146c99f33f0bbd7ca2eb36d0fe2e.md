# ISO/IEC 14882:2017(E)

# 23.6 Optional objects [optional]

# 23.6.1 In general [optional.general]

This subclass describes class template that represents optional objects. An optional object is an object that contains the storage for another object manages the lifetime of this contained object, if any. The contained object may be initialized after the optional object has been initialized, and may be destroyed before the optional object has destroyed. The initialization state of the contained object is tracked by the optional object.

# 23.6.2 Header <optional> synopsis [optional.syn]

```
namespace std {
// 23.6.3. class optional
template <class T>
class optional;

// 23.6.4. no-value state indicator
struct nullopt_t (see below);
inline const nullopt_t nullopt(specified);

// 23.6.5. class bad_optional_access
class bad_optional_access;

// 23.6.6. relational operators
template <class T, class U>
constexpr bool operator==(const optional<T>&, const optional<U>);
template <class T, class U>
constexpr bool operator!=(const optional<T>&, const optional<U>);
template <class T, class U>
constexpr bool operator>(const optional<T>&, const optional<U>);
template <class T, class U>
constexpr bool operator<=(const optional<T>&, const optional<U>);
template <class T, class U>
constexpr bool operator>=(const optional<T>&, const optional<U>);
template <class T, class U>
constexpr bool operator>(const optional<T>&, const optional<U>);
```

```
// 23.6.7. comparison with nullopt
template <class T>
constexpr bool operator==(const optional<T>&, nullopt_t) noexcept;
template <class T>
constexpr bool operator!=(const optional<T>&, nullopt_t) noexcept;
template <class T>
constexpr bool operator<>(const optional<T>&, nullopt_t) noexcept;
template <class T>
constexpr bool operator<=(const optional<T>&, nullopt_t) noexcept;
template <class T>
constexpr bool operator>(const optional<T>&, nullopt_t) noexcept;
template <class T>
constexpr bool operator>=(const optional<T>&, nullopt_t) noexcept;
template <class T>
constexpr bool operator==(const optional<T>&, nullopt_t) noexcept;
template <class T>
constexpr bool operator!=(const optional<T>&, nullopt_t) noexcept;
```

```
// 23.6.8. comparison with T
template <class T, class U>
constexpr bool operator==(const optional<T>&, const optional<U>);
template <class T, class U>
constexpr bool operator!=(const optional<U>, const optional<U>);
template <class T, class U>
constexpr bool operator<=(const optional<T>, const optional<U>);
template <class T, class U>
constexpr bool operator>=(const optional<U>, const optional<U>);
```