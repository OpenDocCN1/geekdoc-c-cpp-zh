
```
cout << "\nEnter a number: ";
cin >> firstnum;
cout << "Great! Please enter a second number: ";
cin >> secnum;

findMax(firstnum, secnum); // the function is called here

return 0;
}
```

First, examine the declaration and calling of the findMax() function from main(). You then see how to write findMax() to accept data passed to it, determine the largest or maximum value of the two passed values, and display the maximum value.

The findMax() function is referred to as the called function because it's called or summoned into action by its reference in main(). The function that does the calling—in this case, main()—is referred to as the calling function. The terms "called" and "calling" come from standard phone usage, in which one party calls the other. The person initiating the call is the calling party, and the person receiving the call is the called party. The same terms describe function calls. The called function—in this case, findMax()—is declared as a function that expects to receive two integer numbers and to return no value (a void) to main(). This declaration is formally called a function prototype. The function is then called by the last statement in the program.

## Function Prototypes

Before a function can be called, it must be declared to the function that will do the calling. The declaration statement for a function is referred to as a function prototype. The function prototype tells the calling function the type of value that will be formally returned, if any, and the data type and order of the values the calling function should transmit to the called function.

For example, the function prototype used in Program 6.1

```
void findMax(int, int);
```

declares that the findMax() function expects two integer values to be sent to it and returns no value (void).

Function prototypes can be placed with the variable declaration statements of the calling function, above the calling function name, as in Program 6.1, or in a separate header file specified with an #include preprocessor statement. The function prototype for findMax() could have been placed before or after the statement #include <iostream>, before main(), or within main(). (The reasons for the choice of placement are explained in Section 6.3.) The general form of function prototype statements is as follows:

```
returnDataType functionName(list of argument data types);
```

The returnDataType refers to the type of value the function returns. Here are some examples of function prototypes:

```
int fmax(int, int);
double swap(int, char, char, double);
void display(double, double);
```

The function prototype for fmax() declares that this function expects to receive two integer arguments and returns an integer value. The function prototype for swap() declares that this function requires four arguments—consisting of an integer, two characters, and a double-precision argument, in that order—and returns a double-precision number. Finally, the function prototype for display() declares that this function requires two double-precision arguments and doesn't return any value. This function might be used to display the results of a computation without returning any value to the called function.

Using function prototypes permits the compiler to error-check data types. If the function prototype doesn't agree with data types defined when the function is written, a warning message is displayed when the program is compiled. The prototype also serves another task: It ensures that all arguments passed to the function are converted to the declared data type when the function is called.

## Calling a Function

Calling a function is rather easy. The only requirements are using the name of the function and enclosing any data passed to the function in the parentheses following the function name, using the same order and type declared in the function prototype. The items enclosed in parentheses are called arguments of the called function (see Figure 6.2).

![](img/202cface8244f523c2641baa2e00d7dd_247_0.png)

Figure 6.2 Calling and passing two values to findMax()

If a variable is one of the arguments in a function call, the called function receives a copy of the value stored in the variable. For example, the statement findMax(firstnum, secnum); calls the findMax() function and causes the values stored in the variables firstnum and secnum to be passed to findMax(). The variable names in parentheses are arguments that provide values to the called function. After values are passed, control is transferred to the called function.

As shown in Figure 6.3, the findMax() function does not receive the variables named firstnum and secnum and has no knowledge of these variable names.¹ The function simply receives the values in these variables and must then determine where to store these values before it does anything else. Although this procedure for passing data to a function might seem surprising, it's actually a safety measure for ensuring that a called function doesn't inadvertently change data stored in a variable. The function gets a copy of the data to use. It can change its copy and, of course, change any variables declared inside it. However, unless specific steps to do so are taken, a function isn't allowed to change the contents of variables declared in other functions.

> ¹In Section 6.3, you see how C++ also allows direct access to the calling function's variables by using reference variables.

![](img/202cface8244f523c2641baa2e00d7dd_248_0.png)

Figure 6.3 The findMax() function receives actual values

Next, you begin writing the findMax() function to process the values passed to it.

## Defining a Function

A function is defined when it's written. Each function is defined once (that is, written once) in a program and can then be used by any other function in the program that declares it suitably.

Like the main() function, every C++ function consists of two parts, a function header and a function body, as shown in Figure 6.4. The function header's purpose is to identify the data type of the value the function returns, give the function a name, and specify the number, order, and type of arguments the function expects. The function body's purpose is to operate on the passed data and return, at most, one value directly back to the calling function. (In Section 6.3, you see how a function can be made to return multiple values indirectly by using its arguments.)

The function header is always the first line of a function and contains the function's return value type, its name, and the names and data types of its arguments. Because findMax() doesn't formally return any value and receives two integer values, the following function header can be used:

```
void findMax(int x, int y)
```

no semicolon

## Modularity Using Functions

![](img/202cface8244f523c2641baa2e00d7dd_249_0.png)

The argument names in parentheses in the header are called the **formal parameters** of the function (or parameters, for short).² Therefore, the parameter x is used to store the first value passed to `findMax()` and the parameter y is used to store the second value passed at the time of the function call. The function doesn't know where the values come from when the call is made from `main()`. The first part of the called procedure that executes involves going to the variables firstnum and secnum and retrieving the stored values. These values are then passed to `findMax()` and stored in the parameters x and y (see Figure 6.5).

![](img/202cface8244f523c2641baa2e00d7dd_249_1.png)

The function name and all parameter names in the header—in this case, `findMax`, x, and y—are chosen by the programmer. Any names selected according to the rules for choosing variable names can be used. Any parameter listed in the function header must include a data type. If more than one parameter is declared in the function header, they must be separated by commas and have their data types declared separately.

> ²The portion of the function header containing function names and parameters is formally referred to as a "function declarator." The items enclosed in parentheses, the parameters, are specifications for the arguments. The arguments are the values provided when the function is called.
