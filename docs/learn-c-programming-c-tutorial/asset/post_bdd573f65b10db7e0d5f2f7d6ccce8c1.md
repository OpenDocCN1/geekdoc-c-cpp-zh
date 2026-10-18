
## Return Array from a Function

C programming does not allow to return an entire array as an argument to a function. However, you can return a pointer to an array by specifying the array's name without an index.

![](img/6e49c39a6ef9e32d938b03dc613e44f6_104_0.png)

If you want to return a single-dimension array from a function, you would have to declare a function returning a pointer as in the following example:

```
int * myFunction()
{

}
```

Second point to remember is that C does not advocate to return the address of a local variable to outside of the function, so you would have to define the local variable as static variable.

Now, consider the following function which will generate 10 random numbers and return them using an array and call this function as follows:

```
#include <stdio.h>

/* function to generate and return random numbers */
int * getRandom( )
{
static int r[10];
int i;

/* set the seed */
srand( (unsigned)time( NULL ) );
for ( i = 0; i < 10; ++i)
{
r[i] = rand();
printf( "r[%d] = %d\n", i, r[i]);
}

return r;
}
/* main function to call above defined function */
```

![](img/6e49c39a6ef9e32d938b03dc613e44f6_105_0.png)

[PAGE 106]

```
int main ()
{
    /* a pointer to an int */
    int *p;
    int i;

    p = getRandom();
    for ( i = 0; i < 10; i++ )
    {
    printf( "*(p + %d) : %d\n", i, *(p + i));
    }

    return 0;
}
```

When the above code is compiled together and executed, it produces the following result:

```
r[0] = 313959809
r[1] = 1759055877
r[2] = 1113101911
r[3] = 2133832223
r[4] = 2073354073
r[5] = 167288147
r[6] = 1827471542
r[7] = 834791014
r[8] = 1901409888
r[9] = 1990469526
*(p + 0) : 313959809
*(p + 1) : 1759055877
*(p + 2) : 1113101911
*(p + 3) : 2133832223
*(p + 4) : 2073354073
*(p + 5) : 167288147
*(p + 6) : 1827471542
*(p + 7) : 834791014
```

![](img/6e49c39a6ef9e32d938b03dc613e44f6_106_0.png)

[PAGE 107]

[PAGE 108]

```
```c
printf( "Array values using pointer\\n");
for ( i = 0; i < 5; i++ )
{
    printf("*(p + %d) : %f\\n", i, *(p + i) );
}

printf( "Array values using balance as address\\n");
for ( i = 0; i < 5; i++ )
{
    printf("*(balance + %d) : %f\\n", i, *(balance + i) );
}

return 0;
}
```
```

When the above code is compiled and executed, it produces the following result:

```
```text
Array values using pointer

*(p + 0) : 1000.000000

*(p + 1) : 2.000000

*(p + 2) : 3.400000

*(p + 3) : 17.000000

*(p + 4) : 50.000000

Array values using balance as address

*(balance + 0) : 1000.000000

*(balance + 1) : 2.000000

*(balance + 2) : 3.400000

*(balance + 3) : 17.000000

*(balance + 4) : 50.000000
```
```

In the above example, p is a pointer to double, which means it can store the address of a variable of double type. Once we have the address in p, *p will give us the value available at the address stored in p, as we have shown in the above example.

[PAGE 109]

# 15. POINTERS

Pointers in C are easy and fun to learn. Some C programming tasks are performed more easily with pointers, and other tasks, such as dynamic memory allocation, cannot be performed without using pointers. So it becomes necessary to learn pointers to become a perfect C programmer. Let's start learning them in simple and easy steps.

As you know, every variable is a memory location and every memory location has its address defined which can be accessed using ampersand (&) operator, which denotes an address in memory. Consider the following example, which prints the address of the variables defined:

```
```c
#include <stdio.h>

int main ()
{
    int var1;
    char var2[10];

    printf("Address of var1 variable: %x\n", &var1 );
    printf("Address of var2 variable: %x\n", &var2 );

    return 0;
}
```
```

When the above code is compiled and executed, it produces the following result:

```
```text
Address of var1 variable: bff5a400

Address of var2 variable: bff5a3f6
```
```

# What are Pointers?

A **pointer** is a variable whose value is the address of another variable, i.e., direct address of the memory location. Like any variable or constant, you must declare a pointer before using it to store any variable address. The general form of a pointer variable declaration is:

![](img/6e49c39a6ef9e32d938b03dc613e44f6_109_0.png)

[PAGE 110]

<!-- no content -->

[PAGE 111]

```
```c
/* access the value using the pointer */
printf("Value of *ip variable: %d\n", *ip );

return 0;
}
```
```

When the above code is compiled and executed, it produces the following result:

```
```
Address of var variable: bffd8b3c

Address stored in ip variable: bffd8b3c

Value of *ip variable: 20
```
```

# NULL Pointers

It is always a good practice to assign a NULL value to a pointer variable in case you do not have an exact address to be assigned. This is done at the time of variable declaration. A pointer that is assigned NULL is called a **null pointer**.

The NULL pointer is a constant with a value of zero defined in several standard libraries. Consider the following program:

```
```c
#include <stdio.h>

int main ()
{
    int *ptr = NULL;

    printf("The value of ptr is : %X\n", ptr );

    return 0;
}
```
```

When the above code is compiled and executed, it produces the following result:

```
```
The value of ptr is 0
```
```

In most of the operating systems, programs are not permitted to access memory at address 0 because that memory is reserved by the operating system. However, the memory address 0 has special significance; it signals that the pointer is not intended to point to an accessible memory location. But by convention, if a pointer contains the null (zero) value, it is assumed to point to nothing.

[PAGE 112]

To check for a null pointer, you can use an `if` statement as follows:

```
if(ptr)    /\* succeeds if p is not null \*/
if(!ptr)    /\* succeeds if p is null \*/
```

# Pointers in Detail

Pointers have many but easy concepts and they are very important to C programming. The following important pointer concepts should be clear to any C programmer:

\begin{tabular}{cc}
**Concept** & **Description** \\
Pointer arithmetic & There are four arithmetic operators that can be used in pointers: ++, --, +, - \\
Array of pointers & You can define arrays to hold a number of pointers. \\
Pointer to pointer & C allows you to have pointer on a pointer and so on. \\
Passing pointers to functions in C & Passing an argument by reference or by address enable the passed argument to be changed in the calling function by the called function. \\
Return pointer from functions in C & C allows a function to return a pointer to the local variable, static variable, and dynamically allocated memory as well. \\
\end{tabular}

# Pointer Arithmetic

A pointer in C is an address, which is a numeric value. Therefore, you can perform arithmetic operations on a pointer just as you can on a numeric value. There are four arithmetic operators that can be used on pointers: ++, --, +, and -

To understand pointer arithmetic, let us consider that ptr is an integer pointer which points to the address 1000. Assuming 32-bit integers, let us perform the following arithmetic operation on the pointer:

![](img/6e49c39a6ef9e32d938b03dc613e44f6_112_0.png)

[PAGE 113]

```
```c
ptr++
```
```

After the above operation, the **ptr** will point to the location 1004 because each time ptr is incremented, it will point to the next integer location which is 4 bytes next to the current location. This operation will move the pointer to the next memory location without impacting the actual value at the memory location. If **ptr** points to a character whose address is 1000, then the above operation will point to the location 1001 because the next character will be available at 1001.

# Incrementing a Pointer

We prefer using a pointer in our program instead of an array because the variable pointer can be incremented, unlike the array name which cannot be incremented because it is a constant pointer. The following program increments the variable pointer to access each succeeding element of the array:

```
```c
#include <stdio.h>

const int MAX = 3;

int main ()
{
    int var[] = {10, 100, 200};
    int i, *ptr;

    /* let us have array address in pointer */
    ptr = var;
    for ( i = 0; i < MAX; i++)
    {
        printf("Address of var[%d] = %x\n", i, ptr );
        printf("Value of var[%d] = %d\n", i, *ptr );

        /* move to the next location */
        ptr++;
    }
    return 0;
}
```
```
