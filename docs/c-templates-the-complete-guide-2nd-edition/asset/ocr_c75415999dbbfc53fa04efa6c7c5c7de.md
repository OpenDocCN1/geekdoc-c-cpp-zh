Here, the operator version of `noexcept` is used, which determines whether an expression is non-throwing. Because the result is a Boolean value, we can pass it directly to define the base class, `std::bool_constant<>`, which is used to define `std::true_type` and `std::false_type` (see Section 19.3.3 on page 411).

However, this implementation should be improved because it is not SFINAE-friendly (see Section 19.4.4 on page 424): If the trait is instantiated with a type that does not have a usable move or copy constructor—making the expression `T(std::declval<T&&>())` invalid—the entire program is ill-formed:

![](bbox=[0.117, 0.288, 0.398, 0.307])

```
class E {
public:
  E(E&&) = delete;
};
...
std::cout << IsNothrowMoveConstructibleT<E>::value; // compile-time
ERROR
```

Instead of aborting the compilation, the type trait should yield a value of `false`.

As discussed in Section 19.4.4 on page 424, we have to check whether the expression computing the result is valid before it is evaluated. Here, we have to find out whether move construction is valid before checking whether it is `noexcept`. Thus, we revise the first version of the trait by adding a template parameter that defaults to `void` and a partial that uses `std::void_t` for that parameter with an argument that is valid only if move construction is valid:

![](bbox=[0.117, 0.602, 0.398, 0.621])

```
traits/isnothrowmoveconstructible2.hpp

#include <utility> // for declval
#include <type_traits> // for true_type, false_type, and
                       // bool_constant<>

// primary template:
template<typename T, typename = std::void_t<>>
struct IsNothrowMoveConstructibleT : std::false_type
{
};

// partial specialization (may be SFINAE’d away):
template<typename T>
struct IsNothrowMoveConstructibleT
<T, std::void_t<decltype(T(std::declval<T>()))>>
```