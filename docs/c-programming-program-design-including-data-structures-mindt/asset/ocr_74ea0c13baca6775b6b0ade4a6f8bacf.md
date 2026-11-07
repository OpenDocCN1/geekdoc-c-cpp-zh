# **EXAMPLE 14-15**

```
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
```