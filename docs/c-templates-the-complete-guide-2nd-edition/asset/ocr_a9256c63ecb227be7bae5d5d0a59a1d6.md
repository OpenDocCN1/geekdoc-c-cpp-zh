```
#include <typeinfo>
#include <type_traits>
#include "decay.hpp"

template<typename T>
void printDecayedType()
{
using A = typename DecayT<T>::Type;
std::cout << "Parameter type: " << typeid(A).name() << '\n';
std::cout << "- is int: " << std::is_same<A,int>::value << '\n';
std::cout << "- is const: " << std::is_const<A>::value << '\n';
std::cout << "- is pointer: " << std::is_pointer<A>::value << '\n';
}

int main()
{
printDecayedType<int>();
printDecayedType<int const>();
printDecayedType<int[7]>();
printDecayedType<int(int)>();
}
```

As usual, we provide a convenience alias template: Click here to view code image

```
template typename T>
using Decay = typename DecayT<T>::Type; As written, the C++ standard library also provides a corresponding type traits std::decay<>, which is described in Section D.4 on page 731.
```

# 19.3.3 Predicate Traits

So far we have studied and developed type functions of a single type: Given one type, provide other related types or constants. In general, however, we can develop type functions that depend on multiple arguments. This also leads to a special form of type traits, type predicates (type functions yielding a Boolean value).

# IsSameT

The IsSameT trait yields whether two types are equal: Click here to view code image

*traits/issame0.hpp*