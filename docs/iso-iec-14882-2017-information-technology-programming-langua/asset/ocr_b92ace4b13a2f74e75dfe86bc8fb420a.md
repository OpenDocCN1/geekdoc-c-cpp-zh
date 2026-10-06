# ISO/IEC 14882:2017(E)

```
template <class T, class D>
bool operator|=(nullptr_t, const unique_ptr<T, D& y) noexcept;
template <class T, class D>
bool operator<(const unique_ptr<T, D& x, nullptr_t);
template <class T, class D>
bool operator>=(nullptr_t, const unique_ptr<T, D& y);
template <class T, class D>
bool operator<(const unique_ptr<T, D& x, nullptr_t);
template <class T, class D>
bool operator<=(nullptr_t, const unique_ptr<T, D& y);
template <class T, class D>
bool operator>(const unique_ptr<T, D& x, nullptr_t);
template <class T, class D>
bool operator>=(const unique_ptr<T, D& x, nullptr_t);
template <class T, class D>
bool operator>=(const unique_ptr<T, D& x, nullptr_t);
template <class T, class D>
bool operator>=(nullptr_t, const unique_ptr<T, D& y));
```

# 23.11.1 Default deleters [unique_ptr.dltr]

# 23.11.1.1 In general [unique_ptr.dltr.general]

+   1 The class template default_delete serves as the default deleter (destruction policy) for the class template unique_ptr.

+   2 The template parameter T of default_delete may be an incomplete type.

```
23.11.1.2 default_delete [unique_ptr.dltfr.nft]
namespace std {
template <class U> struct default_delete {
    constexpr default_delete() noexcept = default;
t    template <class V> default_delete(const default_delete<V>&) noexcept;
    void operator()(U* const) const;
};
};
```

```
template <class U> default_delete(const default_delete<U>& other) noexcept = default;
```

+   1 Effects: Constructs a default_delete object from another default_delete<U> object.

+   2 Remarks: This constructor shall not participate in overload resolution U* is implicitly convertible to T.

```
void operator()(U* const) const;
```

+   3 Effects: Calls delete on ptr.

+   4 Remarks: If T is an incomplete type, the program is ill-formed.

# 23.11.1.3 default_delete<T[]> [unique_ptr.dltfr.nft]

```
namespace std {
template <class T> struct default_delete<T[]> {
    constexpr default_delete() noexcept = default;
template <class U> default_delete(const default_delete<U[]>&) noexcept = default;
template <class U> void operator()(U* ptr) const;
};
}
```

§ 23.11.1.3