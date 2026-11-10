```
```
}      /****** pgm1.c file ends ********/
/*******************************************/
/*      Program file: pgm2.c                */
/*******************************************/
extern int i;
/****** function definition of show() ********/
void show()        /*** function header ***/
{   /*** fn. body starts...*/
    printf("\n Value of i in pgm2.c=%d", i);
}       /*** fn. body ends... ***/
```
```

```
```
Output
Value of i in pgm2.c=10
Value of i in pgm1.c=10
```
```

Here is another example where the global variable i is assigned a value in the program file in which the basic declaration statement and main() are absent. There is a minor difference between this example and the previous one.

# EXAMPLE

```
```
22. /*******************************************/
    /*      Program file: pgm1.c                */
    /*******************************************/
#include <stdio.h>
#include "pgm2.c"  /* link program pgm2.c  */
int i;  /* external/global decl.*/
void show(void); /* function prototype ***/
int main()
{
    show(); /* call to function in program file pgm2.c */
    printf("\n Value of i in pgm1.c=%d", i);
    return 0;
} /****** pgm1.c file ends ********/
/*******************************************/
/*      Program file: pgm2.c                */
/*******************************************/
extern int i;
/****** function definition of show() ********/
void show()        /*** function header ***/
{   /*** fn. body starts...*/
    i = 20;
    printf("\n Value of i in pgm2.c=%d", i);
}       /*** fn. body ends... ***/
```
```

```
```
Output
Value of i in pgm2.c=20
Value of i in pgm1.c=20
```
```

# ### 12.8.2 Storage Class Specifiers for Functions

The only storage class specifiers that may be assigned with functions are extern and static. Extern signifies that

the function can be referenced from other files. that is, the function name is exported to the linker. Static signifies that the function cannot be referenced from other files, that is, the function name is not exported to the linker. If no storage class appears in a function definition, extern is presumed.

# ### 12.8.3 Linkage

An identifier's linkage determines which of the references to that identifier refers to the same object. An identifier's linkage is determined by whether it appears inside or outside a function, whether it appears in a declaration of a function (as opposed to an object), its storage-class specifier, and the linkage of any previous declarations of the same identifier that have file scope. C defines three types of linkages—external, internal, and no linkage. In general,

+   - Functions and global variables have external linkage. This means they are available to all files that constitute a program.
+   - Identifiers with file scope declared as static have internal linkage. These are known only within the file in which they are declared.
+   - Local identifiers have no linkage and are therefore known only within their own block.

Two declarations of the same identifier in a single file that have the same linkage, either internal or external, refer to the same object. The same identifier cannot appear in a file with both internal and external linkage.

> > **Note**
> >
> > - It is not always necessary to specify both the storage class and the type of identifiers in a declaration. Storage class specifiers appearing in declarations outside of functions are assumed to be extern. In a declaration inside a function, if a type but no storage class is indicated, the identifier is assumed to be auto. An exception to the latter rule is made for functions because functions with storage class auto do not exist; it is implicitly declared to be extern.

# ### 12.9 THE INLINE FUNCTION

C99 has added the keyword inline, which applies to functions. By preceding a function declaration with inline, the compiler is instructed to optimize calls to the function. Typically, this means that the function's code will be expanded in line, rather than called. Below is a definition of such inline function.

```
```
inline int sum(int x, int y)
{
    return x+y;
}
```
```

The inline designation is only a hint to the compiler, suggesting that calls to the inline function should be as fast as possible. The name comes from a compiler optimization