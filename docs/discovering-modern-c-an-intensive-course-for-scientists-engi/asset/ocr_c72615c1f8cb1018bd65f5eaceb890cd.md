The method max is static and can be called for the type directly without the need of an object. Likewise, the static method min yields the minimal value—more precisely, the minimal representable value for int types and the minimal value larger than 0 for floating-point types. Therefore, C++11 introduces the member lowest which yields the smallest value for all fundamental types.

Termination criteria in fixed-point computations should be type-dependent. When they are too large, the result is unnecessarily imprecise. When they are too small, the algorithm might not terminate (i.e., it may only finish when two consecutive values are identical). For a floating-point type, the static method epsilon yields the smallest value to be added to 1 for a number larger than 1, in other words, the smallest possible increment (with respect to 1), also called Unit of Least Precision (ULP). We already used it in Section 4.2.2.2 for determining the similarity of two values.

The following generic example computes the square root iteratively. The termination criterion is that the approximated result of \(\sqrt{x}\) should be in an \(\epsilon\)-environment of \(x\). To ascertain that our environment is large enough, we scale it with \(x\) and double it afterward:

```
template <typename T>
T square_root(const T& x)
{
    const T my_eps = T{2} * x * numeric_limits<T>::epsilon();
    T r = x;
    while (std::abs((r * r) - x) > my_eps)
        r = (r + x/r) / T{2};
    return r;
}
```

The complete set of numeric_limits's members is available in online references like www.cppreference.com or www.cplusplus.com.

# 4.3.2 Type Traits

```
=> c++11/type_traits_example.cpp
```

The type traits that many programmers have already used for several years from the Boost library were standardized in C++11 and provided in <type_traits>. We refrain at this point from enumerating them completely and refer you instead to the before-mentioned online manuals. Some of the type traits—like is_const (§5.2.3.3)—are very easy to implement by partial template specialization. Establishing domain-specific type traits in this style (e.g., is_matrix) is not difficult and can be quite useful. Other type traits that reflect the existence of functions or properties thereof—such as is_nothrow_assignable—are quite tricky to implement. Providing type traits of this kind requires a fair amount of expertise (if not black magic).

```
=> c++11/is_pod_test.cpp
```

With all the new features, C++11 did not forget its roots. There are type traits that allow us to check the compatibility with C. is_pod tells us whether a type is a Plain Old Data type