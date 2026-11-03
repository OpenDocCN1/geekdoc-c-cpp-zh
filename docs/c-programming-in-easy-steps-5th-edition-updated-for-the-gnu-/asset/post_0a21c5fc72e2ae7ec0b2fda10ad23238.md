
## 6 Employing Functions

*This chapter demonstrates how statements can be enclosed within a “function” for execution whenever called by the C program.*

- Declaring functions
- Supplying arguments
- Calling recursively
- Placing functions in headers
- Restricting accessibility
- Summary

### Declaring functions

Previous examples in this book have used the obligatory main() function and standard functions contained in the C header library, such as the printf() function from the stdio.h file. However, most C programs contain a number of custom functions, which can be called as required during the execution of the program.

![](img/db19f3858a1e321646bf2590afd29547_124_0.png)

A function block simply contains a group of statements that get executed whenever that function is called. Once the function statements have been executed, program flow resumes at the point directly following the function call. This modularity is very useful in C programming to isolate set routines so they can be called upon repeatedly.

To introduce a custom function into a C program it must first be declared, in a similar manner that variables must be declared before they can be used. Function declarations should be added before the main() function block.

Like the main() function, custom functions can return a value. The data type of this return value must be included in the function declaration. If the function is to return no value, its return data type should be declared with the void keyword. The function should be named following the same naming conventions used for variable names.

The function declaration is more correctly known as the “function prototype” and simply informs the compiler about the function. The actual function definition, which includes the statements to be executed, appears after the main() function. The custom function can then be called upon to execute its statements from within the main() function, as required.

If a custom function returns a value this can be assigned to a variable of an appropriate data type, or simply displayed as output using the appropriate format specifier.

1. Begin a new program with a preprocessor instruction to include the standard input/output library functions

```
#include <stdio.h>
```

![](img/db19f3858a1e321646bf2590afd29547_125_0.png)

first.c

2. Declare three custom function prototypes

```
void first();
int square5();
int cube5();
```

![](img/db19f3858a1e321646bf2590afd29547_125_1.png)

The function prototype is sometimes referred to as the “function header”.

3. Add a main function that declares an integer variable

```
int main()
{
    int num ;
}
```

4. After the main function, define the custom functions

```
void first()
{
    printf( "Hello from the first function\n" );
}

int square5()
{
    int square = 5 * 5 ;
    return square ;
}

int cube5()
{
```

```
int cube = (5 * 5) * 5 ;
return cube ;
}
```

Now, insert calls to the custom functions in the main function block

```
first();
num = square5();
printf("5x5= %d\n", num );
printf("5x5x5= %d\n", cube5() );
```

At the end of the main function block, return a zero integer value, as required by that function declaration

```
return 0 ;
```

Save the program file, then compile and execute the program to see the output from custom functions

![](img/db19f3858a1e321646bf2590afd29547_126_0.png)

![](img/db19f3858a1e321646bf2590afd29547_126_1.png)

Notice that each function prototype must end with a semi-colon.

![](img/db19f3858a1e321646bf2590afd29547_126_2.png)

The custom function definitions could technically appear before the main() function – but convention is to include prototypes and keep the main() function at the beginning of the program code.

### Supplying arguments

Data can be passed as “arguments” to custom functions, which can then use that data to execute their statements. The function prototype must include the name and data type of each argument.

It is important to recognize that in C programming, the data is passed “by value” to the variable specified as the function argument. This is different to some other programming languages, such as Pascal, whose arguments are passed “by reference” – where the function operates on the original value, not just a local copy.

The arguments in a function prototype are known as the “formal parameters” of the function. These may be of different data types, and multiple arguments can be specified for a single function if separated by a comma. For example, a function prototype with arguments of each of the four data types could look like this:

```
void action( char c , int i , float f , double d ) ;
```

The compiler checks that the formal parameters specified in the function prototype match those in the function definition and will report an error if they do not match.

1 Begin a new program with a preprocessor instruction to include the standard input/output library functions

```
#include <stdio.h>
```

![](img/db19f3858a1e321646bf2590afd29547_127_0.png)

2 Declare three custom function prototypes with one argument to be passed to each one when called

```
void display( char str[] ) ;
int square( int x ) ;
int cube( int y ) ;
```

3 Add a main function that declares an integer variable and a character array variable initialized with a string of text

```c
int main()
{
int num ;
char msg[50] = "String to be passed to a function" ;
}
```

![](img/db19f3858a1e321646bf2590afd29547_128_0.png)

Passing data "by value" assigns the value to a variable in the called function. The function can then manipulate that copy but it does not affect the original data.

4 After the main function, define the custom functions

```c
void display( char str[] )
{
printf( "%s\n", str );
}

int square( int x )
{
return (x * x);
}

int cube( int y )
{
return ( y * y ) * y ;
}
```

5 Now, in the main function, insert statements calling each of the custom functions and passing argument values

```c
display( msg );
num = square( 4 );
printf( "4x4= %d\n", num );
printf( "4x4x4= %d\n", cube( 4 ) );
```

6 At the end of the main function block, return a zero integer value, as required by the function declaration

```c
return 0;
```

7 Save the program file, then compile and execute the program to see the output from custom functions using passed argument values

![](img/db19f3858a1e321646bf2590afd29547_129_0.png)

![](img/db19f3858a1e321646bf2590afd29547_129_1.png)

The argument names used in the function definition can differ from those used in the function prototype but the argument data types, number, and order must be the same. It is clearer to adopt the same names in both, though.

![](img/db19f3858a1e321646bf2590afd29547_129_2.png)

A function need not return any value but can still include the **return** keyword without any following value to signify the return of control to the caller.

### Calling recursively

Statements within custom functions can freely call other custom functions just as readily as they can call standard library functions like **printf()**.

Additionally, functions can call themselves, and these are known as “recursive functions”. As with loops it is important that recursive functions must modify a tested expression to avoid continuous execution – so the function call ends at some point.

1. Begin a new program with a preprocessor instruction to include the standard input/output library functions

```
#include <stdio.h>
```

![](img/db19f3858a1e321646bf2590afd29547_130_0.png)

2. Declare a custom function prototype with one argument to be passed when called

```
void count_down_from( int num );
```

3. Add a main function that declares an integer variable

```
int main()
{
    int start;
}
```

4. Next, in the main function block, add a statement requesting the user input an integer value to be assigned to the variable

```
printf("Enter a positive integer to count down from: ");
scanf("%d", &start);
```

5. Now, in the main function block, add a call to the custom function, passing it the value entered by the user

```
count_down_from( start );
```

6. In the main function block, add a statement to output a message when
