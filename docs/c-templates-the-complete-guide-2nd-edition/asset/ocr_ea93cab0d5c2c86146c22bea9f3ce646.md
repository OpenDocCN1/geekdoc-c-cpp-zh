```
constexpr auto isDefaultConstructible
= isValid([](auto x) -> decltype((void)decltype(valueT(x))()) {
});
```