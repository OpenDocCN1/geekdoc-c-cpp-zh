
```cpp
catch (divisionByZero divByZeroObj)                         //Line 13
{
    cout << "Line 14: In the divisionByZero "
         << "catch block: "
         << divByZeroObj.what() << endl;                    //Line 14

    return 0;                                               //Line 15
}
```

**Sample Run 1:** In this sample run, the user input is shaded.

Line 3: Enter the dividend: 34

Line 6: Enter the divisor: 5

Line 12: Quotient = 6

**Sample Run 2:** In this sample run, the user input is shaded.

Line 3: Enter the dividend: 56

Line 6: Enter the divisor: 0

Line 14: In the divisionByZero catch block: Found division by zero

This program works the same way as the program in Example 14-11. The details are left as an exercise for you.

In the programs in Examples 14-11 and 14-12, the data manipulation is done in the function main. Therefore, the exception is thrown, caught, and processed in the function main. The program in Example 14-13 uses the user-defined function doDivision to manipulate the data. Therefore, the exception is thrown, caught, and processed in the function doDivision.

### EXAMPLE 14-13

```cpp
// Handling an exception thrown by a function.

#include <iostream>
#include "divisionByZero.h"

using namespace std;

void doDivision();

int main()
{
    doDivision();                                             //Line 1

    return 0;                                                  //Line 2
}

void doDivision()
{
    int dividend, divisor, quotient;                         //Line 3

    try
    {
        cout << "Line 4: Enter the dividend: ";             //Line 4
        cin >> dividend;                                     //Line 5
        cout << endl;                                        //Line 6

        cout << "Line 7: Enter the divisor: ";              //Line 7
        cin >> divisor;                                      //Line 8
        cout << endl;                                        //Line 9

        if (divisor == 0)                                    //Line 10
            throw divisionByZero();                          //Line 11

        quotient = dividend / divisor;                        //Line 12
        cout << "Line 13: Quotient = " << quotient
             << endl;                                        //Line 13
    }
    catch (divisionByZero divByZeroObj)                       //Line 14
    {
        cout << "Line 15: In the function "
             << "doDivision: " << divByZeroObj.what() << endl; //Line 15
    }
}
```

**Sample Run 1:** In this sample run, the user input is shaded.

Line 4: Enter the dividend: 34

Line 7: Enter the divisor: 5

Line 13: Quotient = 6

**Sample Run 2:** In this sample run, the user input is shaded.

Line 4: Enter the dividend: 56

Line 7: Enter the divisor: 0

Line 15: In the function doDivision: Division by zero

### EXAMPLE 14-14

Example 10-8 defined the **class** `circleType` to implement the basic properties of a circle. If a `circleType` object tries to set the radius to a negative number, then the function `setRadius` of this class sets the radius to 0. In this example, first we define the **class** `negativeNumber` to handle negative number exceptions and then use this class to throw an exception if a `circleType` object tries to set the radius to a negative number. So consider the following class:

```cpp
// User-defined exception class.

#include <iostream>
#include <string>

using namespace std;

class negativeNumber
{
public:
    negativeNumber()
    {
        message = "Number cannot be negative";
    }

    negativeNumber(string str)
    {
        message = str + " cannot be negative";
    }

    string what()
    {
        return message;
    }

private:
    string message;
};
```

Note that the definition of the **class** `negativeNumber` is similar to the definition of the **class** `divisionByZero`.

The definition of the **class** `circleType` is the same as in Example 10-8, except for the definition of function `setRadius`. The modified definition of this function is:

```cpp
void circleType::setRadius(double r)
{
    if (r < 0)
        throw negativeNumber("Radius");

    radius = r;
}
```

If the value of the parameter `r` is a negative number, the function `setRadius` throws a `negativeNumber` object. In this case, the value of the instance variable `message` of the object thrown is "Radius cannot be negative." The user program will handle the exception, if any, thrown by this function.

Consider the following program:

```cpp
// The user program that uses the class circleType

#include <iostream>
#include <iomanip>
#include "circleType.h"
#include "negativeNumber.h"

using namespace std;                                      //Line 1
int main()                                                //Line 2
{                                                         //Line 3
    circleType circle;

    double radius;                                         //Line 4

    cout << fixed << showpoint << setprecision(2);        //Line 5
    try                                                   //Line 6
    {                                                     //Line 7
        cout << "Line 8: Enter the radius of a circle: "; //Line 8
        cin >> radius;                                    //Line 9
        cout << endl;                                     //Line 10

        circle.setRadius(radius);                         //Line 11

        cout << "Line 12: circle - "
             << "radius: " << circle.getRadius()
             << ", area: " << circle.area()
             << ", circumference: "
             << circle.circumference() << endl;           //Line 12
    }                                                     //Line 13
    catch (negativeNumber obj)                             //Line 14
    {                                                     //Line 15
        cout << "Line 16: " << obj.what() << endl;        //Line 16
    }                                                     //Line 17

    return 0;                                             //Line 18
}//end main                                               //Line 19
```

**Sample Run 1:** In this sample run, the user input is shaded.

Line 8: Enter the radius of a circle: 4.75

Line 12: circle - radius: 4.75, area: 70.88, circumference: 29.85

**Sample Run 2:** In this sample run, the user input is shaded.

Line 8: Enter the radius of a circle: -2.65

Line 16: Radius cannot be negative

The preceding program works as follows. The statement in Line 3 creates the circleType object circle and using the default constructors sets the radius to 0.0. The statement in Line 4 declares the **double** variable radius. The **try/catch** block, between Lines 7 and 17 contains the code to prompt the user to enter the radius of the circle and depending on the value entered by the user generates the output. For example, if the user enters a nonnegative radius, the statement in Line 11 sets the radius of the circle and the statement in Line 12 outputs the radius, area, and the perimeter of the circle. If the user enters a negative number, the statement in Line 11 throws an exception, which is a negativeNumber object, and the **catch** block processes the exception. In Sample Run 1, the user enters 4.75, a nonnegative number, and the program outputs the radius, area, and the perimeter of the circle. In Sample Run 2, the user enters −2.65, which is a negative number, and the statement in Line 16 outputs that the radius cannot be negative.

## Rethrowing and Throwing an Exception

When an exception occurs in a `try` block, control immediately passes to one of the `catch` blocks. Typically, a `catch` block either handles the exception or partially processes the exception and then rethrows the same exception, or it rethrows another exception in order for the calling environment to handle the exception. The `catch` block in Examples 14–4 through 14–14 handles the exception. The mechanism of rethrowing or throwing an exception is quite useful in cases in which a `catch` block catches the exception but cannot handle the exception, or if the `catch` block decides that the exception should be handled by the calling block or environment. This allows the programmer to provide the exception-handling code all in one place.

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
void expThrowExcep(int x) throw (int, string, divisionByZero)
{
    .
    .
    .
    //include the appropriate throw statements
    .
}
```

The program in Example 14–15 further explains how a function specifies the exception it throws.

### EXAMPLE 14-15

```cpp
// Handling an exception, in the main function, thrown by another
// function. The function throws the same exception object.

#include <iostream>
#include "divisionByZero.h"
```
