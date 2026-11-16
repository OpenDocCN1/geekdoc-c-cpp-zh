
The member function concat() appends one string to another. It can be called as follows:

```
s3.concat(s2);
```

Here, the variable str is the data member of s3, the object which invoked the member function. The argument passed to the member function is an object of class String. Using the strcpy() function, s2.str will be appended to s3.str.

Therefore the call from main():

```
s3.concat(s2);
```

causes s2 to be appended to the existing s3.

Note that s1 = s2 effectively copies the contents of the data members from object s2 to the object s1. Thus, we have created an assignment facility for strings. This assignment facility is already built in because we defined the class String. It is not due to any member function. We'll enhance the String class later.

## Arrays of Class Objects

Just as we can declare arrays of common data types, we can declare arrays of class objects. For example, we can declare an array of 5 `Elevator` objects:

```
// e1.cpp

#include <iostream>
#include "elevator.h"

using namespace std;

int main() {
    Elevator e[5];
    ...
}
```

Storage for the entire array is allocated on the stack as shown below:

![](img/adb3588dc0dfe9f607c1d417be6bb240_123_0.png)

There's only one hard and fast rule to remember: class objects to be stored within arrays must have default constructors. The default constructors could either be provided by the compiler or the programmer. However, if the programmer declares a constructor and does not provide a default constructor, the default constructor provided by the compiler is gone.

When an array of class objects comes into being, C++ calls the class default constructor once for each object in the array. In the case of the `Elevator` constructor above, C++ calls `Elevator`'s default constructor 5 times, thus initializing objects `e[0]` through `e[4]` to the correct values.

If you want C++ to call a different constructor, you must explicitly initialize each array element directly in the array's declaration:

```
// e2.cpp
#include <iostream>
#include "elevator.h"
using namespace std;
int main() {
    Elevator e[5] = {
        Elevator(),
        Elevator(),
        Elevator(2, 5),
        Elevator(7, 3),
        Elevator()
    };
    ...
}
```

Note that sometimes braces are used as if we were initializing fields of a `struct` but some compilers are ok without them.

There is no easy way to initialize some arrayed class objects using the default constructor and some using an alternate constructor. If you need to do that, it's probably best to use the default constructor for the entire array and then reinitialize selected objects as needed. Except for small arrays, this is probably too unwieldy to be of much practical use.

## Dynamic Arrays

Arrays of class objects may also be stored on the heap (free store) and addressed with pointers. The following program declares an array of pointers to `Elevator` objects. Storage for the array of pointers is allocated on the stack while storage for each of the actual `Elevator` objects is allocated on the heap.

```
// e3.cpp
#include <iostream>
#include "elevator.h"
using namespace std;
int main() {
    int i;
    Elevator *e[5];
    for (i = 0; i < 5; i++)
        e[i] = new Elevator;
    for (i = 0; i < 5; i++)
        cout << e[i]->getFloor() << endl;
    for (i = 0; i < 5; i++)
        delete e[i];
}
```

Below is a representation of the dynamic array created in the preceding program:

created on stack   created on heap

e
---
0 | •-----|------> [Elevator object]
1 | •-----|------> [Elevator object]
2 | •-----|------> [Elevator object]
3 | •-----|------> [Elevator object]
4 | •-----|------> [Elevator object]

An alternate approach to dynamically create an array of class objects on the heap is as follows:

```
// e4.cpp
//-------------------------------------
#include <iostream>
#include "elevator.h"

using namespace std;

int main() {
   Elevator *eptr;

   eptr = new Elevator[5];
   for (int i = 0; i < 5; i++)
      cout << eptr[i].getFloor() << endl;
   delete [] eptr;
}
```

As shown in the diagram below, the only storage that is allocated on the stack is the storage for the pointer to the Elevator array. Storage for the array itself (i.e., storage for each Elevator object) is allocated on the heap.

| | created on stack | created on heap | |
|---|---|---|---|
| | eptr=====> | 0 | Elevator object | |
| | | 1 | Elevator object | |
| | | 2 | Elevator object | |
| | | 3 | Elevator object | |
| | | 4 | Elevator object | |

In the above program, note that we use the direct component selector (.) operator rather than the indirect component selector (->) operator to access the member functions. This is due to the fact that we do not have an array of pointers to class objects this time, but rather the class objects themselves are contained within the array.

As with other dynamic objects, we should delete dynamic class object arrays after we are done using them. However, deleting such an array leads to a problem. Due to the C and C++ inability to distinguish between pointers and arrays, programs must use a special form of delete ([]) to ensure that when deleting a dynamic array of class objects any destructor for those objects is properly called.

If we had simply written:

```
delete eptr;
```

the compiler would not know whether eptr addresses a single Elevator class object or an array of Elevator class objects. To inform the compiler that eptr addresses an array, we add empty brackets to delete:

```
delete [] eptr;
```

This ensures that the class destructor is called for each object in the array. Note that older compilers required the following:

```
delete [5] eptr;
```

Our next example also creates a dynamic array of class objects on the heap. This time, however, not only is an array of pointers created on the heap, but the Elevator objects that the pointers point to are also created on the heap.

```
// e5.cpp

#include <iostream>
#include "elevator.h"

using namespace std;

int main() {
    int i;
    Elevator **eptr;

    eptr = new Elevator *[5];
    for (i = 0; i < 5; i++)
        eptr[i] = new Elevator;
    for (i = 0; i < 5; i++)
        cout << eptr[i]->getFloor() << endl;
    for (i = 0; i < 5; i++)
        delete eptr[i];
    delete [] eptr;
}
```

Below is a representation of the dynamic array created in the above program:

created on stack   created on heap   created on heap

eptr =======> 0 | . -------> [Elevator object]
             1 | . -------> [Elevator object]
             2 | . -------> [Elevator object]
             3 | . -------> [Elevator object]
             4 | . -------> [Elevator object]

## Dynamic Memory Allocation

Like the `malloc()` function in C, the C++ keyword `new` is used to allocate contiguous memory at execution time. In its simplest form, we use the keyword `new` followed by whatever type of data you want to allocate.

```
char *p = new char; // allocates a single char
int *p = new int; // allocates an int
double *p = new double; // allocates a single double
```

Unlike `malloc()`, you no longer need to use the `sizeof` keyword to specify the exact number of bytes needed. Instead, you merely specify a particular type, either fundamental or user-defined. The fact that different types occupy different amounts of storage is handled automatically by the compiler.

When allocating an object of type T with the `new` operator, a first argument of `sizeof(T)` is automatically supplied to this function. If `operator new()` cannot allocate the requested amount of heap space, it returns a pointer whose value is zero. If `operator new()` successfully allocates storage on the heap, then it returns the address of this space which is converted to a pointer to the type being allocated.

Because it's so important to be able to initialize variables and objects in C++, fundamental types allocated from the heap via `new` can be initialized with some value by enclosing the value within parentheses immediately after the type name.

```
char *p = new char ('A'); // allocates a single char
int *p = new int(65); // allocates an int
double *p = new double(5.2); // allocates a single double
```

## Memory Allocation for an Array of a Fundamental Type

To allocate memory for an array of some fundamental type, we use the keyword `new`, the type name, and the number of array elements enclosed within square brackets. This number can be either a constant or some expression whose value
