that does not point to an object; instead, we use the value 0 for the symbolic constant NULL, which expands to (0). Trying to use a null pointer results in a crash with an error message such as "Segmentation fault", "General protection fault", or "Bus error". Using a debugger, we can find out which line of code caused the crash.

At the end of the function, the alpha object holds the coordinate pair (1.0, 2.5), whereas beta holds (4.0, 4.5).

Pointers are often used to store objects allocated dynamically using new. In C++ jargon, we say that these objects are allocated on the "heap", whereas local variables (variables defined inside a function) are stored on the "stack".

Here's a code snippet that illustrates dynamic memory allocation using new:

```
#include "point2d.h"

int main()
{
    Point2D *point = new Point2D;
    point->setX(1.0);
    point->setY(2.5);
    delete point;

    return 0;
}
```

The new operator returns the memory address of a newly allocated object. We store the address in a pointer variable and access the object through that pointer. When we are done with the object, we release its memory using the delete operator. Unlike Java and C#, C++ has no garbage collector; dynamically allocated objects must be explicitly released using delete when we don't need them anymore. Chapter 2 describes Qt's parent-child mechanism, which greatly simplifies memory management in C++ programs.

If we forget to delete, the memory is kept around until the program finishes. This would not be an issue in the preceding example, because we allocate only one object, but in a program that allocates new objects all the time, this could cause the program to keep allocating memory until the memory is exhausted. Once an object is deleted, the pointer still holds the address of the object. Such a pointer is a "dangling pointer" and should not be used to access the object. Qt provides a "smart" pointer, QPointer<T>, that automatically sets itself to 0 if the QObject it points to is deleted.

In the following example, we invoked the default constructor and called setX(*