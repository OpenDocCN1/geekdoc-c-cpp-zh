```
```cpp
y = std::pow(x, 2);
.
.
}
```
```

This example accesses the function `pow` of the header file `cmath`.

# EXAMPLE 8-11

Consider the following C++ code:

```
```cpp
#include <iostream>
.
.
int main()
{
    using namespace std;
.
.
.
}
.
.
.
```
```

In this example, the function `main` can refer to the global identifiers of the header file `iostream` without using the prefix `std::` before the identifier name. The `using` statement appears inside the function `main`. Therefore, other functions (if any) should use the prefix `std::` before the name of the global identifier of the header file `iostream` unless the function has a similar `using` statement.

# EXAMPLE 8-12

Consider the following C++ code:

```
```cpp
#include <iostream>

using namespace std;        //Line 1

int t;                       //Line 2
double u;                    //Line 3

namespace expN
{
    int x;                   //Line 4
    char t;                  //Line 5
```
```