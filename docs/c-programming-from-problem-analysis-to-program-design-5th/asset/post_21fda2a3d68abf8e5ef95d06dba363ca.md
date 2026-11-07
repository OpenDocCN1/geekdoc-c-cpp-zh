
### EXAMPLE 16-11

```cpp
// Using user-defined exception class divisionByZero with
// default error message.

#include <iostream>
#include "divisionByZero.h"

using namespace std;

int main()
{
    int dividend, divisor, quotient;                 //Line 1

    try                                           //Line 2
    {
        cout << "Line 3: Enter the dividend: ";    //Line 3
        cin >> dividend;                           //Line 4
        cout << endl;                              //Line 5

        cout << "Line 6: Enter the divisor: ";     //Line 6
        cin >> divisor;                            //Line 7
        cout << endl;                              //Line 8

        if (divisor == 0)                          //Line 9
            throw divisionByZero();                //Line 10

        quotient = dividend / divisor;             //Line 11
        cout << "Line 12: Quotient = " << quotient //Line 12
             << endl;
    }
    catch (divisionByZero divByZeroObj)             //Line 13
    {
        cout << "Line 14: In the divisionByZero "
             << "catch block."
             << divByZeroObj.what() << endl;       //Line 14
    }

    return 0;                                      //Line 15
}
```

**Sample Run 1:** In this sample run, the user input is shaded.

Line 3: Enter the dividend: **34**  
Line 6: Enter the divisor: **5**  
Line 12: Quotient = 6

**Sample Run 2:** In this sample run, the user input is shaded.

Line 3: Enter the dividend: **56**  
Line 6: Enter the divisor: **0**  
Line 14: In the divisionByZero catch block: Division by zero

In this program, the statement in Line 10 throws an object (exception) of the class `divisionByZero` if the user enters 0 for the divisor. This thrown exception is caught and processed by the catch block in Line 13. The parameter divByZeroObj in the catch block catches the value of the thrown object and then uses the function what to return the string stored in the object. The statement in Line 14 outputs the appropriate error message.

The program in Example 16-12 is similar to the program in Example 16-11. Here, the thrown object is still an anonymous object, but the error message is specified by the user (see the statement in Line 10).

### EXAMPLE 16-12

```cpp
// Using user-defined exception class divisionByZero with a
// specific error message.

#include <iostream>
#include "divisionByZero.h"

using namespace std;

int main()
{
    int dividend, divisor, quotient;                    //Line 1

    try                                                //Line 2
    {
        cout << "Line 3: Enter the dividend: ";       //Line 3
        cin >> dividend;                               //Line 4
        cout << endl;                                  //Line 5

        cout << "Line 6: Enter the divisor: ";        //Line 6
        cin >> divisor;                                //Line 7
        cout << endl;                                  //Line 8

        if (divisor == 0)                              //Line 9
            throw divisionByZero("Found division by zero"); //Line 10

        quotient = dividend / divisor;                 //Line 11
        cout << "Line 12: Quotient = " << quotient    //Line 12
             << endl;
    }
    catch (divisionByZero divByZeroObj)
    {
        cout << "Line 14: In the divisionByZero "
             << "catch block:"
             << divByZeroObj.what() << endl;
    }

    return 0;
}
```

**Sample Run 1:** In this sample run, the user input is shaded.

Line 3: Enter the dividend: **34**  
Line 6: Enter the divisor: **5**  
Line 12: Quotient = 6

**Sample Run 2:** In this sample run, the user input is shaded.

Line 3: Enter the dividend: **56**  
Line 6: Enter the divisor: **0**  
Line 14: In the divisionByZero catch block: Found division by zero

This program works the same way as the program in Example 16-11. The details are left as an exercise for you.

In the programs in Examples 16-11 and 16-12, the data manipulation is done in the function main. Therefore, the exception is thrown, caught, and processed in the function main. The program in Example 16-13 uses the user-defined function doDivision to manipulate the data. Therefore, the exception is thrown, caught, and processed in the function doDivision.

### EXAMPLE 16-13

```cpp
// Handling an exception thrown by a function.

#include <iostream>
#include "divisionByZero.h"

using namespace std;

void doDivision();

int main()
{
    doDivision();                         //Line 1

    return 0;                             //Line 2
}

void doDivision()
{
    int dividend, divisor, quotient;                //Line 3

    try
    {
        cout << "Line 4: Enter the dividend: ";     //Line 4
        cin >> dividend;                            //Line 5
        cout << endl;                               //Line 6

        cout << "Line 7: Enter the divisor: ";      //Line 7
        cin >> divisor;                             //Line 8
        cout << endl;                               //Line 9

        if (divisor == 0)                           //Line 10
            throw divisionByZero();                 //Line 11

        quotient = dividend / divisor;              //Line 12
        cout << "Line 13: Quotient = " << quotient
             << endl;                               //Line 13
    }
    catch (divisionByZero divByZeroObj)             //Line 14
    {
        cout << "Line 15: In the function "
             << "doDivision: "
             << divByZeroObj.what() << endl;        //Line 15
    }
}
```

**Sample Run 1:** In this sample run, the user input is shaded.

Line 4: Enter the dividend: **34**  
Line 7: Enter the divisor: **5**  
Line 13: Quotient = 6

**Sample Run 2:** In this sample run, the user input is shaded.

Line 4: Enter the dividend: **56**  
Line 7: Enter the divisor: **0**  
Line 15: In the function doDivision: Division by zero

## Rethrowing and Throwing an Exception

When an exception occurs in a `try` block, control immediately passes to one of the `catch` blocks. Typically, a `catch` block either handles the exception or partially processes the exception and then rethrows the same exception, or it rethrows another exception in order for the calling environment to handle the exception. The `catch` block in Examples 16-4 through 16-13 handles the exception. The mechanism of rethrowing or throwing an exception is quite useful in cases in which a `catch` block catches the exception but cannot handle the exception, or if the `catch` block decides that the exception should be handled by the calling block or environment. This allows the programmer to provide the exception-handling code all in one place.

To rethrow or throw an exception, we use the `throw` statement. The general syntax to rethrow an exception caught by a `catch` block is:

```cpp
throw;
```

(in this case, the same exception is rethrown) or:

```cpp
throw expression;
```

in which `expression` is a constant value, variable, or object. The object being thrown can be either a specific object or an anonymous object.

A function specifies the exceptions it throws (to be handled somewhere) in its heading using the `throw` clause. For example, the following function specifies that it throws exceptions of type `int`, `string`, and `divisionByZero`, in which `divisionByZero` is the class, as defined previously.

```cpp
void someThrowExcep(int x) throw (int, string, divisionByZero)
{
    .
    .
    .
    //include the appropriate throw statements
    .
    .
    .
}
```

The program in Example 16-14 further explains how a function specifies the exception it throws.

### EXAMPLE 16-14

```cpp
// Handling an exception, in the main function, thrown by another
// function. The function throws the same exception object.

#include <iostream>
#include "divisionByZero.h"

using namespace std;

void doDivision() throw (divisionByZero);
```
