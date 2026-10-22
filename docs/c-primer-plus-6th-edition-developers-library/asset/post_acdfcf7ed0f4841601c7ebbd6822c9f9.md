
The amount of memory needed for the static duration storage classes is known at compile time, and the data stored in this section is available as long as the program runs. Each variable of these classes comes into being when the program starts and expires when the program ends.

An automatic variable, however, comes into existence when a program enters the block of code containing the variable's definition and expires when its block of code is exited. Therefore, as a program calls functions and as functions terminate, the amount of memory used by automatic variables grows and shrinks. This section of memory is typically handled as a stack. That means new variables are added sequentially in memory as they are created and then are removed in the opposite order as they pass away.

Dynamically allocated memory comes into existence when malloc() or a related function is called, and it's freed when free() is called. Memory persistence is controlled by the programmer, not by a set of rigid rules, so a memory block can be created in one function and disposed of in another function. Because of this, the section of memory used for dynamic memory allocation can end up fragmented—that is, unused chunks could be interspersed among active blocks of memory. Also, using dynamic memory tends to be a slower process than using stack memory.

Typically, a program uses different regions of memory for static objects, automatic objects, and dynamically allocated objects. Listing 12.15 illustrates this point.

## Listing 12.15 The where.c Program

```
// where.c -- where's the memory?

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int static_store = 30;
const char * pcg = "String Literal";
int main()
{
    int auto_store = 40;
    char auto_string[] = "Auto char Array";
    int * pi;
    char * pcl;

    pi = (int *) malloc(sizeof(int));
    *pi = 35;
    pcl = (char *) malloc(strlen("Dynamic String") + 1);
    strcpy(pcl, "Dynamic String");

    printf("static_store: %d at %p\n", static_store, &static_store);
    printf("  auto_store: %d at %p\n", auto_store, &auto_store);
    printf("         *pi: %d at %p\n", *pi, pi);
    printf(" %s at %p\n", pcg, pcg);
    printf(" %s at %p\n", auto_string, auto_string);
    printf(" %s at %p\n", pcl, pcl);
    printf("  %s at %p\n", "Quoted String", "Quoted String");
    free(pi);
    free(pcl);

    return 0;
}
```

Here is the output for one system:

```
static_store: 30 at 00378000
  auto_store: 40 at 0049FB8C
    *pi: 35 at 008E9BA0
String Literal at 00375858
Auto char Array at 0049FB74
Dynamic String at 008E9BD0
  Quoted String at 00375908
```

As you can see, static data, including string literals, occupies one region, automatic data a second region, and dynamically allocated data a third region (often called a memory heap or free store).

## ANSI C Type Qualifiers

You’ve seen that a variable is characterized by both its type and its storage class. C90 added two more properties: constancy and volatility. These properties are declared with the keywords const and volatile, which create qualified types. The C99 standard added a third qualifier, restrict, designed to facilitate compiler optimizations. And C11 adds a fourth, _Atomic. C11 provides an optional library, managed by stdatomic.h, to support concurrent programming, and _Atomic is part of that optional support.

C99 granted type qualifiers a new property—they now are idempotent! Although this sounds like a powerful claim, all it really means is that you can use the same qualifier more than once in a declaration, and the superfluous ones are ignored:

```
const const const int n = 6; // same as const int n = 6;
```

This makes it possible, for example, for the following sequence to be accepted:

```
typedef const int zip;
const zip q = 8;
```

### The `const` Type Qualifier

Chapter 4, “Character Strings and Formatted Input/Output,” and Chapter 10, “Arrays and Pointers,” have already introduced const. To review, the const keyword in a declaration establishes a variable whose value cannot be modified by assignment or by incrementing or decrementing. On an ANSI-compliant compiler, the code

```
const int nochange;    /* qualifies m as being constant */
nochange = 12;         /* not allowed                 */
```

should produce an error message. You can, however, initialize a const variable. Therefore, the following code is fine:

```
const int nochange = 12;   /* ok */
```

The preceding declaration makes nochange a read-only variable. After it is initialized, it cannot be changed.

You can use the const keyword to, for example, create an array of data that the program can’t alter:

```
const int days[12] = {31,28,31,30,31,30,31,31,30,31,30,31};
```

### Using const with Pointers and Parameter Declarations

Using the const keyword when declaring a simple variable and an array is pretty easy. Pointers are more complicated because you have to distinguish between making the pointer itself const and making the value that is pointed to const. The declaration

```
const float * pf;   /* pf points to a constant float value */
```

establishes that pf points to a value that must remain constant. The value of pf itself can be changed. For example, it can be set to point at another const value. In contrast, the declaration

```
float * const pt;    /* pt is a const pointer */
```

says that the pointer pt itself cannot have its value changed. It must always point to the same address, but the pointed-to value can change. Finally, the declaration

```
const float * const ptr;
```

means both that ptr must always point to the same location and that the value stored at the location must not change.

There is a third location in which you can place const:

```
float const * pfc;    // same as const float * pfc;
```

As the comment indicates, placing const after the type name and before the * means that the pointer can’t be used to change the pointed-to value. In short, a const anywhere to the left

The second approach is to place the constants in an include file. Here, you must take the additional step of using the static external storage class:

```
/* constant.h -- defines some global constants */
static const double PI = 3.14159;
static const char * MONTHS[12] =
    {"January", "February", "March", "April", "May", "June", "July",
     "August", "September", "October", "November", "December"};

/* file1.c -- use global constants defined elsewhere */
#include "constant.h"

/* file2.c -- use global constants defined elsewhere */
#include "constant.h"
```

If you don’t use the keyword static, including constant.h in file1.c and in file2.c would result in each file having a defining declaration of the same identifier, which is not supported by the C standard. (Some compilers, however, do allow it.) By making each identifier static external, you actually give each file a separate copy of the data. That wouldn’t work if the files are supposed to use the data to communicate with one another because each file would see only its own copy. Because the data is constant (by using the const keyword) and identical (by having both files include the same header file), however, that’s not a problem.

The advantage of the header file approach is that you don’t have to remember to use defining declarations in one file and reference declarations in the next; all files simply include the same header file. The disadvantage is that the data is duplicated. For the preceding examples, that’s not a real problem, but it might be one if your constant data includes enormous arrays.

### The volatile Type Qualifier

The volatile qualifier tells the compiler that a variable can have its value altered by agencies other than the program. It is typically used for hardware addresses and for data shared with other programs or threads running simultaneously. For example, an address might hold the current clock time. The value at that address changes as time changes, regardless of what your program is doing. Or an address could be used to receive information transmitted from, say, another computer.

The syntax is the same as for const:

```
volatile int loc1;  /* loc1 is a volatile location */
volatile int * ploc; /* ploc points to a volatile location */
```

These statements declare loc1 to be a volatile value and ploc to point to a volatile value.

You may think that volatile is an interesting concept, but you might be wondering why the ANSI committee felt it necessary to make volatile a keyword. The reason is that it facilitates compiler optimization. Suppose, for example, you have code like this:
