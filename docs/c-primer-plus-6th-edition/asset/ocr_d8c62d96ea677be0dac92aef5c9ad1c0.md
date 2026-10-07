# 158 Chapter 4 Compound Types

This emphasizes the idea that int* is a type, pointer-to-int.Where you put the spaces makes no difference to the compiler.You could even do this:

```
int *ptr;
```

Be aware, however, the following declaration creates one pointer (p1) and one ordinary int (p2):

```
int* p1, p2;
```

You need an * for each pointer variable name.

> Note
 C++, the combination int * is a compound type, pointer-to-int.

You use the syntax to declare pointers to other types:

```
double *tax_ptr; // tax_ptr points to type double
char * str; // str points to type char
```

Because you declare tax_ptr as a pointer-to-double, the compiler knows that *tax_ptr is a double value.That is, it is known that *tax_ptr represents a number in floating-point format that occupies (on most systems) 8 bytes. A pointer variable is never a pointer. It is always a pointer to a specific type.tax_ptr (or double *), and str is type pointer-to-char (or char *). Although both are pointers, they are pointers of two different types. Like arrays, pointers are based on other types.

Note where tax_ptr and str point to data types of two different sizes, the two variables tax_ptr and str themselves are the same size. That, the address of a char is the same size as the address of a double, much as 1016 might be the street address of a department store, where 1024 could be the street address of a small cottage. The size or value of an address doesn't tell you about the size or kind of variable or building you find at address. Usually, addresses require 2 or 4 bytes, depending on the computer system. (Some systems have larger addresses, and a system can use different addresses for different types).

You can use a declaration to initialize a pointer. In that case, the pointer, not the pointed-to, is initialized. That is, the following statements set pt and *pt to the value higgens:

```
int higgens = 5;
int *pt = &higgens;
```

Listing 4.16 how to initialize a pointer to an address.

# Listing 4.16 init_ptr.cpp

```
// init_ptr.cpp -- initialize a pointer
#include <iostream>
int main()
{
```