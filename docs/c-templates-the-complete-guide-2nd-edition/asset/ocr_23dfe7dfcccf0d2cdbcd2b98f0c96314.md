The essence of the EnableIf technique is to enable a particular template or partial specialization only when the template arguments meet some specific criteria. For example, the most efficient form of the advanceIter() algorithm checks that the iterator argument’s category is convertible to std::random_access_iterator_tag, which implies that the various random-access iterator operations will be available to the algorithm.

What if we took this notion to the extreme and encoded every operation that the template performs on its template arguments as part of the EnableIf condition? The instantiation of such a template could never fail, because template arguments that do not provide the required operations would cause a deduction failure (via EnableIf) rather than allowing the instantiation to proceed. We refer to such templates as “instantiation-safe” templates and sketch the implementation of such templates here.

We start with a very basic template, min(), which computes the minimum of two values. We would typically implement such as a template as follows: Click here to view code image

```
template<typename T>
T const& min(T const& x, T const& y)
{
if (y < x) {
return y;
}
return x;
}
```

This template requires the type T to have a < operator able to compare two T values (specifically, two T const lvalues) and then implicitly convert the result of that comparison to bool for use in the if statement. A trait that checks for the < operator and computes its result type is analogous to the SFINAE-friendly PlusResultT trait discussed in Section 19.4.4 on page 424, but we show the LessResultT trait here for convenience: Click here to view code image

typeoverload/lessresult.hpp

```
#include <utility> // for declval()
#include <type_traits> // for true_type and false_type

template<typename T1, typename T2>
class HasLess {
template<typename T> struct Identity;
template<typename U1, typename U2> static std::true_type
test(Identity<decltype(std::declval<U1>() < std::declval<U2>())>*);
template<typename U1, typename U2> static std::false_type
```