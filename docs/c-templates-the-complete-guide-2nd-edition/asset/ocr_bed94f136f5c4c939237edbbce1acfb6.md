```
void valuelisttest()
{
using Integers = Valuelist<int, 6, 2, 4, 9, 5, 2, 1, 7>;

using SortedIntegers = InsertionSort<Integers, GreaterThanT>;

static_assert(std::is_same_v<SortedIntegers,
Valuelist<int, 9, 7, 6, 5, 4, 2, 2, 1>>,
"insertion sort failed");
```

Note that you can provide the ability to initialize CTValue by using the literal operator, e.g., Click here to view code image

```
auto a = 42_c; // initializes a as CTValue<int,42>
```

See Section 25.6 on page 599 for details.

# 24.3.1 Deducible Non-type Parameters

In C++17, CTValue can be improved by using a single, deducible non-type parameter (spelled with auto): Click here to view code image

*typelist/ctvalue17.hpp*

```
template<auto Value>
struct CTValue
{
static constexpr auto value = Value;
};
```

This eliminates the need to specify the type for each use of CTValue, making it easier to use: Click here to view code image

```
using Primes = Typelist<CTValue<2>, CTValue<3>, CTValue<5>,
CTValue<7>, CTValue<11>>;
```

The same can be done for a C++17 Valuelist, but the result isn’t necessarily better. As noted in Section 15.10.1 on page 296, a non-type parameter pack with deduced type allows the types of each argument to differ: Click here to view code image

```
template<auto... Values>
class Valuelist { };
```

```
int x;
```