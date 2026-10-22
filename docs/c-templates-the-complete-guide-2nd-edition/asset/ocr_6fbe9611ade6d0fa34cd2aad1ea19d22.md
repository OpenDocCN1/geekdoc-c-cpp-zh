# traits/removeconst.hpp

```
template<typename T>
struct RemoveConstT {
using Type = T;
};
```

```
template<typename T>
struct RemoveConstT<T const> {
using Type = T;
};
```

```
template<typename T>
using RemoveConst = typename RemoveConstT<T>::Type; Moreover,
transformation traits can be composed, such as creating a RemoveCVT
trait that removes both const and volatile: Click here to view code image
```

# traits/removecv.hpp

```
#include "removeconst.hpp"
#include "removevolatile.hpp"
```

```
template<typename T>
struct RemoveCVT : RemoveConstT<typename RemoveVolatileT<T>::Type> {
};
```

template<typename T>
using RemoveCV = typename RemoveCVT<T>::Type; There are two things to note with the definition of RemoveCVT. First, it is making use of both RemoveConstT and the related RemoveVolatileT, first removing the volatile (if present) and then passing the resulting type to RemoveConstT.⁸ Second, it is using metafunction forwarding to inherit the Type member from RemoveConstT rather than declaring its own Type member that is identical to the one in the RemoveConstT specialization. Here, metafunction forwarding is used simply to reduce the amount of typing in the definition of RemoveCVT. However, metafunction forwarding is also useful when the metafunction is not defined for all inputs, a technique that will be discussed further in Section 19.4 on page 416.

The convenience alias template RemoveCV could be simplified to Click here to view code image

```
template<typename T>
using RemoveCV = RemoveConst<RemoveVolatile<T>>; Again, this works only if RemoveCVT is not specialized. Unlike in the case of AddLValueReference and AddRValueReference, we cannot think of any reasons for such specializations.
```

The C++ standard library also provides corresponding type traits