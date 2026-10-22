```
#include "accumtraits3.hpp"

template<typename T>
auto accum (T const* beg, T const* end)
{
// return type is traits of the element type
using AccT = typename AccumulationTraits<T>::AccT;
AccT total = AccumulationTraits<T>::zero; // init total by trait value
while (beg != end) {
total += *beg;
++beg;
}
return total;
}

#endif // ACCUM_HPP
```

In this code, the initialization of the accumulation variable remains straightforward: Click here to view code image

```
AccT total = AccumulationTraits<T>::zero;
```

A drawback of this formulation is that C++ allows us to initialize a static constant data member inside its class only if it has an integral or enumeration type.

constexpr static data members are slightly more general, allowing floating-point types as well as other literal types: Click here to view code image

```
template<>
struct AccumulationTraits<float> {
using AccT = float;
static constexpr float zero = 0.0f;
};
```

However, neither const nor constexpr permit nonliteral types to be initialized this way. For example, a user-defined arbitrary-precision BigInt type might not be a literal type, because typically it has to allocate components on the heap, which usually precludes it from being a literal type, or just because the required constructor is not constexpr. The following specialization is then an error: Click here to view code image

```
class BigInt {
BigInt(long long);
...};
...
template<>
struct AccumulationTraits<BigInt> {
```