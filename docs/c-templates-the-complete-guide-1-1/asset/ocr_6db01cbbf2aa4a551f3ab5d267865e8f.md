First, this formulation has the desirable property that the number of instantiations required to insert an element into a sorted typelist is proportional to the length of the resulting typelist. The number of recursive instantiations of Insert is at most the number of insertions in sorted order, at least in the length of the list. (Insertion sort maintains quadratic in the number of instantiations for inputs sorted in reverse.)

The following program demonstrates the use of insertion sort to order a list of types based on a size. The comparison operation used is the `SmallerThanT` predicate.

Click here to view code image

```
```cpp
template<typename T, typename U>
struct SmallerThanT
{
    static constexpr bool value = sizeof(T) < sizeof(U);
};

void test_insertion_sort()
{
    using Types = Typelist<int, char, short, double>;
    using BT = InsertionSort<Types, SmallerThanT>;
    std::cout << std::is_same<BT, Typelist<char, short,
        int, double>>::value << '\n';
}
```
```

# ## 24.3 NON-TYPE TYPELISTS

Typelists provide the ability to describe and manipulate a sequence of types in a rich set of algorithms and operations. In some cases, it is also useful to work with sequences of compile-time values, such as the length of a multidimensional array or indices into another typelist.

There are several ways to produce a typelist of compile-time values. One simple approach involves defining a `CTValue` class template (named for a compile-time value) that represents a value of a specific type within a typelist.

Click here to view code image

```
```cpp
template<typename T, T Value>
struct CTValue
{
    static constexpr T value = Value;
};
```
```

Using the `CTValue` template, we can now express a typelist containing integer values for the first five prime numbers.

Click here to view code image

```
```cpp
using Primes = Typelist<CTValue<int, 2>, CTValue<int, 3>,
                       CTValue<int, 5>, CTValue<int, 7>,
                       CTValue<int, 11>>;
```
```

With this representation, we can perform numeric computations on a typelist of values, such as computing the product of those primes.

First, `Multiply` accepts two compile-time values with the same type and produces a new compile-time value of that same type, multiplying the input values.

Click here to view code image

```
```cpp
template<typename T, typename U>
struct MultiplyT;

template<typename T, T Value1, T Value2>
struct MultiplyT<CTValue<T, Value1>, CTValue<T, Value2>>
{
    using type = CTValue<T, Value1 * Value2>;
};
```
```