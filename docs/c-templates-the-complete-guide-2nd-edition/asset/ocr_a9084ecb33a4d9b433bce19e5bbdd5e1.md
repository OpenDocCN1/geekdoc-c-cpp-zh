```
template<typename T>
struct ElementT; // primary template

template<typename T>
struct ElementT<std::vector<T>> { //partial specialization for
std::vector
using Type = T;
};

template<typename T>
struct ElementT<std::list<T>> { //partial specialization for std::list
using Type = T;
};
...

template<typename T, std::size_t N>
struct ElementT<T[N]> { //partial specialization for arrays of known
bounds
using Type = T;
};

template<typename T>
struct ElementT<T[]> { //partial specialization for arrays of unknown
bounds
using Type = T;
};
...
```

Note that we should provide partial specializations for all possible array types (see Section 5.4 on page 71 for details).
We can use the type function as follows:

Click here to view code image

traits/elementtype.cpp

```
#include "elementtype.hpp"
#include <vector>
#include <iostream>
#include <typeinfo>

template<typename T>
void printElementType (T const& c)
{
std::cout << "Container of "
<< typeid(typename ElementT<T>::Type).name()
<< " elements.\n";
}

int main()
```