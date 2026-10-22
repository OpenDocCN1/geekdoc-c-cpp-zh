As with the improved version of `IsDefaultConstructibleT` for predicate traits above, we define the general case to be derived from `std::false_type`, because by default a type doesn’t have the member `size_type`.

The interesting feature here is the second template argument that defaults to the type of a helper `VoidT`. It enables us to provide partial specializations that use an arbitrary number of compile-time type constructs.

In this case, we need only one construct:

```
`decltype(T())` to check again whether the default constructor for T is valid. If, for a specific T, the construct is invalid, SFINAE this time causes the whole partial specialization to be discarded, and we fall back to the primary template. Otherwise, the partial specialization is valid and preferred.
```

In C++17, the C++ standard library introduced a type trait `std::void_t<>` that corresponds to the type `VoidT` introduced here. Before C++17, it might be helpful to define it ourselves as above or even in namespace `std` as follows:

[Click here to view code image](#)

```
```cpp
#include <type_traits>

#ifndef __cpp_lib_void_t
namespace std {
template<typename...> using void_t = void;
}
#endif
```
```

Starting with C++14, the C++ standardization committee has recommended that compilers and standard libraries indicate which parts of the standard they have implemented by defining agreed-upon *feature macros*. This is not a requirement for standard conformance, but implementers typically follow the recommendation to be helpful to their users. The macro `__cpp_lib_void_t` is the macro recommended to indicate that a library implements `std::void_t`, and thus our code above is made conditional on it.

Obviously, this way to define a type trait looks more condensed that the first approach to overload function templates. But it requires the ability to formulate the condition inside the declaration of a template parameter. Using a class template with function overloads enables us to use additional helper functions or helper types.

# 19.4.3 Using Generic Lambdas for SFINAE