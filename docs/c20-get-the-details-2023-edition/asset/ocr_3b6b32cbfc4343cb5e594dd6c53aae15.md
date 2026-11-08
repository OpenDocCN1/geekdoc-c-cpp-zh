```
```text
1 2 3 4 5
true
10
10
```
```

Constrained placeholders instead of unconstrained placeholders in action

# 4.1.6 Abbreviated Function Templates

With C++20, you can use an unconstrained placeholder (auto) or a constrained placeholder (concept) in a function declaration including member functions and operators. This function declaration automatically becomes a function template.

Abbreviated function templates

```
```cpp
// abbreviatedFunctionTemplates.cpp

#include <concepts>
#include <iostream>

template<typename T>
requires std::integral<T>
T gcd(T a, T b) {
    if( b == 0 ) return a;
    else return gcd(b, a % b);
}

template<typename T>
T gcd1(T a, T b) requires std::integral<T> {
    if( b == 0 ) return a;
    else return gcd1(b, a % b);
}

template<std::integral T>
T gcd2(T a, T b) {
    if( b == 0 ) return a;
    else return gcd2(b, a % b);
}

std::integral auto gcd3(std::integral auto a, std::integral auto b) {
    if( b == 0 ) return a;
    else return gcd3(b, a % b);
}
```
```