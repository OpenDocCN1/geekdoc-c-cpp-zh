# ISO/IEC 14882:2017(E)

```
// 2.37.10, specialized algorithms
template <class... Types>
void swap(variant<Types...)&, variant<Types...)&) noexcept(see below);

// 2.37.11, class bad_variant_access
class bad_variant_access;

// 2.37.12, hash_support
template <class> struct hash;
template <class... Types> struct hash<variant<Types...>>;
template <> struct hash<monostate>;

// 2.37.13, allocator-related
template <class T, class Alloc> struct uses_allocator;
template <class... Types, class Alloc> uses_allocator<variant<Types...>, Alloc>;
```

# 23.7.3 Class template variant [variant.variant]

§ 23.7.3 ISO/IEC 2017 - All rights reserved 569