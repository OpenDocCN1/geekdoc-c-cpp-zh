ovl() function, these elements require a promotion to `int`. Because the perfect match is better than a promotion, the first call to `ovl()` calls #1.

In the second call to `ovl()`, the first five elements are of type `char`, while the last is of type `int`. For the first `ovl()` function, the `char` elements are a perfect match, but the `int` requires a standard conversion, so the overall conversion is ranked as a standard conversion. For the second `ovl()` function, the `char` elements require a promotion to `int`, while the `int` element at the end is a perfect match. The overall conversion for the second `ovl()` function is ranked as a promotion, which makes it a better candidate than the first `ovl()`, even though only a single element’s conversion was better.

When initializing an object of class type with an initializer list, as in the calls to `g()` and `h()` in our original example, overload resolution proceeds in two phases: 1. The first phase considers only *initializer-list constructors*, that is, constructors whose only nondefault parameter is of type `std::initializer_list<T>` for some type T (after removing the top-level reference and `const`/`volatile` qualifiers).

+   2. If no such viable constructor is found, then the second phase considers all other constructors. There is one exception to this rule: If the initializer list is empty and the class has a default constructor, the first phase is skipped so that the default constructor will be called.

The effect of this rule is that any initializer-list constructor is a better match than any non-initializer-list constructor, as illustrated in the following example:

[Click here to view code image](#)

```
overload/initlistctor.cpp

#include <initializer_list>
#include <string>
#include <iostream>

template<typename T>
struct Array {
Array(std::initializer_list<T>) {
std::cout << "#1\n";
}
Array(unsigned n, T const&) {
std::cout << "#2\n";
}
};

void arr1(Array<int>) {
}

void arr2(Array<std::string>) {
```