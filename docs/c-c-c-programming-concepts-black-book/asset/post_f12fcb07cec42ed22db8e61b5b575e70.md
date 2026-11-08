
Listing 2.29 shows external linkage in C:

### Listing 2.29: External Linkage in C

```c
#include<stdio.h>

int main()
{
    extern int varA;
    printf("\n The value of the variable is [%d] ",varA);
    getch();
    return 0;
}

int varA = 10;
```

The output of Listing 2.29 is given as follows:

```text
The value of the variable is [10]
```

The output of the program is 10, because the global variable “varA” is assigned a value of 10. Note that the extern keyword is used in this program because the varA variable is getting accessed before its declaration in the main function. If the compiler finds an undeclared variable inside the current scope, it checks for a match with all the variables inside the enclosed block. After that, the compiler tries to find a match with the global variables. Extern allows us to declare a variable without defining it. If we provide an initialization for the same variable, then the extern declaration becomes a definition for that variable.

Another important usage of the extern storage class specifier is in multi-file programming. It might happen that a program spans through two separate files that are compiled separately but linked together. In such cases, the only way of letting the compiler know about the presence of global variables is by using the extern keyword. Assume that we have two files, File_1 and File_2. A variable has been declared as a global variable in File_1 and has been modified inside it. If we want to use the same variable inside File_2 and also with the same value, then we need to declare the variable inside File_2 as the extern variable and use it. The extern keyword will notify the compiler that the variable name that follows the extern keyword is declared elsewhere in the program so it will take up the one declared inside File_1.

To understand the flow of a global variable from one file to another, we need to create a multi-file project in C which will have multiple source files with a common header. The header contains the global variable and a common display function, which is used to print the global variable. In our example, the header is defined in Listing 2.30:

### Listing 2.30: Multifile Programming in C

```c
/* test.h */

/* Header file that contains the global variable */

int global_var = 10;

void display_file1();

void display()
{
    printf("\n global variable [%d]",global_var);
    return;
}
```

The following source files, Source file 1 and Source file 2, are included in the project:

```c
/* Source file 1 */

#include<stdio.h>

extern int global_var;

void display_file1()
{
    global_var++;
    display();
    return;
}
/* Source file 2 */

#include<stdio.h>

extern int global_var;

void display_file2()
{
    global_var++;
    display();
    return;
}
```

The following main module is also included:

```c
/* The main module */

#include <stdio.h>
#include <stdlib.h>
#include "test.h"

int main(int argc, char *argv[])
{
    display();
    display_file1();
    display_file2();
    getch();
    return 0;
}
```

Both the source files use the global variable “global_var” and increments it with 1 before displaying the variable. Inside the main module, we call two different functions “display_file1()” and “display_file2()”, which are defined in the source files 1 and 2, respectively.

The output of Listing 2.30 is given as follows:

```text
global variable [10]
global variable [11]
global variable [12]
```

In Listing 2.30, inside the main function, first the common display function defined inside the header gets called. This function displays the global variable. In the first case, no change has yet been made to the global variable so we get the value as 10. Next “display_file1()” gets called which is defined inside the source file 1. Inside the source file, the global variable gets referenced with the extern keyword and then the value gets incremented by 1. When the common display function gets called from source file 1, we get a value of 11 due to the increment that was made. After the control comes back to the main module, “display_file2()” is invoked which is defined inside the source file 2. The same thing repeats for source file 2 and as the global variable already had a value of 11 inside it, the next value displayed was 12. This variable can be used to transfer values from one file to another by using the extern keyword.

## Static Storage Class

Static storage class specifier is used for creating permanent variables. Once variables are declared static within a function or a file, they maintain their values between function calls. If variables are declared static inside a function, they have the same scope as that of an automatic variable. The major difference between an automatic and static variable is that a static variable retains its value throughout the lifetime of the program. If control is returned from a function and then the function is again called, static variables defined within that function will retain their former values.

### Static Local Variables

When a static storage class specifier is used against a local variable defined within a function, then a permanent storage gets created for that variable. The static keyword ensures that the variable will retain its values in between function calls. Listing 2.31 shows the non-static storage class specification in C.

### Listing 2.31: Non Static Storage Class Specification in C

```c
#include<stdio.h>

void display();

int main()
{
    int i;

    for(i=0; i < 5; i++)
    {
        display();
    }
    getch();

}

void display()
{
    int x = 1;
    printf("\n Value of x is [%d] ",x);
    x++;
}
```

The output of Listing 2.31 is given as follows:

```text
Value of x is [1]
Value of x is [1]
Value of x is [1]
Value of x is [1]
Value of x is [1]
```

Every time, the call to the display() function is being made, the x variable gets reinitialized to 1, which is the reason for the output that we are getting. If the same code is re-written using a static keyword then it would look like, as shown in Listing 2.32:

### Listing 2.32: Static Storage Class Specification in C

```c
#include<stdio.h>

void display();

int main()
{
    int i;

    for(i=0; i < 5; i++)
    {
        display();
    }
    getch();
}

void display()
{
        static int x = 1;

        printf("\n Value of X is [%d] ",x);
        x++;
}
```

The output of Listing 2.32 is given as follows:

```text
Value of X is [1]
Value of X is [2]
Value of X is [3]
Value of X is [4]
Value of X is [5]
```

The static storage class specifier makes the content of the local variable permanent. The initialization takes place only once, that is when the display() function is called for the first time, the successive calls to the function use the value that was formerly incremented. There can be multiple use cases for static variables. Consider a scenario where we need to generate a number which would be determined from the value of the previous iteration. One of the ways of solving this issue could be through global variables. However, it might happen that some other function accesses that variable and modifies its value before the actual purpose is fulfilled. To avoid such scenarios, static variables are best solutions that one can use.

### Static Global Variables

If we apply a static specifier to a global variable, it instructs the compiler to create a global variable which will be only known inside that file in which it is declared. Unlike extern, a static global variable has an internal linkage. Even though the variable is declared as a global variable, functions and routines present in other files do not have any access to that variable.

In spite of all the advantages that a static specifier provides, it has some disadvantages. Static variables are also defined as permanent variables and their values are kept in memory even when the variable is not getting accessed, which can eventually lead to memory wastage.
