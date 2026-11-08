
This section discusses how to handle exceptions. However, first we offer some examples that show what can happen if an exception is not handled. We also review some of the ways to handle exceptions.

The program in Example 14-1 shows what happens when division by zero occurs and the problem is not addressed.

## EXAMPLE 14-1

```cpp
// Division by zero.

#include <iostream>

using namespace std;

int main()
{
    int dividend, divisor, quotient;                 //Line 1

    cout << "Line 2: Enter the dividend: ";          //Line 2
    cin >> dividend;                                 //Line 3
    cout << endl;                                    //Line 4

    cout << "Line 5: Enter the divisor: ";           //Line 5
    cin >> divisor;                                  //Line 6
    cout << endl;                                    //Line 7

    quotient = dividend / divisor;                  //Line 8
    cout << "Line 9: Quotient = " << quotient
         << endl;                                    //Line 9

    return 0;                                        //Line 10
}
```

### Sample Run 1

```text
Line 2: Enter the dividend: 12

Line 5: Enter the divisor: 5

Line 9: Quotient = 2
```

### Sample Run 2

```text
Line 2: Enter the dividend: 24

Line 5: Enter the divisor: 0
```

CPP_Proj1.exe has encountered a problem and needs to close. We are sorry for the inconvenience.

In Sample Run 1, the value of divisor is nonzero, so no exception occurs. The program calculates and outputs the quotient and terminates normally.

In Sample Run 2, the value entered for divisor is 0. The statement in Line 8 divides dividend by the divisor. However, the program does not check whether divisor is 0 before dividing dividend by divisor. So, the program crashes with the message shown. Notice that the error message is platform independent, that is, IDE dependent. Some IDEs might not give this error message and might simply hang.

Next, consider Example 14-2. This is the same program as in Example 14-1, except that in Line 8, the program checks whether divisor is zero.

## EXAMPLE 14-2

```cpp
// Checking division by zero.

#include <iostream>

using namespace std;

int main()
{
    int dividend, divisor, quotient;                 //Line 1

    cout << "Line 2: Enter the dividend: ";          //Line 2
    cin >> dividend;                                 //Line 3
    cout << endl;                                    //Line 4

    cout << "Line 5: Enter the divisor: ";           //Line 5
    cin >> divisor;                                  //Line 6
    cout << endl;                                    //Line 7

    if (divisor != 0)                                //Line 8
    {
        quotient = dividend / divisor;               //Line 9
        cout << "Line 10: Quotient = " << quotient
             << endl;                                //Line 10
    }
    else                                             //Line 11
        cout << "Line 12: Cannot divide by zero."
             << endl;                                //Line 12

    return 0;                                        //Line 13
}
```

### Sample Run 1

```text
Line 2: Enter the dividend: 12

Line 5: Enter the divisor: 5

Line 10: Quotient = 2
```

### Sample Run 2

```text
Line 2: Enter the dividend: 24
Line 5: Enter the divisor: 0
Assertion failed: divisor != 0, file c:\\e\chapter14 source code\ch14_exp3.cpp, line 20
```

In Sample Run 1, the value of divisor is nonzero, so no exception occurs. The program calculates and outputs the quotient and terminates normally.

In Sample Run 2, the value entered for divisor is 0. In Line 8, the function assert checks whether divisor is nonzero. Because divisor is 0, the expression in the assert statement evaluates to false, and the function assert terminates the program with the error message shown in the third line of the output.

## C++ Mechanisms of Exception Handling

Examples 14-1 through 14-3 show what happens when an exception occurs in a program and is not processed. This section describes how to include the necessary code to handle exceptions within a program.

### try/catch Block

The statements that may generate an exception are placed in a try block. The try block also contains statements that should not be executed if an exception occurs. The try block is followed by one or more catch blocks. A catch block specifies the type of exception it can catch and contains an exception handler.

The general syntax of the try/catch block is:

```cpp
try
{
    //statements
}
catch (dataType1 identifier)
{
    //exception-handling code
}
.
.
.
catch (dataTypen identifier)
{
    //exception-handling code
}
.
.
.
catch (...)
{
    //exception-handling code
}
```

Suppose there is a statement that can generate an exception, for example, division by 0. Usually, before executing such a statement, we check whether certain conditions are met. For example, before performing the division, we check whether the divisor is nonzero. If the conditions are not met, we typically generate an exception, which in C++ terminology is called throwing an exception. This is typically done using the `throw` statement, which we will explain shortly. We will show what is typically thrown to generate an exception.

Let us now note the following about try/catch blocks.

- If no exception is thrown in a try block, all catch blocks associated with that try block are ignored and program execution resumes after the last catch block.
- If an exception is thrown in a try block, the remaining statements in that try block are ignored. The program searches the catch blocks in the order they appear after the try block and looks for an appropriate exception handler. If the type of thrown exception matches the parameter type in one of the catch blocks, the code of that catch block executes, and the remaining catch blocks after this catch block are ignored.
- The last catch block that has an ellipsis (three dots) is designed to catch any type of exception.

Consider the following catch block:

```cpp
catch (int x)
{
    //exception-handling code
}
```

In this catch block:

- The identifier x acts as a parameter. In fact, it is called a catch block parameter.
- The data type int specifies that this catch block can catch an exception of type int.
- A catch block can have at most one catch block parameter.

Essentially, the catch block parameter becomes a placeholder for the value thrown. In this case, x becomes a placeholder for any thrown value that is of type int. In other words, if the thrown value is caught by this catch block, then the thrown value is stored in the catch block parameter. This way, if the exception-handling code wants to do something with that value, it can be accessed via the catch block parameter.

Suppose in a catch block heading only the data type is specified, that is, there is no catch block parameter. The thrown value then may not be accessible in the catch block exception-handling code.

### THROWING AN EXCEPTION

In order for an exception to occur in a try block and be caught by a catch block, the exception must be thrown in the try block. The general syntax to throw an exception is:

```cpp
throw expression;
```

In which expression is a constant value, variable, or object. The object being thrown can be either a specific object or an anonymous object. It follows that in C++, an exception is a value.

In C++, throw is a reserved word.

Example 14-4 illustrates how to use a throw statement.

## EXAMPLE 14-4

Suppose we have the following declaration:

```cpp
int num = 5;
string str = "Something is wrong!!!";
```

| throw expression | Effect |
|---|---|
| `throw 4;` | The constant value 4 is thrown. |
| `throw x;` | The value of the variable x is thrown. |
| `throw str;` | The object str is thrown. |
| `throw string("Exception found!");` | An anonymous string object with the string "Exception found!" is thrown. |

### ORDER OF catch BLOCKS

A catch block can catch either all exceptions of a specific type or all types of exceptions. The heading of a catch block specifies the type of exception it handles. As noted previously, the catch block that handles an ellipsis (three dots) is designed to catch any type of exception. Therefore, if we put this catch block first, then this catch block can catch all types of exceptions.

Suppose that an exception occurs in a try block and is caught by a catch block. The remaining catch blocks associated with that try block are then ignored. Therefore, you should be careful about the order in which you list your catch blocks following a try block. For example, consider the following sequence of try/catch blocks:

```cpp
try                 //Line 1
{
    //statements
}
catch (...)         //Line 2
{
    //statements
}
catch (int x)       //Line 3
{
    //statements
}
```
