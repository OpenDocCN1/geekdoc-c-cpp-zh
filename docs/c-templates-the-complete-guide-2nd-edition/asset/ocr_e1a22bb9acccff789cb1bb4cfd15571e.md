```
is_const<int* const>::value      // true
is_const<int const*>::value     // false
is_const<int const&>::value     // false
```