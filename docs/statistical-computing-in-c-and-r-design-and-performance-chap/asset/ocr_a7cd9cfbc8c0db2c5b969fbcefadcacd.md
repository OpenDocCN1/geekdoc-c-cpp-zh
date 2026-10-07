# MATRIX AND VECTOR CLASSES

```
g(m);
cout << "The destructor will now be called." << endl;
return 0;
}
```

A similar outcome will be obtained from naive use of the assignment or = operator in

```
//equalEx.cpp
#include "simpleMatrix.h"
#include <iostream>

using std::cout; using std::endl;

int main() {
    Matrix m1(1., 2, 2);
    Matrix m2;
    m2 = m1;
    cout << "The destructor will now be called." << endl;
    return 0;
}
```

Specifically, either of these two programs produces run-time errors that output in-
cluding a statement such as

```
The destructor will now be called
equalEx(417): malloc: *** error for object 0x10010090
pointer being freed was not allocated
*** a breakpoint in malloc_error_break to debug
Abort trap
```

This message is about a memory problem related to the C function malloc for dynamic
memory allocation that lies under the hood of the C++ new operator. It specifies the
problem may arise from an attempt to delete the memory for a pointer (using the C function
free is called by delete) that has not actually been allocated memory on the freestore.
That is precisely what occurred.

To understand what has transpired we need to think about when a destructor for a class
is called occurs when an object goes out of scope: i.e., when the end
of a block of code contains the object is reached. For the first nonoperative driver
program ExCpp a copy of the Matrix object is created to pass by value to the
function g. It then goes out of scope when control passes back to main and the
code is destroyed by the destructor function Matrix deletes the memory
to pointers associated with the pa member for the class. But, since the copy was made
element-element, that the memory pointed to by pa (i.e., the pa pointer
associated with the Matrix object in main) is what is actually deleted. So, at point
is not allocated to m pa. When m goes out of scope at the end of main the
dest is called again and deletes the memory for m pa that no
longer points to the allocated memory.

A similar problem arises for the second nonoperative driver equalEx.cpp. In
this latter define the behavior of is to make an element-by-element copy m2 of the
Matrix object m1 when m2 is equal to m1. At the end of main the destructor for m2 is
created also by deleting the memory allocated to m1. pa. When an attempt is made to
delete this memory, for the object m1, an error occurs.

The above discussion makes defined explicitly: namely, when dynamic memory is involved
two things must a copy constructor and an overloaded version
of assignment operator. Let us first deal with the issue of creating a copy constructor.

Copy constructors are a special type of constructor that have a const reference to a class
object as their argument. Specifically, they employs the syntax