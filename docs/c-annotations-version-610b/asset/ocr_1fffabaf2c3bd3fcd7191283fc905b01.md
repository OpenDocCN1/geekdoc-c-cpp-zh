```
```cpp
DataType &Matrix<1, 1, DataType>::get()
{
    return d_cell;
}
```
```

Finally, the main function shown below illustrates how the `Matrix` class template and its partial specializations can be used:

```
```cpp
#include <iostream>
#include "matrix.h"
using namespace std;

int main(int argc, char **argv)
{
    Matrix<3, 2> matrix(cin);

    Matrix<1, 2> colMargins(matrix);
    cout << "Column margins:\n";
    cout << colMargins[0] << " " << colMargins[1] << '\n';

    Matrix<3, 1> rowMargins(matrix);
    cout << "Row marginals:\n";
    for(size_t idx = 0; idx < 3; idx++)
        cout << rowMargins[idx] << '\n';

    cout << "Sum total: " << Matrix<1, 1>(matrix) << '\n';
    return 0;
}
/*
    Generated output from input: 1 2 3 4 5 6

    Column marginals:
    9 12
    Row marginals:
    3
    7
    11
    Sum total: 21
*/
```
```

# 21.5 Variadic templates (C++11)

Up to this point we’ve only encountered templates having a fixed number of template parameters. The C++11 standard extends this with *variadic templates*.

Variadic templates are defined for function templates and for class templates. Variadic templates allow us to specify an arbitrary number of template arguments of any type.

Variadic templates were added to the language to prevent us from having to define many overloaded templates and to be able to create *type safe* variadic functions.

Although C (and C++) support variadic functions, their use has always been deprecated in C++ as those functions are notoriously *type-unsafe*. Variadic function templates can be used to process objects that until now couldn’t be processed properly by C-style variadic functions.

Template headers of variadic templates use the phrase `typename ...Params` (Params being a formal name). A variadic class template `Variadic` could be declared as follows: