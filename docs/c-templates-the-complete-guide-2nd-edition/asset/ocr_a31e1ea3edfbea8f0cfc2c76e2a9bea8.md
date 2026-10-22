TryEquals class template that can either invoke == on the given type (when it’s available) or throw an exception if no suitable == exists: Click here to view code image

# bridge/tryequals.hpp

```
#include <exception>
#include "isequalitycomparable.hpp"

template<typename T,
bool EqComparable = IsEqualityComparable<T>::value>
struct TryEquals
{
static bool equals(T const& x1, T const& x2) {
return x1 == x2;
}
};

class NotEqualityComparable : public std::exception
{
};

template<typename T>
struct TryEquals<T, false>
{
static bool equals(T const& x1, T const& x2) {
throw NotEqualityComparable();
}
};
```

Finally, by using TryEquals within our implementation of SpecificFunctorBridge, we are able to provide support for == within FunctionPtr whenever the stored function object types match and the function object supports ==: Click here to view code image

```
virtual bool equals(FunctorBridge<R, Args...> const* fb) const override
{
if (auto specFb = dynamic_cast<SpecificFunctorBridge const*>(fb)) {
return TryEquals<Functor>::equals(functor, specFb->functor);
}
//functors with different types are never equal:
return false;
}
```

# 22.6 Performance Considerations