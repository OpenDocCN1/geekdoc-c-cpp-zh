|  | and so on. |
|---|---|
| Passing pointers to functions | Passing an argument by reference or by address both enable the passed argument to be changed in the calling function by the called function. |
| Return pointer from functions | C++ allows a function to return a pointer to local variable, static variable and dynamically allocated memory as well. |

# Null Pointers

It is always a good practice to assign the pointer NULL to a pointer variable in case you do not have exact address to be assigned. This is done at the time of variable declaration. A pointer that is assigned NULL is called a **null** pointer.

The NULL pointer is a constant with a value of zero defined in several standard libraries, including iostream. Consider the following program:

```
```cpp
#include <iostream>

using namespace std;

int main ()
{
    int *ptr = NULL;

    cout << "The value of ptr is " << ptr ;

    return 0;
}
```
```

When the above code is compiled and executed, it produces the following result:

```
```text
The value of ptr is 0
```
```

On most of the operating systems, programs are not permitted to access memory at address 0 because that memory is reserved by the operating system. However, the memory address 0 has special significance; it signals that the pointer is not intended to point to an accessible memory location. But by