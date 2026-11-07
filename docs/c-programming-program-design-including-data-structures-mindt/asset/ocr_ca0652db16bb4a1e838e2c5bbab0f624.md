In Sample Run 1, the value of `divisor` is nonzero, so no exception occurs. The program calculates and outputs the quotient and terminates normally. In Sample Run 2, the value entered for `divisor` is 0. The statement in Line 12 divides `dividend` by the `divisor`. However, the program does not check whether `divisor` is 0 before dividing `dividend` by `divisor`. So the program crashes with an error message shown. Notice that the error message is platform independent, that is, IDE dependent. Some IDEs might not give this error message and might simply hang.

Next, consider Example 14-2. This is the same program as in Example 14-1, except that in Line 8, the program checks whether `divisor` is zero.

# EXAMPLE 14-2

```
```cpp
// Checking division by zero.

#include <iostream>                                      //Line 1

using namespace std;                                     //Line 2

int main()                                               //Line 3
{
    int dividend, divisor, quotient;                     //Line 5

    cout << "Line 6: Enter the dividend: ";              //Line 6
    cin >> dividend;                                      //Line 7
    cout << endl;                                         //Line 8

    cout << "Line 9: Enter the divisor: ";               //Line 9
    cin >> divisor;                                       //Line 10
    cout << endl;                                         //Line 11

    if (divisor != 0)                                     //Line 12
    {
        quotient = dividend / divisor;                    //Line 14
        cout << "Line 15: Quotient = " << quotient       //Line 15
             << endl;
    }
    else                                                   //Line 17
        cout << "Line 18: Cannot divide by zero."         //Line 18
             << endl;

    return 0;                                             //Line 19
}                                                        //Line 20
```
```

# Sample Run 1:

```
```text
Line 6: Enter the dividend: 17
Line 9: Enter the divisor: 5
Line 15: Quotient = 3
```
```