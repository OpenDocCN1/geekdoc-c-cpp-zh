# ISO/IEC 14882:2017(E)

# 23.6.10 Hash support [optional.hash]

template <class T> struct optional<T>;nThe specialization hash<optional<T>> is enabled (23.14.15) if and only if `remove_const_t<T>` is enabled. When, for an object of type `optional<T>`, if bool(o) == true, then `hash<optional<T>>()(o)` will evaluate to the same value as `hash<remove_const_t<T>>`; otherwise it evaluates to an unspecified value. The member functions are guaranteed to be noexcept.

# 23.7 Variants [variant]

+   23.7.1 In general [variant.general]
A variant object holds and manages the lifetime of a variant. If a variant holds a value, that variant's type has been one of the template types given by variant. These template arguments are alternatives.

# 23.7.2 Header <variant> synopsis [variant.syn]

```
namespace std {
  // variant. class template
  template <... Types>
  class variant {
    // variant. helper classes
    template <T> struct variant_size; // not defined
    template <T> struct variant_size<const T>;
    template <T> struct variant_size<const volatile T>;
    template <T>
    inline constexpr size_t variant_v = variant_size<T>::value;

    template <... Types>
    struct variant_size<Types...>;

    template <size_t I, class T> struct variant_alternative; // not defined
    template <size_t I, class T> struct variant_alternative<I, const T>;
    template <size_t I, class T> struct variant_alternative<I, volatile T>;
    template <size_t I, class T> struct variant_alternative<I, const volatile T>;
    template <size_t I, class T>
    using variant_alternative_t = typename variant_alternative<I, T>::type;

    template <size_t I, class... Types>
    struct variant_alternative<Types...>;

    inline constexpr size_t variant_npos = -1;

    // variant.7.5, value access
    template <... Types>
    class variant {
    bool holds_alternative(const variant<Types...>&...) noexcept;

    template <size_t I, class... Types>
    constexpr variant_alternative_t<I, Types...>& get(const variant<Types...>&...) const noexcept;
    template <size_t I, class... Types>
    constexpr variant_alternative_t<I, Types...>& get(const variant<Types...>&...) const noexcept;
    template <size_t I, class... Types>
    constexpr variant_alternative_t<I, Types...>& get(const variant<Types...>&...) const noexcept;
};
```