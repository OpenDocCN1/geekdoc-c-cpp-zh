```
/* intro2pointers.c: A simple example of a pointer in action. */
#include <stdio.h>
int main(void)
{
    int x = 420;
    int *p;                         /* p has type int * */

    printf("Value of x = %d\n", x);
    printf("Uninitialized value of pointer p = %p\n", p);
    p = &x;                         /* p stores address of x */
    printf("Initialized value of pointer p = %p\n", p);
    printf("Value at address pointed to by p = %d\n", *p);
    printf("This is the same value as x: %d\n", x);

    *p = 840;                       /* Same as x = 840; */
    printf("New value of x = %d\n", x);
    return 0;
}
```

# PROGRAM 12.1: `intro2pointers.c`

```
Value of x = 420
Uninitialized value of pointer p = 0xb7f1df60    %p prints in hex
Initialized value of pointer p = 0xbf1b163c     Address of x
Value at address pointed to by p = 420
This is the same value as x: 420
New value of x = 840
```

# PROGRAM OUTPUT: `intro2pointers.c`

only after it is made to point to a legal memory location. This can be the address of an int variable (say, x), which is obtained by using the & operator:

```
int x = 5;
p = &x;    *p stores the address of x
```

The & operator evaluates its operand (x) as an address. Expectedly, we can combine the declaration and assignment in this manner:

```
int *p = &x;    int* p = &x; is also OK
```

p has the data type int *, or pointer to int, which simply means that the value pointed to has the type int. Similarly, a float variable is pointed to by a pointer of type float * or pointer to float. However, the size of the pointer itself has no relation to the size of the variable pointed to. A pointer has a fixed size and its value is printed with the %p format specifier of printf.

After a pointer has been assigned a valid address with p = &x;, we can use the concept of indirection to obtain the value of x from p. The expression *p evaluates to x:

```
printf("Value of x is %d\n", *p);    Prints the value 5
```