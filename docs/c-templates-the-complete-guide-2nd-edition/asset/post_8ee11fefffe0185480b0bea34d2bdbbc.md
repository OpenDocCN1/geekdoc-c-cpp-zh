
## 19.4.4 SFINAE-Friendly Traits

Traits can be implemented with just one declaration. For example, testing for access to a member named `first` is rather clean (see Section 19.6.4 on page 438 for the complete example):

```cpp
constexpr auto hasFirst
    = isValid([](auto x) -> decltype((void)valueT(x).first) {
    });
```

In general, a type trait should be able to answer a particular query without causing the program to become ill-formed. SFINAE-based traits address this problem by carefully trapping potential problems within a SFINAE context, turning those would-be errors into negative results.

However, some traits presented thus far (such as the `PlusResultT` trait described in Section 19.3.4 on page 413) do not behave well in the presence of errors. Recall the definition of `PlusResultT` from that section:

`traits/plus2.hpp`

```cpp
#include <utility>

template<typename T1, typename T2>
struct PlusResultT {
    using Type = decltype(std::declval<T1>() + std::declval<T2>());
};
```

```cpp
template<typename T1, typename T2>
using PlusResult = typename PlusResultT<T1, T2>::Type;
```

In this definition, the `+` is used in a context that is not protected by SFINAE. Therefore, if a program attempts to evaluate `PlusResultT` for types that do not have a suitable `+` operator, the evaluation of `PlusResultT` itself will cause the program to become ill-formed, as in the following attempt to declare the return type of adding arrays of unrelated types `A` and `B`:20

```cpp
template<typename T>
class Array {
    ...
};
```

```cpp
// declare + for arrays of different element types:
```

Here, the type computation happens during template argument substitution, and SFINAE does not protect us from attempts to form invalid types or expressions there. Instead of just discarding the function template candidate, an error is issued right away because we try to call `operator+` for two elements of types `A` and `B` inside `PlusResultT<>`:

```cpp
template<typename T1, typename T2>
struct PlusResultT {
    using Type = decltype(std::declval<T1>() + std::declval<T2>());
};
```

To solve this problem, we have to make the `PlusResultT` SFINAE-friendly, which means to make it more resilient by giving it a suitable definition even when its `decltype` expression is ill-formed.

Following the example of `HasLessT` described in the previous section, we define a `HasPlusT` trait that allows us to detect whether there is a suitable `+` operation for the given types:

`traits/hasplus.hpp`

```cpp
#include <utility>        // for declval
#include <type_traits>    // for true_type, false_type, and void_t

// primary template:
template<typename, typename, typename = std::void_t<>>
struct HasPlusT : std::false_type
{};

// partial specialization (may be SFINAE'd away):
template<typename T1, typename T2>
struct HasPlusT<T1, T2, std::void_t<decltype(std::declval<T1>() + std::declval<T2>())>>
: std::true_type
{};
```

If it yields a true result, `PlusResultT` can use the existing implementation. Otherwise, `PlusResultT` needs a safe default. The best default for a trait that has no meaningful result for a set of template arguments is to not provide any member `Type` at all. That way, if the trait is used within a SFINAE context—such as the return type of the array `operator+` template above—the missing member `Type` will make template argument deduction fail, which is precisely the behavior desired for the array `operator+` template.

The following implementation of `PlusResultT` provides this behavior:

`traits/plus3.hpp`

```cpp
#include "hasplus.hpp"

template<typename T1, typename T2, bool = HasPlusT<T1, T2>::value>
struct PlusResultT { // primary template, used when HasPlusT yields true
    using Type = decltype(std::declval<T1>() + std::declval<T2>());
};

template<typename T1, typename T2>
struct PlusResultT<T1, T2, false> { // partial specialization, used otherwise
};
```

In this version of `PlusResultT`, we add a template parameter with a default argument that determines if the first two parameters support addition as determined by our `HasPlusT` trait above. We then partially specialize `PlusResultT` for `false` values of that extra parameter, and our partial specialization definition has no members at all, avoiding the problems we described. For cases where addition is supported, the default argument evaluates to `true` and the primary template is selected, with our existing definition of the `Type` member. Thus, we fulfill the contract that `PlusResultT` provide the result type only if in fact the `+` operation is well-formed. (Note that the added template parameter should never have an explicit template argument.) Consider again the addition of `Array<A>` and `Array<B>`: With our latest implementation of the `PlusResultT` template, the instantiation of `PlusResultT<A, B>` will not have a `Type` member, because `A` and `B` values are not addable. Therefore, the result type of the array `operator+` template is invalid, and SFINAE will eliminate the function template from consideration. The overloaded `operator+` that is specific to `Array<A>` and `Array<B>` will therefore be chosen.

As a general design principle, a trait template should never fail at instantiation time if given reasonable template arguments as inputs. And the general approach is often to perform the corresponding check twice:

1. Once to find out whether the operation is valid
2. Once to compute its result

We saw that already with `PlusResultT`, where we call `HasPlusT<>` to find out whether the call of `operator+` in `PlusResultT` is valid.

Let’s apply this principle to `ElementT` as introduced in Section 19.3.1 on page 401: It produces an element type from a container type. Again, since the answer relies on a (container) type having a member type `value_type`, the primary template should attempt to define the member `Type` only when the container type has such a `value_type` member:

```cpp
template<typename C, bool = HasMemberT_value_type<C>::value>
struct ElementT {
    using Type = typename C::value_type;
};
```

```cpp
template<typename C>
struct ElementT<C, false> {
};
```

A third example of making traits SFINAE-friendly is shown in Section 19.7.2 on page 444, where `IsNothrowMoveConstructibleT` first has to check whether a move constructor exists before checking whether it is declared with `noexcept`.

## 19.5 IsConvertibleT

Details matter. And for that reason, the general approach for SFINAE-based traits might become more complicated in practice. Let’s illustrate this by defining a trait that can determine whether a given type is convertible to another given type—for example, if we expect a certain base class or one of its derived classes. The `IsConvertibleT` trait yields whether we can convert a passed first type to a passed second type:

`traits/isconvertible.hpp`

```cpp
#include <type_traits> // for true_type and false_type
#include <utility>     // for declval

template<typename FROM, typename TO>
struct IsConvertibleHelper {
 private:
    // test() trying to call the helper aux(TO) for a FROM passed as F:
    static void aux(TO);
    template<typename F,
             typename = decltype(aux(std::declval<F>()))>
    static std::true_type test(void*);
    // test() fallback:
    template<typename>
    static std::false_type test(...);
 public:
    using Type = decltype(test<FROM>(nullptr));
};

template<typename FROM, typename TO>
struct IsConvertibleT : IsConvertibleHelper<FROM, TO>::Type {
};

template<typename FROM, typename TO>
using IsConvertible = typename IsConvertibleT<FROM, TO>::Type;

template<typename FROM, typename TO>
constexpr bool isConvertible = IsConvertibleT<FROM, TO>::value;
```

Here, we use the approach with function overloading, as introduced in Section 19.4.1 on page 416. That is, inside a helper class we declare two overloaded function templates named `test()` with different return types and declare a `Type` member for the base class of the resulting trait:

```cpp
template<typename F,
         typename = decltype(aux(std::declval<F>()))>
static std::true_type test(void*);

template<typename>
static std::false_type test(...);
...
using Type = decltype(test<FROM>(nullptr));
...
template<typename FROM, typename TO>
struct IsConvertibleT : IsConvertibleHelper<FROM, TO>::Type {
};
```

As usual, the first `test()` overload is designed to match only if the requested check succeeds, while the second overload is the fallback. Thus, the goal is to make the first `test()` overload valid if and only if type `FROM` converts to type `TO`. To achieve this, again we give our first declaration of `test` a dummy (unnamed) template argument initialized with a construct that is valid if and only if the conversion is valid. This template parameter cannot be deduced, and we will not provide an explicit template argument for it. Therefore, it will be substituted, and if the substitution fails, that declaration of `test()` will be discarded.

Again, note that the following doesn’t work:

```cpp
static void aux(TO);
template<typename = decltype(aux(std::declval<FROM>()))>
static char test(void*);
```

Here, `FROM` and `TO` are completely determined when this member function template is parsed, and therefore a pair of types for which the conversion is not valid (e.g., `double*` and `int*`) will trigger an error right away, before any call to `test()` (and therefore outside any SFINAE context).

For that reason, we introduce `F` as a specific member function template parameter.
