```
```cpp
return operator+(std::move(tmp), rhs);
}

#endif
```
```

*Caveat:* when defining these function templates ensure that the binary operator specifying an rvalue reference as its first parameter is defined before the binary operator specifying a const lvalue reference as its first parameter, or programs using these templates fail due to infinite recursion.

The function templates for the other binary operators can easily be added to these addition operators. After collecting them in a file `binops.h` include this file in, e.g., your class header file to add the binary operators to your class.

Interestingly, classes *not* implementing move constructors can still use these templates, as the move constructor itself is never called by the implementations of the binary operator (and its call is usually optimized away by copy elision). The following program (using modified function templates containing output statements) behaves identically whether or not the move constructor is defined:

```
```cpp
#include <iostream>
using namespace std;

template <typename Class>
Class operator+(Class &&lhs, Class const &rhs)
{
    cout << "operator+(Class &&lhs, Class const &rhs)\n";

    return lhs += rhs;
}

template <typename Class>
Class operator+(Class const &lhs, Class const &rhs)
{
    cout << "operator+(Class const &, Class const &)\n";

    Class tmp(lhs);
    return operator+(std::move(tmp), rhs);
}

template <typename Class>
Class operator-(Class &&lhs, Class const &rhs)
{
    return lhs -= rhs;
}

template <typename Class>
Class operator-(Class const &lhs, Class const &rhs)
{
    Class tmp(lhs);
    return operator-(std::move(tmp), rhs);
}

class Class
{
public:
    Class() = default;
    Class(Class const &other) = default;
    Class(int)
    {}
    Class(Class &&tmp)
```
```