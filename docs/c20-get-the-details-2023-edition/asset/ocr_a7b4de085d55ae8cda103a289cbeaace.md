```
```cpp
// macro.ixx

module;

#include "macro.h"

export module macro;
```
```

# #### 4.2.4.2 Templates in Modules

I often hear the question: How do modules export templates? When you instantiate a template, its definition must be available. For this reason, template definitions are hosted in headers. Conceptually, the usage of a template has the following structure.

# ##### 4.2.4.2.1 Without Modules

+   - `templateSum.h`

# **Definition of the function template sum**

```
```cpp
// templateSum.h

template <typename T, typename T2>
auto sum(T fir, T2 sec) {
    return fir + sec;
}
```
```

+   - `sumMain.cpp`

# **Use of the template sum**

```
```cpp
// sumMain.cpp

#include "templateSum.h"

int main() {

    sum(1, 1.5);

}
```
```

The main program includes the header `templateSum.h`. The call `sum(1, 1.5)` triggers the template instantiation. In this case, the compiler generates out of the function template `sum` the concrete function `sum`, which takes an `int` and a `double` as arguments. If you want to visualize this process, use the example on [C++ Insights](https://cppinsights.io/).

[https://cppinsights.io/](https://cppinsights.io/)