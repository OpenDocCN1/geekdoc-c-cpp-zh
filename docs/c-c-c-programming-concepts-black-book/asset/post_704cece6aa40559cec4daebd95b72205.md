
## Chapter 2

Listing 2.11 shows an example of a function without prototypes:

### Listing 2.11: Functions Without Prototypes

```c
#include<stdio.h>

float myFunc(float x)
{
        return x*3.5;
}

int main()
{
        float ret;

        ret = myFunc(87.67);
        printf("\n Ret [%f] ",ret);
        getch();
}
```

The output of Listing 2.11 is given as follows:

```
Ret [306.845001]
```

Listing 2.12 shows an example where a function is accessed before its definition:

### Listing 2.12: Accessing Function before its Definition

```c
#include<stdio.h>

int main()
{
        float ret;

        ret = myFunc(87.67);
        printf("\n Ret [%f] ",ret);
        getch();
}

float myFunc(float x)
{
        return x*3.5;
}
```

The output of Listing 2.12 is given as follows:

```
conflicting types for 'myFunc'
previous implicit declaration of 'myFunc' was here
```

The compilation error is thrown as the function is getting accessed prior to its definition. Generally, when a function is defined or is accessed, the compiler knows about the signature of the function. However, in our case, the function is accessed before it is defined, so the compiler fails to find a signature for the function. Function prototypes are designed to solve such issues and are written at the beginning of the program ahead of any user-defined functions (including main). The following code snippet shows the general form of a function prototype:

```c
data-type name(type 1, arg 1, type 2, arg 2, ..., type n, arg n);
```

In the preceding code snippet, the data-type represents the data type of the item that is getting returned by the function, name represents the name of the function, type 1, type 2, ..., type n represent the data type of the arguments arg 1, arg 2, ..., arg n. The function prototype resembles the first line of the function definition. One of the major differences between a function prototype and that of a function definition is that a function prototype always terminates with a semicolon; whereas, a function definition does not. The argument names given within the function prototype definition just plays the role of a dummy variable and can be omitted while writing a prototype. A function prototype declaration makes the compiler understand the signature of the function beforehand. When a compiler executes a function prototype, it comes to know that a function with a similar signature is getting used in the program. If the prototype of a function is declared, then the compiler would not throw any compilation error in case the function is accessed prior to its definition.

A function prototype helps the user to figure out if any mismatch takes place between a function prototype and function definition. In case of a mismatch, a compilation error occurs.

Listing 2.13 shows the usage of function prototypes:

### Listing 2.13: Writing Functions with Prototypes

```c
#include<stdio.h>

float myFunc(float x);        /* Function Prototype */

int main()
{
    float ret;

    ret = myFunc(87.67);
    printf("\n Ret [%f] ",ret);  /* Function Call */
    getch();
}

float myFunc(float x)    /* Function Definition */
{
    return x*3.5;        /* Function Body */
}
```

The output of Listing 2.13 is given as follows:

```
Ret [306.845001]
```

It is not mandatory for a function prototype to contain name of a variable as defined above. The following code snippet shows an example of the function prototype:

```c
float myFunc(float);        /* Function Prototype */
```

Although, main is a function, it does require a function prototype. Please note that main is the first function to be called in a C program; in fact, we can say that a C program starts with the main function. As main is the first function that gets called in a C program, therefore, it is necessary to define the main function before accessing it in a C program.

Both C and C++ handle prototypes in different ways. In C++, an empty parameter list is used to signify that the function does not take any argument, for example:

```c
int myFunction();   /* C++ Prototype declaration for a function with no parameters */
```

However, the empty parameter list of a function prototype in C does not always signify that the function is not going to take up any parameters. This style of prototyping in C is known as the old style of prototyping.

Listing 2.14 shows an example of the old type prototyping:

### Listing 2.14: Old Style of Prototyping in C

```c
#include<stdio.h>

int myFunc();        /* Function Prototype */

int main()
{
    printf("\n Ret = %d ",myFunc(10,20));
    getch();
}

int myFunc(int x, int y)      /* Function Definition */
{
    return x;      /* Function Body */
}
```

The output of Listing 2.14 is given as follows:

```
Ret = 10
```

In the code mentioned in Listing 2.14, we have declared a prototype of a function with an empty parameter list but while accessing the function from the main function, we have passed multiple parameters in it. In spite of passing parameters to a function with an empty parameter list, the code given in Listing 2.14 is compiled without error. In C, the empty argument list does not signify how many arguments the function actually takes, so debugging and error handling become even more difficult with such declarations. The proper way of declaring a function prototype with no arguments is done with the void keyword, as shown in the following code snippet:

```c
int myFunction(void);  /* C Prototype declaration for a function with no parameters */
```

Listing 2.15 shows an alternative way in which the preceding code can be written using the correct prototyping:

### Listing 2.15: Correct Prototyping in C

```c
#include<stdio.h>

int myFunc(void);          /* Function Prototype */

int main()
{
    printf("\n Ret = %d ",myFunc(10,20));
    getch();
}

int myFunc(int x, int y)     /* Function Definition */
{
    return x;      /* Function Body */
}
```

The output of Listing 2.15 is given as follows:

```
In function `main':
too many arguments to function `myFunc'
conflicting types for 'myFunc'
previous declaration of 'myFunc' was here
```

In Listing 2.15, the myFunc function has been declared with a void parameter. If any argument is passed to the myFunc function, then it should give a compilation error. This happens as the parameter list of myFunc is explicitly declared to be void.

### Old Style Function Declaration

Prior to function prototypes, C had a way of letting the compiler know of the data type being returned by a function. This method, also known as the old style function declaration, does not take into account the arguments that are being passed to the function or their types. Old style function declaration is done by using a function declaration that just contains the return type and the name of the function.

Listing 2.16 shows an example of the old style function declaration in C:

### Listing 2.16: Old Style of Function Declaration

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

In Listing 2.16, the old style of function declaration tells the compiler that the myFunc function returns a variable whose type is integer. It does not say anything about the number and type of arguments that are passed to the function. The old style of function declaration has a generic form, as mentioned in the following code snippet:

```c
data-type function_name();
```

The old style of function declaration is not used nowadays as the style doesn't say anything about the number of arguments, so it's less reliable to use.

### Standard Library Function Prototypes

The standard library functions must have their prototypes declared before using them in the C language. In order to achieve this, we need to include header files in our code. All appropriate headers for standard library functions are provided by the C compiler. The function prototypes for the standard library functions are mentioned in the header files in C. The library headers are the files that end with a .h extension. The library headers contain the library function definitions and their prototypes. The stdio header contains the definition and prototype for "printf()", "scanf()", and lots of other standard library functions, so we need to include the stdio header whenever we write any code in C. More header files and standard library functions are discussed in the latter half of the book.

### Variable Length Parameter List

C enables its users to declare functions that take variable number of parameters as arguments. Let's take an example of a common standard library function "printf()". This function is capable of handling variable arguments. In order to tell the compiler that the function will be able to handle variable argument list, the function prototype must contain three dots (periods) in its parameter list, as shown in the following code snippet:

```c
int myFunc(int x, float y, ...);
```

The preceding code snippet tells the compiler that myFunc function will take at least one integer and one float variable and an undetermined number of arguments after that. A function that uses the variable argument list must also contain at least one actual argument as its parameter. The code snippet mentioned below shows an erroneous variable length parameter list:

```c
int myFunc( ... );
```
