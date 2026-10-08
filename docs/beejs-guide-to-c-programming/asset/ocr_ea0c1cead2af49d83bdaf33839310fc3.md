# 35.4 Use Case: Arrays in Header Files

It can be useful to declare incomplete array types in header files. In those cases, the actual storage (where the complete array is declared) should be in a single .c file. If you put it in the .h file, it will be duplicated every time the header file is included.

So what you do make a header file with an incomplete type that refers to the array, like so:

```
// File: bar.h
#ifndef BAR_H
#define BAR_H

extern int my_array[]; // Incomplete type

#endif
```

And in the .c file, actually define the array:

```
// File: bar.c
int my_array[1024]; // Complete type!
```

Then you can include the header from as many places as you'd, and every one of places will refer to the same underlying my_array.

```
// File: foo.c
#include <stdio.h>
#include "bar.h" // includes the incomplete type for my_array

int main(void) {
    my_array[0] = 10;

    printf("%d\n", my_array[0]);
}
```

When compiling files, remember to specify all the .c files to the compiler, but not the .h files, e.g.:
gcc -o foo foo.c bar.c

# 35.5 Completing Incomplete Types

If you have an incomplete type, you can complete it by defining the complete struct, union, enum, or array in the same scope.

```
struct foo // incomplete type
struct foo *p; // pointer, no problem
struct foo foo; // Error: incomplete type

struct foo {
    int x, y, z;
};\ Now the struct foo is complete!

struct foo foo; // Success!
```