compiler can detect and report the problems. All current C++ compilers share one weakness with template processing: poor human-readable error messages. The error messages the compiler produces in these situations tend to be lengthy and difficult to decipher even for experienced C++ programmers. This is because the compiler bases its error messages on its processing of the instantiated code, not the original un-instantiated source. Since programmers see only the un-instantiated source, deciphering the compiler's template error messages tends to be more challenging than usual.

As Listing 19.4 (templatescale.cpp) shows, a template can accept non-type parameters.

# Listing 19.4: templatescale.cpp

```
```cpp
#include <iostream>

template <int N>
int scale(int value) {
    return value * N;
}

int main() {
    std::cout << scale<3>(5) << '\n';
    std::cout << scale<4>(10) << '\n';
}
```
```

Note that in Listing 19.4 (templatescale.cpp) the typename keyword is missing, and in its place is the actual type int. This means parameter N is a non-type template parameter. The program prints

```
15
40
```

Listing 19.5 (templatescale2.cpp) uses both a type-parameter and a non-type parameter.

# Listing 19.5: templatescale2.cpp

```
```cpp
#include <iostream>

template <typename T, int N>
T scale(const T& value) {
    return value * N;
}

int main() {
    std::cout << scale<double, 3>(5.3) << '\n';
    std::cout << scale<int, 4>(10) << '\n';
}
```
```

Listing 19.5 (templatescale2.cpp) displays the following during its execution:

```
15.9
40
```

The compiler will instantiate two scale functions:

```
```cpp
// Instantiated by the compiler due to scale<double, 3>:
double scale(const double& value) {
    return value * 3;
}
```
```