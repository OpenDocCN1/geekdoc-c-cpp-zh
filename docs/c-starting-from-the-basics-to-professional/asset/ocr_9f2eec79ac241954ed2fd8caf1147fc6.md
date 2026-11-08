The second using declaration in the exported math namespace similarly brings all overloads of the `sqrt()` function into this namespace as well. You cannot pick and choose which overloads of a function to import into a namespace; you can only import a particular name (see also the comment in the code). `std::sqrt()`, for instance, has overloads for double, float, long double, and various integral parameters; due to our single using declaration all these overloads are addressable now as `math::sqrt()`.

If you want to introduce all constants (and variable templates) of the `<numbers>` module into the math namespace—instead of only the `sqrt2` constant like we did originally—you can do so by adding (and exporting) the following using directive.

```
```cpp
namespace math
{
    export using namespace std::numbers;
}
```
```

When adding a using directive or declaration at any scope that is not a namespace, analogous aliasing rules apply, but then only within that scope. Take the following function template, for instance, for functions that compute the length of the hypotenuse of a right-angle triangle given the length of the other two sides (using the well-known Pythagorean theorem). Since this type is defined in the global namespace, its body would by default have to qualify the `sqrt` and square names with `math::`.

```
```cpp
auto hypot(const auto& x, const auto& y)
{
    using namespace math;
    // Or:
    //     using math::square;
    //     using math::sqrt; // Same as, of course: using std::sqrt; */
    return sqrt(square(x) + square(y));
}
```
```

The declaration or directive applies until the end of the block that contains it.

> **Caution**  Never use this naive implementation of `hypot()` in practice. Always use the `std::hypot()` functions of `<cmath>` instead. The reason is that our naive solution often fails in inaccurate (it suffers both from underflow and overflow issues). Because creating efficient and numerically stable mathematical primitives is deceptively hard (many scientific articles have been written on algorithms for `hypot()` alone), you should always look for predefined primitives first.

> **Tip**  What we explained here for using directives and declarations also applies for type aliases and using enum declarations (both introduced in Chapter 3). They all can be exported from modules and/or brought into a namespace, or applied more locally at function or event statement scopes. You saw an example of a local using enum declaration inside the switch statement in the `from_roman()` helper function earlier in this chapter.
> 
> Personally, we prefer to apply using directives and declarations only sparsely, and always as locally as possible. That way we do not only avoid inadvertent name clashes, but we also clarify to the reader of our code from which namespace each entity name originates.