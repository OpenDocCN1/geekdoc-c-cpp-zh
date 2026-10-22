In the previous section we saw that two function templates with the same name can coexist, even though they may be instantiated so that both have identical parameter types. Here is another simple example of this:

```
```cpp
template<typename T>
int f(T)
{
    return 1;
}

template<typename T>
int f(T*)
{
    return 2;
}
```
```

```
```cpp
template<typename T>
int f(T)
{
return 1;
}

template<typename T>
int f(T*)
{
return 2;
}
```
```

When T is substituted by `int*` in the first template, a function is obtained that has exactly the same parameter (and return) types as the one obtained by substituting `int` for T in the second template. Not only can these templates coexist, their respective instantiations can coexist even if they have identical parameter and return types.

The following demonstrates how two such generated functions can be called using explicit template argument syntax (assuming the previous template declarations): [Click here to view code image](#)

```
```cpp
#include <iostream>
#include "funcովerload1.hpp"

int main()
```
```