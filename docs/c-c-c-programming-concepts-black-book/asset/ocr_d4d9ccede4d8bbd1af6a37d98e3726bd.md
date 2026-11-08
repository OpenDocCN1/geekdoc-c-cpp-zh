Listing 2.16 shows an example of the old style function declaration in C:

**Listing 2.16: Old Style of Function Declaration**

```
```c
#include<stdio.h>

int myFunc();        /* Old Style of Function Declaration */

int main()
{
    printf("\n Ret = %d ",myFunc(10,20));
    getch();
}

int myFunc(int x, int y)    /* Function Definition */
{
    return x;               /* Function Body */
}
```
```

In Listing 2.16, the old style of function declaration tells the compiler that the myFunc function returns a variable whose type is integer. It does not say anything about the number and type of arguments that are passed to the function. The old style of function declaration has a generic form, as mentioned in the following code snippet:

```
```c
data-type function_name();
```
```

The old style of function declaration is not used nowadays as the style doesn't say anything about the number of argument's so it's less reliable to use..

# ## Standard Library Function Prototypes

The standard library functions must have their prototypes declared before using them in the C language. In order to achieve this, we need to include header files in our code. All appropriate headers for standard library functions are provided by the C compiler. The function prototypes for the standard library functions are mentioned in the header files in C. The library headers are the files that end with a .h extension. The library headers contain the library function definitions and their prototypes. The stdio header contains the definition and prototype for "printf()", "scanf()", and lots of other standard library functions, so we need to include the stdio header whenever we write any code in C. More header files and standard library functions are discussed in the latter half of the book.

# ## Variable Length Parameter List

C enables its users to declare functions that take variable number of parameters as arguments. Let's take an example of a common standard library function "printf()". This function is capable of handling variable arguments. In order to tell the compiler that the function will be able to handle variable argument list, the function prototype must contain three dots (periods) in its parameter list, as shown in the following code snippet:

```
```c
int myFunc(int x, float y, ...);
```
```

The preceding code snippet tells the compiler that myFunc function will take at least one integer and one float variable and an undetermined number of arguments after that. A function that uses the variable argument list must also contain at least one actual argument as its parameter. The code snippet mentioned below shows an erroneous variable length parameter list:

```
```c
int myFunc( ... );
```
```