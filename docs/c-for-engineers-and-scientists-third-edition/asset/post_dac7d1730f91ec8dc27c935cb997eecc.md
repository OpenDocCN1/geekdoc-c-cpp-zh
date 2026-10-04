
## Chapter 6: Function and Parameter Declarations

## Program 6.1

```cpp
#include <iostream>
using namespace std;

void findMax(int, int); // the function declaration (prototype)

int main() {
    int firstnum, secnum;
    cout << "\nEnter a number: ";
    cin >> firstnum;
    cout << "Great! Please enter a second number: ";
    cin >> secnum;

    findMax(firstnum, secnum); // the function is called here
    return 0;
}
```

First, the declaration and calling of the findMax() function from main(). You then see how to use findMax() to accept data passed to it and determine the largest or maximum value of the two values.

The function findMax() is referred to as the called function because it's called or summoned by its reference in main(). The function that does the calling, in this case main(), is referred to as the calling function. The terms "called" and "calling" come from standard telephone usage, in which one party calls the other. The person initiating the call is referred to as the calling party, and the person receiving the call is referred to as the called party. The same terms describe function calls. The function findMax() is declared as a function that expects to receive two integers and to return no value (a void). This declaration is formally referred to as a function prototype. The function is then called by the last statement.

## Function Prototypes

Before a function can be called, it must be declared to the function that will do the calling. The declaration statement for a function is referred to as a function prototype. The prototype tells the calling function the type of value that will be formally returned, if any, and the data type and order of the values the calling function should transmit to the called function. For example, the function prototype previously used in Program 6.1

```cpp
void findMax(int, int);
```

## Modularity Using Functions

declares that the function findMax() expects two integer values to be sent to it and that this function formally returns no value (void).

Function prototypes can be placed with the variable declaration statements of the calling function, above the calling function name (as in a separate header file specified with an #include preprocessor statement). The function prototype for findMax() could have been placed before or after the statement #include<iostream>, within main(). (The reasons for the choice of placement are explained in Section 6.3.) The general form of function prototypes is as follows:

```cpp
return dataTypeName(list of argument data types);
```

The DataType refers to the type of the return value. Here are some examples of function prototypes:

```cpp
int fmax(int, int);
double swap(int, char, double);
void display(double, double);
```

The function prototype for fmax() declares that this function expects to receive two arguments and returns an integer value. The function prototype for swap() declares that this function requires four arguments—consisting of an integer, two characters, and a double-precision, in that order—and returns a double-precision. Finally, the function prototype for display() declares that this function requires double-precision arguments and doesn't return any value. This function might be used to display the results of a computation without returning any value to the called function.

The use of function prototypes permits the compiler to error-check data types. When the function is written, a compiler warning occurs. The prototype also serves another task: It ensures that all arguments passed to the function are converted to the declared data type when the function is called.

## Calling a Function

Calling a function is easy. The only requirements are using the name of the function and enclosing any data passed to the function in the parentheses the function name, using the same order and type declared in the function prototype. The items enclosed in parentheses are called arguments of the called function (see Figure 6.2).

| Statement | Description |
| :--- | :--- |
| findMax(firstnum, secnum); | This identifies the findMax() function | This two values to be passed to findMax() |

> Figure 6.2 Calling and passing two values to findMax()

If a variable is one of the arguments of a function call, the called function receives a copy of the value stored in that. For example, the statement findMax(firstnum, secnum); calls findMax() and causes the values in the variables firstnum and secnum to be passed to findMax(). The variable names in parentheses are arguments that provide values to the called function. After values are passed, control is transferred to the called function.

## Function and Parameter Declarations

As illustrated in Figure 6.3, the findMax() function does not receive the variables firstnum and secnum and has no knowledge of these variables. The function simply receives the values in these variables and must determine where to store them before it does anything. Although this procedure for passing data to a function might seem surprising, it's actually a safety procedure for ensuring that a function doesn't inadvertently change data in variables. The function gets a copy of the data to use. It can change its copy, of course, not any variables declared within it. Unless specific tips are taken...

**Figure 6.3** The findMax() function receives actual values. Next, you begin writing findMax() to process the values passed to it.

## Defining a Function

A function is defined when it's written. Each function is defined once (that is, written once) in a program and can be used by any other function that declares it. Like the main() function, every C++ function consists of two parts, a **function header** and a **function body**, as illustrated in 6.4. The function header's purpose is to identify the data type of the value the function returns, provide the function with a name, and specify the number, order, and type of arguments the function expects. The function body's purpose is to operate on the passed data and return, most, one value directly back to the calling function (In Section 6.3, you see how a function can be made to return multiple values indirectly.)

> In Section 6.3, you see how C++ also permits direct access to the calling function's variables.

The function header is always the first line of a function and contains the function's returned value type, its name, and the names and data types of its parameters. Because findMax() doesn't return any value and receives two integer values, the following function header can be used:

```cpp
void findMax(int x, int y) // no semicolon
```

The names in parentheses are called the formal parameters of the function (or parameters, for short). Therefore the parameter x is used to store the first value passed to findMax(), and the parameter y is used to store the second value passed at the time of the function call. The function doesn't know where the values come from when the call is made from main(). The first part of the call the computer executes involves going to the variables firstnum and secnum and retrieving the stored values. These values are then passed to findMax() and stored in parameters x and y (see Figure 6.5).

**Figure 6.5** Storing values in parameters

> The portion of the function header containing function names and parameters is formally referred to as a “function declarator.” The items enclosed in parentheses, the parameters, are specifications for the arguments. The arguments are values provided when the function is called.

## Function Definitions and Function Prototypes

When you write a function, you are formally creating a function definition. Each definition begins with a function header that includes a parameter list, if any, enclosed in parentheses and ends with the closing brace that terminates the function body. The parentheses are required whether or not the function uses any parameters. The following is a commonly used syntax for a function definition:

```cpp
returnDataType function(parameter list)
{
    constant declarations
    variable declarations
    other C++ statements
}
```

A prototype declares a function. The syntax for a function prototype, provides the function's return data type, the function's name, and the function's parameter list, is as follows:

```cpp
returnDataType function(list of parameter data types);
```

The prototype, with pre- and postcondition comments (of Information box), should give users all the programming information needed to call the function successfully.

Generally, all function prototypes are placed at the top of the program, and all definitions are placed after the main() function. However, this placement can be changed. The only requirement in C++ is that a function can't be called before it has been declared or defined.

The function name and all parameter names in the header—in this case, findMax, x, and y—are chosen by the programmer. Any names according to the rules for choosing variable names can be used. All parameters listed in the function must be separated by commas and have types declared.
