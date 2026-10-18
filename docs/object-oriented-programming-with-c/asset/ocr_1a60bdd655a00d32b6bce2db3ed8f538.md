> **NOTE:** *The pointers, which are not initialized in a program, are called Null pointers. Pointers of any data type can be assigned with one value i.e., ‘0’ called null address.*

# Manipulation of Pointers

As discussed earlier, we can manipulate a pointer with the indirection operator, i.e., ‘*’ which is also known as dereference operator. With this operator, we can indirectly access the data variable content. It takes the following general form:

`*pointer_variable`

As we know, dereferencing a pointer allows us to get the content of the memory location that the pointer points to. After assigning address of the variable to a pointer, we may want to change the content of the variable. Using the dereference operator, we can change the contents of the memory location.

Let us consider an example that illustrates how to dereference a pointer variable. The value associated with the memory address is divided by 2 using the dereference operator. The division affects only the memory contents and not the memory address itself. Program 9.2 illustrates the use of dereference operator in C++.

# Program 9.2  Manipulation of Pointers

```
```cpp
#include <iostream.h>
#include <conio.h>
void main( )
{
int a=10, *ptr;
```
```