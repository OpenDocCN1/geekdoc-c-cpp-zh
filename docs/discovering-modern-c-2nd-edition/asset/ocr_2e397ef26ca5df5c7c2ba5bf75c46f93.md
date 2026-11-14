```
template <bool Cond, typename T = void>
using enable_if_t = typename enable_if<Cond, T>::type;
```