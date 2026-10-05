# C++ Standard Library: std::reference_wrapper

# std::reference_wrapper

A reference wrapper is a class template that creates a reference to an object or a variable. It's declaration is:

```
template< class T >nclass reference_wrapper;
```

Note: reference_wrapper declares a family of reference wrapper types parameterized on T.

This class will wrap an object or variable of type T and create a reference to this object or variable. The wrapper object can be treated as if it is the object itself. A std::reference_wrapper object can be copied and assigned.

Here is an example:

```
#include <iostream>
#include <functional>
int main() {
int x = 5;
// create a reference wrapper for x
std::reference_wrapper<int> int_wrapper {x};
std::cout << int_wrapper << std::endl;
int_wrapper++;
std::cout << int_wrapper << std::endl;
x++;
std::cout << int_wrapper << std::endl;
return 0;
}
# output
5
6
7
```