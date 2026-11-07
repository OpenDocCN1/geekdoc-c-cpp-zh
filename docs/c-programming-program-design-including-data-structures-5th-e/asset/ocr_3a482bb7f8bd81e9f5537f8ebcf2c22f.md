**Sample Run 2:**

Line 2: Enter the dividend: 24

Line 5: Enter the divisor: 0

Line 12: Cannot divide by zero.

In Sample Run 1, the value of divisor is nonzero, so no exception occurs. The program calculates and outputs the quotient and terminates normally.

In Sample Run 2, the value entered for divisor is 0. In Line 8, the program checks whether divisor is 0. Because divisor is 0, the expression in the `if` statement fails, so the `else` part executes, which outputs the third line of the sample run.

The program in Example 15-3 uses the function `assert` to determine whether the divisor is zero. If the divisor is zero, the function `assert` terminates the program with an error message.

# EXAMPLE 15-3

```
```cpp
// Division by zero and the assert function.

#include <iostream>
#include <cassert>

using namespace std;

int main()
{
    int dividend, divisor, quotient;                 //Line 1

    cout << "Line 2: Enter the dividend: ";         //Line 2
    cin >> dividend;                                 //Line 3
    cout << endl;                                    //Line 4

    cout << "Line 5: Enter the divisor: ";          //Line 5
    cin >> divisor;                                  //Line 6
    cout << endl;                                    //Line 7

    assert(divisor != 0);                            //Line 8
    quotient = dividend / divisor;                   //Line 9

    cout << "Line 10: Quotient = " << quotient      //Line 10
         << endl;

    return 0;                                        //Line 11
}
```
```

**Sample Run 1:**

Line 2: Enter the dividend: 26

Line 5: Enter the divisor: 7

Line 10: Quotient = 3