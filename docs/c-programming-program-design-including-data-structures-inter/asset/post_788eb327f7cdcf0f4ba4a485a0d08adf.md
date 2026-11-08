
Suppose that an exception is thrown in the try block. Because the catch block in Line 2 can catch exceptions of all types, the catch block in Line 3 cannot be reached. For this sequence of try/catch blocks, some compilers might, in fact, give a syntax error (check your compiler’s documentation).

In a sequence of try/catch blocks, if the catch block with an ellipsis (in the heading) is needed, then it should be the last catch block of that sequence.

## USING try/catch BLOCKS IN A PROGRAM

Next, we provide examples that illustrate how a try/catch block might appear in a program.

A common error that might occur when performing numeric calculations is division by zero with integer values. If, during program execution, division by zero occurs with integer values and is not addressed by the program, the program might terminate with an error message or might simply hang. Example 14-5 shows how to handle division by zero exceptions.

### EXAMPLE 14-5

This example illustrates how to catch and handle division by zero exceptions. It also shows how a try/catch block might appear in a program.

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
    {
        cout << "Line 14: Division by 0." << endl;  //Line 14
    }

    return 0;                                      //Line 15
}
```

**Sample Run 1:** In this sample run, the user input is shaded.

```
Line 3: Enter the dividend: 16
Line 6: Enter the divisor: 8
Line 12: Quotient = 2
```

**Sample Run 2:** In this sample run, the user input is shaded.

```
Line 3: Enter the dividend: 34
Line 6: Enter the divisor: 0
Line 14: Division by 0.
```

This program works as follows. The statement in Line 1 declares the int variables dividend, divisor, and quotient. The try block starts at Line 2. The statement in Line 3 prompts the user to enter the value for the dividend, and the statement in Line 4 stores this number in the variable dividend. The statement in Line 6 prompts the user to enter the value for the divisor, and the statement in Line 7 stores this number in the variable divisor. The statement in Line 9 checks whether the value of divisor is 0. If the value of divisor is 0, the statement in Line 10 throws the constant value 0. The statement in Line 11 calculates the quotient and stores it in quotient. The statement in Line 12 outputs the value of quotient.

The catch block starts in Line 13 and catches an exception of type int.

In Sample Run 1, the program does not throw any exception.

In Sample Run 2, the entered value of divisor is 0. Therefore, the statement in Line 10 throws 0, which is caught by the catch block starting in Line 13. The statement in Line 14 outputs the appropriate message.

The program in Example 14-6 is the same as the program in Example 14-5, except that the throw statement throws the value of the variable divisor.

### EXAMPLE 14-6

```cpp
// Handling division by zero exception.

#include <iostream>

using namespace std;

int main()
{
    int dividend, divisor, quotient;                 //Line 1

    try                                             //Line 2
    {
        cout << "Line 3: Enter the dividend: ";    //Line 3
        cin >> dividend;                            //Line 4
        cout << endl;                               //Line 5

        cout << "Line 6: Enter the divisor: ";     //Line 6
        cin >> divisor;                             //Line 7
        cout << endl;                               //Line 8

        if (divisor == 0)                           //Line 9
            throw divisor;                          //Line 10

        quotient = dividend / divisor;              //Line 11

        cout << "Line 12: Quotient = " << quotient
             << endl;                               //Line 12
    }
    catch (int x)                                   //Line 13
    {
        cout << "Line 14: Division by " << x
             << endl;                               //Line 14
    }

    return 0;                                       //Line 15
}
```

**Sample Run 1:** In this sample run, the user input is shaded.

Line 3: Enter the dividend: **14**

Line 6: Enter the divisor: **5**

Line 12: Quotient = 2

**Sample Run 2:** In this sample run, the user input is shaded.

Line 3: Enter the dividend: **23**

Line 6: Enter the divisor: **0**

Line 14: Division by 0

This program works the same way as the program in Example 14-5.

The program in Example 14-7 illustrates how to handle division by zero, division by a negative integer, and input failure exceptions. It also shows how to throw and catch an object. This program is similar to the programs in Examples 14-5 and 14-6.

### EXAMPLE 14-7

```cpp
// Handle division by zero, division by a negative integer,
// and input failure exceptions.

#include <iostream>
#include <string>

using namespace std;

int main()
{
    int dividend, divisor = 1, quotient;              //Line 1

    string inpStr
        = "The input stream is in the fail state.";   //Line 2

    try                                             //Line 3
    {
        cout << "Line 4: Enter the dividend: ";    //Line 4
        cin >> dividend;                            //Line 5
        cout << endl;                               //Line 6

        cout << "Line 7: Enter the divisor: ";     //Line 7
        cin >> divisor;                             //Line 8
        cout << endl;                               //Line 9

        if (divisor == 0)                           //Line 10
            throw divisor;                         //Line 11
        else if (divisor < 0)                      //Line 12
            throw string("Negative divisor.");     //Line 13
        else if (!cin)                             //Line 14
            throw inpStr;                           //Line 15

        quotient = dividend / divisor;              //Line 16

        cout << "Line 17: Quotient = " << quotient
             << endl;                               //Line 17
    }
    catch (int x)                                   //Line 18
    {
        cout << "Line 19: Division by " << x
             << endl;                               //Line 19
    }
    catch (string s)                                //Line 20
    {
        cout << "Line 21: " << s << endl;          //Line 21
    }

    return 0;                                       //Line 22
}
```

**Sample Run 1:** In this sample run, the user input is shaded.

Line 4: Enter the dividend: 23

Line 7: Enter the divisor: 6

Line 17: Quotient = 3

**Sample Run 2:** In this sample run, the user input is shaded.

Line 4: Enter the dividend: 34

Line 7: Enter the divisor: -6

Line 21: Negative divisor.

**Sample Run 3:** In this sample run, the user input is shaded.

Line 4: Enter the dividend: 34

Line 7: Enter the divisor: g

Line 21: The input stream is in the fail state.

In this program, the statements in Lines 1 and 2 declare the variables used in the program. Note that the string object inpStr is also initialized.

The statements in Lines 4 through 9 input the data into the variables dividend and divisor. The statement in Line 10 checks whether divisor is 0, the statement in Line 12 checks whether divisor is negative, and the statement in Line 14 checks whether the standard input stream is in the fail state.

The statement in Line 11 throws the variable divisor, the statement in Line 13 throws an anonymous string object with the string "Negative divisor.", and the statement in Line 15 throws the object inpStr.

The catch block in Line 18 catches an exception of type int, and the catch block in Line 20 catches an exception of type string. If the exception is thrown by the statement in Line 11, it is caught and processed by the catch block in Line 18. If the exception is thrown by the statements in Lines 13 or 15, it is caught and processed by the catch block in Line 20.

In Sample Run 1, the program does not encounter any problems. In Sample Run 2, division by a negative number occurs. In Sample Run 3, the standard input stream enters the fail state.

## Using C++ Exception Classes

C++ provides support to handle exceptions via a hierarchy of classes. The class exception is the base of the classes designed to handle exceptions. Among others, this class contains the function what. The function what returns a string containing an
