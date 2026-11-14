```
template <bool b, class T, class F>
using conditional_t = typename conditional<b, T, F>::type;
```