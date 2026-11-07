After the `using` statement, to access a `namespace` member, you do not have to put the namespace name and the scope resolution operator before the `namespace` member. However, if a `namespace` member and a global identifier in a program have the same name, to access this `namespace` member in the program, the namespace name and the scope resolution operator must precede the `namespace` member. Similarly, if a `namespace` member and an identifier in a block have the same name, to access this `namespace` member in the block, the namespace_name and the scope resolution operator must precede the `namespace` member.

Examples 8-9 through 8-12 help clarify the use of the `namespace` mechanism.

# EXAMPLE 8-9

Consider the following C++ code:

```
```cpp
#include <iostream>

using namespace std;
.
.
int main()
{
    .
    .
    .
}
.
.
.
```
```

In this example, you can refer to the global identifiers of the header file `iostream`, such as `cin`, `cout`, and `endl`, without using the prefix `std::` before the identifier name. The obvious restriction is that the block (or function) that refers to the global identifier (of the header file `iostream`) must not contain any identifier with the same name as this global identifier.

# EXAMPLE 8-10

Consider the following C++ code:

```
```cpp
#include <cmath>

int main()
{
    double x = 15.3;
    double y;
```
```