```
```cpp
values.push_back(val);
}

friend std::ostream& operator<<(std::ostream& strm, const Customer& cust) {
    strm << '[' << cust.name << ": ";
    for (int val : cust.values) {
        strm << val << ' ';
    }
    strm << ']';
    return strm;
}
};
```
```

This class has two (potentially) expensive members, a string for the name and a vector of integral values:

```
```cpp
class Customer {
private:
    std::string name;          // name of the customer
    std::vector<int> values;   // some values of the customer
    ...
};
```
```

Both members are expensive to copy

+   - To copy the name, we have to allocate memory for the characters of the string (unless we have a short name and strings are implemented using the *small string optimization (SSO)*).
+   - To copy the values, we have to allocate memory for the elements of the vector.

It would be even more expensive if we had a vector of strings or another pretty expensive element type. For example, a *deep copy* of a vector of strings would have to allocate memory for both the dynamic array of elements and the memory each element needs.

The good news is that **move semantics is usually automatically supported** by such a class. Since C++11, the compiler usually generates a *move constructor* and a *move assignment operator* (similar to the automatic generation of a copy constructor and a copying assignment operator).

This has the following effect:

+   - Returning a local Customer by value will use move semantics (if it is not optimized away).
+   - Passing an unnamed Customer by value will use move semantics (if it is not optimized away).
+   - Passing a temporary Customer (e.g., returned by another function) by value will use move semantics (if it is not optimized away).
+   - Passing a Customer object marked with `std::move()` by value will use move semantics (if it is not optimized away).

For example:

*basics/customer1.cpp*

```
```cpp
#include "customer.hpp"
#include <iostream>
#include <random>
```
```