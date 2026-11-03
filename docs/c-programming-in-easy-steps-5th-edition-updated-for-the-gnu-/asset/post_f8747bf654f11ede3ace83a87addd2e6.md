
control returns from the custom function

```c
printf( "Lift Off!\n" );
```

- 7. At the end of the main function block, return a zero integer value, as required by the function declaration

```c
return 0 ;
```

![](img/db19f3858a1e321646bf2590afd29547_131_0.png)

The variable name must be preceded by the `&` address-of operator in the `scanf()` function, as described here.

- 8. After the main function block, begin the custom function definition with a statement to output the argument value passed during the function call

```c
void count_down_from( int num )
{
    printf( "%d\n", num );
}
```

- 9. Next, in the custom function block, decrement the value passed as the argument

```c
--num ;
```

- 10. Now, in the custom function block, add a conditional test to return control to the main function if the decremented value is below zero or pass it as an argument in a recursive call to this function

```c
if( num < 0 ) return ;
else
count_down_from( num );
```

- 11. Save the program file then compile and execute the program, inputting an integer when requested, to see the output from recursive function calls

![](img/db19f3858a1e321646bf2590afd29547_131_1.png)

```text
C:\MyPrograms>gcc recur.c -o recur.exe
C:\MyPrograms>recur
Enter a positive integer to count down from: 10
10
9
8
7
6
5
4
3
2
1
0
Lift off!!
C:\MyPrograms>_
```

![](img/db19f3858a1e321646bf2590afd29547_132_0.png)

![](img/db19f3858a1e321646bf2590afd29547_132_1.png)

A recursive function can be less efficient than using a loop.

## Placing functions in headers

The example programs listed throughout this book are necessarily small due to space considerations but in reality, most C programs will contain significantly more code.

When developing larger programs, some thought should be given to program structure. Maintaining the entire program code in a single file can become unwieldy as the program grows.

In order to simplify the program structure, a custom header file can be created to contain functions that may be used repeatedly. This should be named with a “.h” file extension, like the standard header files in the C library.

The functions in the custom header file can be made available to the program by adding an `#include` preprocessor directive at the start of the file containing the `main()` function. The custom header file name should be enclosed within double quotes in the preprocessor directive though, rather than by the `<` and `>` angled brackets that are used to include standard header files.

- 1. Create a custom header file named “utils.h” containing the definition of a single function

```c
int square( int num )
{
    return ( num * num );
}
```

![](img/db19f3858a1e321646bf2590afd29547_133_0.png)

- 2. Begin a new program with a preprocessor instruction to include the standard input/output library functions and the custom header file

```c
#include <stdio.h>
#include "utils.h"
```

**square.c**

- 3. Declare a custom function prototype with no arguments

```c
void getnum();
```

- 4. Add a main function to call the other function then return a zero integer as required by the declaration

```c
int main()
{
getnum();
return 0;
}
```

- 5. After the main function block, begin the second function definition by declaring two variables

```c
void getnum()
{
int num;
char again;
}
```

- 6. Next, in this function definition, add statements to request user input and assign its value to a variable

```c
printf("Enter an integer to be squared: ");
scanf("%d", &num);
```

- 7. Now, output the result by calling the function in the custom header file, passing it the input value as its argument

```c
printf("%d squared is %d\n", num, square(num));
```

- 8. Add a statement requesting further user input and assign its value to a variable

```c
printf("Square another number? Y or N: ");
scanf("%1s", &again);
```

- 9. Finally, add a conditional test to execute this function once more or return control to the main function

```c
if( (again == 'Y') || (again == 'y') ) getnum();
else return;
```

- 10. Save the program file then compile and execute the program, inputting an integer and character when requested, to see the output from the function calls

```text
C:\MyPrograms>gcc square.c -o square.exe
C:\MyPrograms>square
Enter an integer to be squared: 4
4 squared is 16
Square another number? Y or N: Y
Enter an integer to be squared: 5
5 squared is 25
Square another number? Y or N: Y
Enter an integer to be squared: 6
6 squared is 36
Square another number? Y or N: N
C:\MyPrograms>
```

![](img/db19f3858a1e321646bf2590afd29547_135_0.png)

The program file and custom header file must be located in the same directory but are compiled with the usual command – the compiler reads the header file automatically because of the `#include` directive.

![](img/db19f3858a1e321646bf2590afd29547_135_1.png)

Notice the use of the `%1s` format specifier in this example – to read the next character entered by the user.

## Restricting accessibility

The **static** keyword can be used to restrict the accessibility of functions to the file in which they are created, in exactly the same way that **static** variables have restricted accessibility. This is recommended practice in larger programs that are spread over multiple “.c” files, to safeguard against accidental misuse of functions. For instance, the **square()** and **multiply()** functions can’t be directly called from the **main()** function in this example.

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions

```c
#include <stdio.h>
```

![](img/db19f3858a1e321646bf2590afd29547_136_0.png)

- 2. Declare two custom function prototypes

```c
void menu();
void action( int option );
```

- 3. Add a main function to call the first custom function then return a zero integer as required by the declaration

```c
int main()
{
    menu();
    return 0 ;
}
```

- 4. After the main block, define the first custom function to pass a menu option as an argument to another function

```c
void menu()
{
    int option ;
    printf( "\n\tWhat would you like to do?" );
    printf( "\n\t1. Square a number" );
    printf( "\n\t2. Multiply two numbers" );
    printf( "\n\t3. Exit\n" );
    scanf("%d", &option);
    action( option );
}
```

- 5. Begin a second program file with a preprocessor to include the standard input/output functions, and declare the custom prototypes once more

```c
#include <stdio.h>
void menu();
void action( int option );
```

![](img/db19f3858a1e321646bf2590afd29547_137_0.png)

action.c

![](img/db19f3858a1e321646bf2590afd29547_137_1.png)

Notice that prototypes are declared here for each file containing calls to those functions – to prevent an “implicit declaration of function” compiler warning.

- 6. Now, define two simple static functions

```c
static int square( int a ) { return (a * a ); }
static int multiply( int a, int b ){ return a * b ; }
```

- 7. Finally, define the function being passed the menu option from the call in the main function to execute an appropriate action – calling upon the static functions created in this file when required

```c
void action( int option )
{
    int n1, n2;
    if( option == 1 )
    {
        printf( "Enter an integer to be squared: " );
        scanf( "%d", &n1 );
        printf( "%d x %d = %d \n", n1 , n1 , square(n1) );
        menu();
    }
    else if( option == 2 )
    {
        printf("Enter two integers to multiply ");
        printf("separated by a space: ");
        scanf("%d", &n1); scanf("%d", &n2);
        printf("%d x %d = %ld\n", n1, n2, multiply(n1, n2));
        menu();
    }
    else return;
}
```

- 8. Save both program files, then compile and execute the program to see the output returned from static functions

![](img/db19f3858a1e321646bf2590afd29547_138_0.png)

![](img/db19f3858a1e321646bf2590afd29547_138_1.png)

An example demonstrating static variables can be found here.

![](img/db19f3858a1e321646bf2590afd29547_138_2.png)

Note that the compiler command specifies both `.c` source code file names to create a single executable file.
