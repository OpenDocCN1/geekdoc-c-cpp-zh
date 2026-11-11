# Dereferencing Operators

In C++, we can access and manipulate the data stored in the memory location through pointers. The process of accessing and manipulating the data is known as dereferencing, and the operators used for dereferencing are called dereferencing operators. Table 13 lists the dereferencing operators:

**Table 13: Member Dereferencing Operators**

| Operator | Description |
| :--- | :--- |
| `::*` | Dereferences pointers to class members |
| `.*` | Accesses a class member using the object and pointer to that member |
| `->*` | Accesses a class member using another pointer that in turn accesses the class object to access the class member |

# Memory Management Operators

Memory management is an essential part of a programming language. Occasionally, it is possible that the object you have created to store 100 elements, stores only 5 elements, implying that the memory allocated to rest of the elements is wasted. Memory should be allocated dynamically that is, at run time, which helps to reduce memory wastage so that other resources can use that memory. C++ provides the `new` and `delete` operators to manage memory.

The `new` operator is used to allocate memory to a variable at run time according its data type. This reduces the wastage of memory unnecessarily allocated to a variable. In case sufficient memory is not available for a variable, the operator returns null.

The delete operator frees the memory allocated to a variable. Listing 30 shows the use of the new and delete operators (you can find the NewDeleteEx.cpp file on the CD in the code/chapter1 folder):

▶ **Listing 30: Using Memory Management Operators**

```
```cpp
#include <iostream.h>
#include <stdlib.h>
int main()
{
    double *pi;
    pi = new double; // allocating memory
    if ( pi == NULL)
    {
        exit (1);
    }
    else
    {
        *pi = 3.14159;
        cout << "The value of pi is " << *pi << endl;
    }
    delete pi; // freeing the memory
```
```