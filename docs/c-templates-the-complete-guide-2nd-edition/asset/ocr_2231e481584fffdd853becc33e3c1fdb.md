```
```cpp
using Result = Accumulate<SignedIntegralTypes, PushFrontT, Typelist<>>;
// produces TypeList<long long, long, int, short, signed char>
```
```