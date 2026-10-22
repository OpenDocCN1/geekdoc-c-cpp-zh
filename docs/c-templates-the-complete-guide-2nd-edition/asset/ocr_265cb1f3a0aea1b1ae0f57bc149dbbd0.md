enumeration types. We tackle these cases in the following sections.
The C++ standard library provides the trait std::is_function<>, which is described in Section D.2.1 on page 706.

# 19.8.4 Determining Class Types

Unlike the other compound types we have handled so far, we have no partial specialization patterns that match class types specifically. Nor is it feasible to enumerate all class types, as it is for fundamental types. Instead, we need to use an indirect method to identify class types, by coming up with some kind of type or expression that is valid for all class types (and not other type). With that type or expression, we can apply the SFINAE trait techniques discussed in Section 19.4 on page 416.

The most convenient property of class types to utilize in this case is that only class types can be used as the basis of pointer-to-member types. That is, in a type construct of the form X Y::*, Y can only be a class type. The following formulation of IsClassT<> exploits this property (and picks int arbitrarily for type X): Click here to view code image

```
traits/isclass.hpp
#include <type_traits>

template<typename T, typename = std::void_t<>>
struct IsClassT : std::false_type { //primary template: by default no class
};

template<typename T>
struct IsClassT<T, std::void_t<int T::*>> // classes can have pointer-to-member
: std::true_type {
};
```

The C++ language specifies that the type of a lambda expression is a “unique, unnamed non-union class type.” For this reason, lambda expressions yield true when examining whether they are class type objects: Click here to view code image

```
auto l = []{};
static_assert<IsClassT<decltype(l)>::value, "">; //succeeds
```