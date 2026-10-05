# C++ Standard Library: std::initializer_list

Initializer lists permit us to initialize a collection of objects using list syntax, for example: `int array[2] {1, 2};`

An initializer list is a class template that is declared as follows:

```
#include <initializer_list>

template <class T>
class initializer_list;
```

The following is an example of the declaration for an `initializer_list` variable:

```
#include <initializer_list>
std::initializer_list<double> bar;
```

Internally, an `initializer_list` is an array of objects of type T.

An `initializer_list` object can be created from a braced init list:

```
#include <iostream>
#include <initializer_list>
int main()
{
    // declare an initializer list and assign values to it
    std::initializer_list<int> ilist = {4, 1, 11};

    for (auto value : ilist) {
        std::cout << value << " ";
    }

    std::cout << std::endl;

    return 0;
}

// output
4 1 11
```