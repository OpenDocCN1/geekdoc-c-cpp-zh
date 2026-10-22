```
template<typename T>
using RemoveCV = RemoveConst<RemoveVolatile<T>>;
```