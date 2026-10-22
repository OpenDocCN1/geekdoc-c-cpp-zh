poly/printmax.cpp

```
#include <vector>
#include <list>
#include <algorithm>
#include <iostream>
#include "MyClass.hpp"

template<typename T>
void printMax (T const& coll)
{
    // compute position of maximum value
    auto pos = std::max_element(coll.begin(),coll.end());

    // print value of maximum element of coll (if any):
    if (pos != coll.end()) {
        std::cout << *pos << '\n';
    }
    else {
        std::cout << "empty" << '\n';
    }
}
```