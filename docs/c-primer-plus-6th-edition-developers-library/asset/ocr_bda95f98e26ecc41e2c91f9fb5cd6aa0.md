Just as with arrays, a regular initializer following a designated initializer provides a value for the member following the designated member. Also, the last value supplied for a particular member is the value it gets. For example, consider this declaration:

```
struct book gift= { .value = 18.90,
    .author = "Philionna Pestle",
    0.25};
```

The value 0.25 is assigned to the value member because it is the one immediately listed after the author member in the structure declaration. The new value of 0.25 supersedes the value of 18.90 provided earlier. Now that you have these basics in hand, you’re ready to expand your horizons and look at several ramifications of structures. You’ll see arrays of structures, structures of structures, pointers to structures, and functions that process structures.

# Arrays of Structures

Let’s extend our book program to handle more books. Clearly, each book can be described by one structure variable of the book type. To describe two books, you need to use two such variables, and so on. To handle several books, you can use an array of such structures, and that is what we have created in the next program, shown in Listing 14.2. (If you’re using Borland C/C++, see section “Borland C and Floating Point” later in the chapter.)

# Structures and Memory

The manybook.c program uses an array of 100 structures. Because the array is an automatic storage class object, the information is typically placed on the stack. Such a large array requires a good-sized chunk of memory, which can cause problems. If you get a runtime error, perhaps complaining about the stack size or stack overflow, your compiler probably uses a default size for the stack that is too small for this example. To fix things, you can use the compiler options to set the stack size to 10,000 to accommodate the array of structures, or you can make the array static or external (so that it isn’t placed in the stack), or you can reduce the array size to 16. Why didn’t we just make the stack small to begin with? Because you should know about the potential stack size problem so that you can cope with it if you run into it on your own.

# Listing 14.2 The manybook.c Program

```
/* manybook.c -- multiple book inventory */
#include <stdio.h>
#include <string.h>
char * s_gets(char * st, int n);
#define MAXTITL  40
#define MAXAUTL  40
#define MAXBKS   100        /* maximum number of books  */
```