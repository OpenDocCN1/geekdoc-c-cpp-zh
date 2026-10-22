+   - As a caller you can often still decide to pass arguments by reference, using `std::ref()` and `std::cref()` (see Section 7.3 on page 112).
+   - Although passing string literals or raw arrays always can become a problem, passing them by reference often is considered to become the bigger problem. All this will be discussed in detail in Chapter 7. For the moment inside the book we will usually pass arguments by value unless some functionality is only possible when using references.

# 1.6.2 Why Not inline?

In general, function templates don’t have to be declared with `inline`. Unlike ordinary noninline functions, we can define noninline function templates in a header file and include this header file in multiple translation units.

The only exception to this rule are full specializations of templates for specific types, so that the resulting code is no longer generic (all template parameters are defined). See Section 9.2 on page 140 for more details.

From a strict language definition perspective, `inline` only means that a definition of a function can appear multiple times in a program. However, it is also meant as a hint to the compiler that calls to that function should be “expanded inline.” Doing so can produce more efficient code for certain cases, but it can also make the code less efficient for many other cases. Nowadays, compilers usually are better at deciding this without the hint implied by the `inline` keyword. However, compilers still account for the presence of `inline` in that decision.

# 1.6.3 Why Not constexpr?

Since C++11, you can use `constexpr` to provide the ability to use code to compute some values at compile time. For a lot of templates this makes sense.

For example, to be able to use the maximum function at compile time, you have to declare it as follows: [Click here to view code image](#)

```
basics/maxconstexpr.hpp

```cpp
template<typename T1, typename T2>
constexpr auto max (T1 a, T2 b)
```
```