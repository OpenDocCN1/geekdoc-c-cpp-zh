There are scenarios where we cannot say from the program sources what kind of constant we have, for instance:

```
```cpp
const long ri = floor(sqrt(i));
static_long<ri> sri; // compiles with g++ 4.7-4.9
```
```

Here, ri is known during compilation when sqrt and floor are both constexpr in the implementation of the standard library (e.g., in g++ 4.7-4.9); otherwise it is an error when used as a template argument.

To ensure that a constant has a compile-time value, we have to declare it constexpr:

```
```cpp
constexpr long ri = floor(sqrt(i)); // compiles with g++ 4.7-4.9
```
```

This guarantees that ri is known during compilation; otherwise this line does not compile. Note that constexpr is stricter for variables than for functions. A constexpr variable accepts only compile-time values while a constexpr function accepts both compile-time and run-time arguments.

# ## 5.2 Providing and Using Type Information

In Chapter 3, we saw the expressive power of function and class templates. However, all those functions and classes contained exactly the same code for all possible argument types. To increase the expressiveness of templates further, we will introduce smaller or larger code variations depending on the argument types. Thus, we first need information on types to dispatch on. Such type information can be technical —like is_const or is_reference—or semantic/domain-specific—like is_matrix or is_pressure. For most technical type information, we will find library support in the headers <type_traits> and <limits> as illustrated in Section 4.3. Domain-specific type properties are waiting for us to be implemented.

# ### 5.2.1 Type Traits

```
=> c++11/magnitude_example.cpp
```

In the function templates we have written so far, the types of temporaries and the return values were equal to one of the function arguments. Unfortunately, this does not always work. Imagine we implement a function that returns out of two values the one with the minimal magnitude:

```
```cpp
template <typename T>
T inline min_magnitude(const T& x, const T& y)
{
    using std::abs;
    T ax = abs(x), ay = abs(y);
    return ax < ay ? x : y;
}
```
```

We can call this function for int, unsigned, or double values:

```
```cpp
double d1 = 3., d2 = 4.;
cout << "min |d1, d2| = " << min_magnitude(d1, d2) << '\n';
```
```