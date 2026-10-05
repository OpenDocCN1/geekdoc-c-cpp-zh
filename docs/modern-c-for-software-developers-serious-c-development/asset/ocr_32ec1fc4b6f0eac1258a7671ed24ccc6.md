initialize a vector as follows:

```
// Compile Error before C++ 11
std::vector<int> vec = {1,2,3,4,5};
```

or:

```
std::vector<int> vec {1,2,3,4,5};
```

Whenever the compiler sees a braced initializer list as {1, 5, 6, 9, 4}, it implicitly creates an object of type std::initializer_list<T> where T is the data type of the list.

We can create a light-weight object of type std::initializer_list<T> as follows:

```
#include <initializer_list>
std::initializer_list<int> data = {1,2,3,4,5};
```

std::initializer_list<T> is an array-like container. It has the following functions:

+   - size(): returns the size of the list
- begin(): returns an iterator to the beginning of the list
- end(): returns an iterator to the end of the list