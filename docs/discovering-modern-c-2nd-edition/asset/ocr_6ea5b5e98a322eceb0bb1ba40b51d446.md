used instantiate the `vec` class with the iterator's `value_type`. Sometimes there is no type information available at all:

+   8. We will discuss type traits more comprehensively in Section 5.2.1.

Click here to view code image

```
template <typename Value>
struct vec
{
    vec(unsigned s) : s(s), d(new Value[s]) {}
};

vec x(3);
```

Then we can provide a default type. Either as a class parameter:

Click here to view code image

```
template <typename Value= double>
struct vec;
```

Or as a deduction guide:

```
vec(unsigned s) -> vec<double>;
```

# **C++17** 3.4.5 Deducing Multiple Types

=> c++17/structured_bindings.cpp

Sometimes we compute multiple results in a function and can return them together as a `pair`, `tuple`, or user-defined class. In the examples in Section 4.4.2 we'll illustrate various possibilities to access and/or copy the single components of a `tuple`. We like to anticipate these examples and show an opportunity from C++17 for using type deduction without storing the bundled results first. It is called *Structured Bindings* and allows us to bind the members of utility or user-defined classes to new variables while deducing their returns. In our example we have a function for an LU factorization that returns a matrix and a vector:

Click here to view code image

```
auto lu(const matrix& A)
{
    // ... some computations
```