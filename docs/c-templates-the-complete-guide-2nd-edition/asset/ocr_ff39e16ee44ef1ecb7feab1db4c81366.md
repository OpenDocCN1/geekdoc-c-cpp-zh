```
template<...> static std::true_type test(void*);  // checking test()
template<...> static std::false_type test(...);  // fallback
```