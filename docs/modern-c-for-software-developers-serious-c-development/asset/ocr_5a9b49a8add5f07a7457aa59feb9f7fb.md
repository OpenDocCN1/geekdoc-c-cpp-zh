# Modern C++: Trailing Return Types (C++11)

C++11 introduces a new syntax for the return type of a function. This syntax is called a trailing return type.

The syntax for trailing return types is:

```
auto getSum() -> float;
```

The declaration auto getSum() -> float is equivalent to:

```
float getSum();
```

When we use a trailing return type, the function declaration must start with auto. The type of the return value is deduced from the trailing return type and not auto.

One of trailing return types occurs in function templates where the return type of the function depends on the types of the arguments:

```
#include <iostream>
template<class T, class U>
auto multiply(T lhs, U rhs) -> decltype(lhs * rhs)
{
    return lhs * rhs;
}
int main()
{
    auto value = multiply(2.3, 6);
    std::cout << value << std::endl;
}
// output
13.8
```