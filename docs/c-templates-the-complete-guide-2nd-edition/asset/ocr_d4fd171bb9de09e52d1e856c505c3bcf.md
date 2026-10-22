traits can be implement with just one declaration. For example, testing for access to a member named first, is rather clean (see Section 19.6.4 on page 438 for the complete example): Click here to view code image

```
constexpr auto hasFirst
= isValid([](auto x) -> decltype((void)valueT(x).first) {
});
```

# 19.4.4 SFINAE-Friendly Traits

In general, a type trait should be able to answer a particular query without causing the program to become ill-formed. SFINAE-based traits address this problem by carefully trapping potential problems within a SFINAE context, turning those would-be errors into negative results.

However, some traits presented thus far (such as the PlusResultT trait described in Section 19.3.4 on page 413) do not behave well in the presence of errors. Recall the definition of PlusResultT from that section: Click here to view code image

traits/plus2.hpp

```
#include <utility>

template<typename T1, typename T2>
struct PlusResultT {
using Type = decltype(std::declval<T1>() + std::declval<T2>());
};
```

```
template<typename T1, typename T2>
using PlusResult = typename PlusResultT<T1, T2>::Type; In this definition, the + is used in a context that is not protected by SFINAE. Therefore, if a program attempts to evaluate PlusResultT for types that do not have a suitable + operator, the evaluation of PlusResultT itself will cause the program to become ill-formed, as in the following attempt to declare the return type of adding arrays of unrelated types A and B:20
```

Click here to view code image

```
template<typename T>
class Array {
...
};
```

```
// declare + for arrays of different element types:
```