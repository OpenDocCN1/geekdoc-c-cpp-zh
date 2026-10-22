```
```cpp
auto ic = is_const<MyType>();                         // object of trait type
cout << is_same<decltype(ic), is_const<int>>::value << '\n';  // true
cout << ic() << '\n';                                  // function call (prints false)

static constexpr auto mytypeIsConst = is_const<MyType>{};
if constexpr(mytypeIsConst) {             // compile-time check since C++17 => false
    ...                                     // discarded statement
}
static_assert(!std::is_const<MyType>{}, "MyType should not be const");
}
```
```