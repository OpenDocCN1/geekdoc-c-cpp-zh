# Listing 5.39: Showing the Const Parameter in C

```
```c
#include<stdio.h>
void checkFunc(const int varA);
int main()
{
    const int varA = 10;
    checkFunc(10);
    getch();
    return 0;
}
void checkFunc(const int varA)
{
    printf("\n variable passed [%d] ",varA);
    varA++;
}
```
```

Compilation error is shown as follows:

```
```
In function 'checkFunc': increment of read-only location
```
```

Many standard library functions, such as strlen() and strchr(), have a const type qualifier for the string arguments that are passed to them. It indicates that the functions would not modify the content of the string passed to them.

A general form for declaring const variables is as follows:

```
```c
const int varA = 10;
```
```

The following alternative form is also acceptable, since the order of type specifiers and qualifiers does not matter:

```
```c
int const varA = 5;
```
```

Order becomes important when composite types with pointers are used, shown as follows:

```
```c
int * const ptr = &i; /* const pointer to int */
const int * ptr_1; /* pointer to const int */
int const * ptr_1; /* pointer to const int */
```
```

The pointer ptr is itself a const, that is, the pointer cannot be modified. However, the integer variable it points to can be modified, that is, pointer ptr_1 can be modified, but the variable it points to cannot.

Casting away the const-ness (type casting a const variable into a non-const one) is possible, but considered dangerous. Modifying a const-qualified variable is not only dangerous, but may even lead to runtime errors, if the values are placed in the read-only storage, shown as follows:

```
```c
const int * ptci;
int *pti, i;
const int ci;
ptci = pti = &i;
*ptci = 5; /* Compiler error */
*pti = 5; /* OK, but dangerous */
pti = &ci; /* Compiler error */
pti = ptci; /* Compiler error */
pti = (int *)&ci; /* OK, but dangerous */
*pti = 5; /* OK, dangerous and potential runtime error */
```
```

# *volatile*

The volatile type qualifier tells the compiler that the value of the variable can be changed outside its current scope. Consider a scenario where the address of a global variable is passed to the operating system's clock routine and is used to hold the system time. In such a situation, the content of the variable will be altered without any explicit assignment statements in the code. The C compiler automatically optimize certain