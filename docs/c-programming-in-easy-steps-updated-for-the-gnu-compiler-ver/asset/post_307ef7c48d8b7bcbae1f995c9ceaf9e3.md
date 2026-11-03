
## Supplying arguments

Data can be passed as “arguments” to custom functions, which can then use that data to execute their statements. The function prototype must include the name and data type of each argument.

It is important to recognize that in C programming, the data is passed “by value” to the variable specified as the function argument. This is different to some other programming languages, such as Pascal, whose arguments are passed “by reference” – where the function operates on the original value, not just a local copy.

The arguments in a function prototype are known as the “formal parameters” of the function. These may be of different data types, and multiple arguments can be specified for a single function if separated by a comma. For example, a function prototype with arguments of each of the four data types could look like this:

```c
void action( char c , int i , float f , double d ) ;
```

The compiler checks that the formal parameters specified in the function prototype match those in the function definition and will report an error if they do not match.

![](img/d1dfb0563339ba187decb78799155b7f_89_0.png)

Passing data “by value” assigns the value to a variable in the called function. The function can then manipulate that copy but it does not affect the original data.

![](img/d1dfb0563339ba187decb78799155b7f_89_1.png)

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions
```c
#include <stdio.h>
```
- 2. Declare three custom function prototypes with one argument to be passed to each one when called
```c
void display( char str[] ) ;
int square( int x ) ;
int cube( int y ) ;
```
- 3. Add a main function that declares an integer variable and a character array variable initialized with a string of text
```c
int main()
{
    int num ;
    char msg[50] = "String to be passed to a function" ;
}
```

### 4
After the main function, define the custom functions

```c
void display( char str[] )
{
    printf( "%s\n", str );
}

int square( int x )
{
    return ( x * x );
}

int cube( int y )
{
    return ( y * y ) * y;
}
```

![](img/d1dfb0563339ba187decb78799155b7f_90_0.png)

The argument names used in the function definition can differ from those used in the function prototype but the argument data types, number, and order must be the same. It is clearer to adopt the same names in both, though.

### 5
Now, in the main function, insert statements calling each of the custom functions and passing argument values

```
display( msg );
num = square( 4 );
printf( "4x4= %d\n", num );
printf( "4x4x4= %d\n", cube( 4 ) );
```

### 6
At the end of the main function block, return a zero integer value, as required by the function declaration

```
return 0 ;
```

### 7
Save the program file, then compile and execute the program to see the output from custom functions using passed argument values

![](img/d1dfb0563339ba187decb78799155b7f_90_1.png)

![](img/d1dfb0563339ba187decb78799155b7f_90_2.png)

A function need not return any value but can still include the return keyword without any following value to signify the return of control to the caller.

## Calling recursively

Statements within custom functions can freely call other custom functions just as readily as they can call standard library functions like `printf()`.

Additionally, functions can call themselves, and these are known as “recursive functions”. As with loops it is important that recursive functions must modify a tested expression to avoid continuous execution – so the function call ends at some point.

![](img/d1dfb0563339ba187decb78799155b7f_91_0.png)

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions
```c
#include <stdio.h>
```
- 2. Declare a custom function prototype with one argument to be passed when called
```c
void count_down_from( int num );
```
- 3. Add a main function that declares an integer variable
```c
int main()
{
    int start ;
}
```
- 4. Next, in the main function block, add a statement requesting the user input an integer value to be assigned to the variable
```c
printf( "Enter a positive integer to count down from: " );
scanf( "%d", &start );
```
- 5. Now, in the main function block, add a call to the custom function, passing it the value entered by the user
```c
count_down_from( start );
```
- 6. In the main function block, add a statement to output a message when control returns from the custom function
```c
printf( "Lift Off!\n" );
```
- 7. At the end of the main function block, return a zero integer value, as required by the function declaration
```c
return 0;
```

![](img/d1dfb0563339ba187decb78799155b7f_91_1.png)

The variable name must be preceded by the & address of operator in the scanf() function, as described on page 24.

After the main function block, begin the custom function definition with a statement to output the argument value passed during the function call

```c
void count_down_from( int num )
{
    printf( "%d\n", num );
}
```

Next, in the custom function block, decrement the value passed as the argument

```c
--num ;
```

Now, in the custom function block, add a conditional test to return control to the main function if the decremented value is below zero or pass it as an argument in a recursive call to this function

```c
if( num < 0 ) return ;
else
    count_down_from( num ) ;
```

Save the program file then compile and execute the program, inputting an integer when requested, to see the output from recursive function calls

![](img/d1dfb0563339ba187decb78799155b7f_92_0.png)

![](img/d1dfb0563339ba187decb78799155b7f_92_1.png)

![](img/d1dfb0563339ba187decb78799155b7f_92_2.png)

A recursive function can be less efficient than using a loop.

![](img/d1dfb0563339ba187decb78799155b7f_92_3.png)

## Placing functions in headers

The example programs listed throughout this book are necessarily small due to space considerations but in reality, most C programs will contain significantly more code.

When developing larger programs, some thought should be given to program structure. Maintaining the entire program code in a single file can become unwieldy as the program grows.

In order to simplify the program structure, a custom header file can be created to contain functions that may be used repeatedly. This should be named with a “.h” file extension, like the standard header files in the C library.

The functions in the custom header file can be made available to the program by adding an #include preprocessor directive at the start of the file containing the main() function. The custom header file name should be enclosed within double quotes in the preprocessor directive though, rather than by the < and > angled brackets that are used to include standard header files.

![](img/d1dfb0563339ba187decb78799155b7f_93_0.png)

![](img/d1dfb0563339ba187decb78799155b7f_93_1.png)

- 1. Create a custom header file named “utils.h” containing the definition of a single function
```c
int square( int num )
{
 return ( num * num ) ;
}
```
- 2. Begin a new program with a preprocessor instruction to include the standard input/output library functions and the custom header file
```c
#include <stdio.h>
#include "utils.h"
```
- 3. Declare a custom function prototype with no arguments
```c
void getnum() ;
```
- 4. Add a main function to call the other function then return a zero integer as required by the declaration
```c
int main()
{
 getnum() ;
 return 0 ;
}
```

- 5. After the main function block, begin the second function definition by declaring two variables
```c
void getnum()
{
    int num ;
    char again ;
}
```
- 6. Next, in this function definition, add statements to request user input and assign its value to a variable
```
printf("Enter an integer to be squared: ");
scanf("%d", &num );
```
- 7. Now, output a result by calling the function in the custom header file, passing it the input value as its argument
```
printf("%d squared is %d\n", num, square(num) );
```
- 8. Add a statement requesting further user input and assign its value to a variable
```
printf("Square another number? Y or N: ");
scanf("%1s", &again );
```
- 9. Finally, add a conditional test to execute this function once more or return control to the main function
```
if( again == 'Y' || ( again == 'y' ) ) getnum();
else return ;
```
- 10. Save the program file then compile and execute the program, inputting an integer and character when requested, to see the output from the function calls

![](img/d1dfb0563339ba187decb78799155b7f_94_0.png)

The program file and custom header file must be located in the same directory but are compiled with the usual command – the compiler reads the header file automatically because of the #include directive.

![](img/d1dfb0563339ba187decb78799155b7f_94_1.png)

Notice the use of the %1s format specifier in this example – to read the next character entered by the user.

![](img/d1dfb0563339ba187decb78799155b7f_94_2.png)
