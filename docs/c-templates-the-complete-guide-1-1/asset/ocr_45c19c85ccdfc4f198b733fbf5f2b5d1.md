```
```cpp
template<typename T>
concept HasPlus = requires(T a, T b) {
    a + b;
};

template<typename T>
int f(T a) requires HasPlus<T> {
    std::cout << "T\n";
}

void g()
{
    int a, b;
    f(a);
    f(b);
}
```
```

[Click here to view code image](#)

```
```cpp
#include <iostream>

template<typename T>
concept HasPlus = requires(T a, T b) {
    a * b;
};

template<typename T>
int f(T a) requires HasPlus<T> {
    std::cout << "T\n";
}

template <int I>
void g() {
    f(I);
}
```
```

This program must output

T
T

which means that the two definition of f() must be mangled differently.

+   1. Continuous iterators are a refinement of random access iterators introduced in C++17. No std::contiguous_iterator tag was added for them because existing algorithms that rely on std::ranges::contiguous_range would be harder to extend if that tag were changed.

+   2. The specification being proposed for standardization is a little more powerful than this. It breaks down containers into sets of "domain concepts" (including the point of regular expressions and analyses that are sent to one or are clearly a direct subset of the other).

+   3. The experimental implementation of concepts in GCC 7.1 is known to be deficient in this respect.