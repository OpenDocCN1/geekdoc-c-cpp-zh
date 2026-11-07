
```cpp
#include "circleType.h"                             //Line 3
#include "negativeNumber.h"                         //Line 4

using namespace std;                                //Line 5

int main()                                          //Line 6
{                                                   //Line 7
    circleType circle;                              //Line 8

    double radius;                                  //Line 9

    cout << fixed << showpoint << setprecision(2);  //Line 10

    try                                             //Line 11
    {                                               //Line 12
        cout << "Line 13: Enter the radius "
             << "of a circle: ";                    //Line 13
        cin >> radius;                              //Line 14
        cout << endl;                               //Line 15

        circle.setRadius(radius);                   //Line 16

        cout << "Line 17: circle - "
             << "radius: " << circle.getRadius()
             << ", area: " << circle.area()
             << ", circumference: "
             << circle.circumference() << endl;     //Line 17
    }                                               //Line 18
    catch (negativeNumber obj)                      //Line 19
    {                                               //Line 20
        cout << "Line 21: " << obj.what() << endl;  //Line 21
    }                                               //Line 22

    return 0;                                       //Line 23
}//end main                                         //Line 24
```

**Sample Run 1:** In this sample run, the user input is shaded.

```
Line 13: Enter the radius of a circle: 5.25
Line 17: circle - radius: 5.25, area: 86.59, circumference: 32.99
```

**Sample Run 2:** In this sample run, the user input is shaded.

```
Line 13: Enter the radius of a circle: -2.5
Line 21: Radius cannot be negative
```

The preceding program works as follows. The statement in Line 8 creates the `circleType` object `circle` and using the default constructor sets the radius to 0.0. The statement in Line 9 declares the `double` variable `radius`. The `try/catch` block, between Lines 11 and 22 contains the code to prompt the user to enter the radius of the circle and depending on the value entered by the user generates the output. For example, if the user enters a nonnegative radius, the statement in Line 16 sets the radius of the circle and the statement in Line 17 outputs the radius, area, and the perimeter of the circle. If the user enters a negative number, the statement in Line 16 throws an exception, which is a `negativeNumber` object, and the `catch` block processes the exception. In Sample Run 1, the user enters `5.25`, a nonnegative number, and the program outputs the radius, area, and the perimeter of the circle. In Sample Run 2, the user enters `-2.5`, which is a negative number, and the statement in Line 21 outputs that the radius cannot be negative.

## Rethrowing and Throwing an Exception

When an exception occurs in a `try` block, control immediately passes to one of the `catch` blocks. Typically, a `catch` block either handles the exception or partially processes the exception and then rethrows the same exception, or it rethrows another exception in order for the calling environment to handle the exception. The `catch` block in Examples 14-4 through 14-14 handles the exception. The mechanism of rethrowing or throwing an exception is quite useful in cases in which a `catch` block catches the exception but cannot handle the exception, or if the `catch` block decides that the exception should be handled by the calling block or environment. This allows the programmer to provide the exception-handling and calling all in one place.

To rethrow or throw an exception, we use the `throw` statement. The general syntax to rethrow an exception caught by a `catch` block is

```
throw;
```

(in this case, the same exception is rethrown) or

```
throw expression;
```

in which `expression` is a constant value, variable, or object. The object being thrown can be either a specific object or an anonymous object.

A function specifies the exceptions it throws (to be handled somewhere) in its heading using the `throw` clause. For example, the following function specifies that it throws exceptions of type `int`, `string`, and `divisionByZero`, in which `divisionByZero` is the class, as defined previously.

```cpp
void exprThrowExcept(int x) throw (int, string, divisionByZero)
{
    .
    .
    //include the appropriate throw statements
    .
    .
}
```

The program in Example 14-15 further explains how a function specifies the exception it throws.

### EXAMPLE 14-15

```cpp
// Handling exception, in the main function, thrown by another
// function. The function throws the same exception object.

#include <iostream>                                      //Line 1
#include "divisionByZero.h"                              //Line 2

using namespace std;                                     //Line 3

void doDivision() throw (divisionByZero);                //Line 4

int main()                                               //Line 5
{                                                        //Line 6
    try                                                  //Line 7
    {                                                    //Line 8
        doDivision();                                    //Line 9
    }                                                    //Line 10
    catch (divisionByZero divByZeroObj)                  //Line 11
    {                                                    //Line 12
        cout << "Line 13: In main: "                     //Line 13
             << divByZeroObj.what() << endl;             //Line 14
    }                                                    //Line 15
    return 0;                                            //Line 16
}                                                        //Line 17

void doDivision() throw (divisionByZero)                 //Line 18
{                                                        //Line 19
    int dividend, divisor, quotient;                     //Line 20
    try                                                  //Line 21
    {                                                    //Line 22
        cout << "Line 22: Enter the dividend: ";         //Line 23
        cin >> dividend;                                 //Line 24
        cout << endl;                                    //Line 25

        cout << "Line 25: Enter the divisor: ";          //Line 26
        cin >> divisor;                                  //Line 27
        cout << endl;                                    //Line 28

        if (divisor == 0)                                //Line 29
            throw                                        //Line 30
                divisionByZero("Found division by 0!");  //Line 31

        quotient = dividend / divisor;                   //Line 32
        cout << "Line 31: Quotient = " << quotient       //Line 33
             << endl;                                    //Line 34
    }                                                    //Line 35
    catch (divisionByZero)                               //Line 36
    {                                                    //Line 37
        throw;                                           //Line 38
    }                                                    //Line 39
}                                                        //Line 40
```

**Sample Run 1:** In this sample run, the user input is shaded.

- Line 22: Enter the dividend: 28
- Line 25: Enter the divisor: 6
- Line 31: Quotient = 4

**Sample Run 2:** In this sample run, the user input is shaded.

- Line 22: Enter the dividend: 35
- Line 25: Enter the divisor: 0
- Line 13: In main: Found division by 0!

In this program, if the value of divisor is 0, the statement in Line 29 throws an exception of type divisionByZero, which is an anonymous object of this class, with the message string:

> "Found division by 0!"

The statement in Line 35, in the catch block, throws the same exception value, which in this case is an object.

In Sample Run 1, no exception is thrown.

Let us see what happens in Sample Run 2. The function **main** calls the function **doDivision** in the **try** block. In the function **doDivision**, the value of divisor is 0, so the statement in Line 29 throws an exception. The exception is caught by the **catch** block in Line 33. The statement in Line 35 rethrows the same exception. In other words, the catch block catches and rethrows the same exception. Therefore, the function call statement in Line 9 results in throwing an exception. This exception is caught and processed by the catch block in Line 11.

### EXAMPLE 14-16

```cpp
// Handling exception, in the main function, thrown by another
// function. The function throws a different exception object.

#include <iostream>                              //Line 1
#include "divisionByZero.h"                      //Line 2

using namespace std;                              //Line 3

void doDivision() throw (divisionByZero);        //Line 4

int main()                                           //Line 5
{
    try                                             //Line 6
    {
        doDivision();                               //Line 9
    }                                               //Line 10
```
