```
template<typename... Ts, Ts... vals> struct StaticValues {};
// ERROR: Ts cannot be expanded in its own parameter list
```