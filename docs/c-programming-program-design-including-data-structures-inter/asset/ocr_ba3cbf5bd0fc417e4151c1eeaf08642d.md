Suppose that an exception is thrown in the try block. Because the catch block in Line 2 can catch exceptions of all types, the catch block in Line 3 cannot be reached. For this sequence of try/catch blocks, some compilers might, in fact, give a syntax error (check your compiler’s documentation).

In a sequence of try/catch blocks, if the catch block with an ellipses (in the heading) is needed, then it should be the last catch block of that sequence.

# USING try/catch BLOCKS IN A PROGRAM

Next, we provide examples that illustrate how a try/catch block might appear in a program.

A common error that might occur when performing numeric calculations is division by zero with integer values. If, during program execution, division by zero occurs with integer values and is not addressed by the program, the program might terminate with an error message or might simply hang. Example 14-5 shows how to handle division by zero exceptions.

# EXAMPLE 14-5

This example illustrates how to catch and handle division by zero exceptions. It also shows how a try/catch block might appear in a program.

```
```cpp
// Handling division by zero exception.

#include <iostream>

using namespace std;

int main()
{
    int dividend, divisor, quotient;                 //Line 1

    try                                            //Line 2
    {
        cout << "Line 3: Enter the dividend: ";    //Line 3
        cin >> dividend;                           //Line 4
        cout << endl;                               //Line 5

        cout << "Line 6: Enter the divisor: ";     //Line 6
        cin >> divisor;                            //Line 7
        cout << endl;                               //Line 8

        if (divisor == 0)                           //Line 9
            throw 0;                                //Line 10

        quotient = dividend / divisor;              //Line 11

        cout << "Line 12: Quotient = " << quotient //Line 12
        << endl;
    }
    catch (int)                                      //Line 13
```
```