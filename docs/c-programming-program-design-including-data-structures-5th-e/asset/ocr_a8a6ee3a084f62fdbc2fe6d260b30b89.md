```
```cpp
{
    cout << "Line 14: Division by 0." << endl;  //Line 14
}

    return 0;                                      //Line 15
}
```
```

**Sample Run 1:** In this sample run, the user input is shaded.

Line 3: Enter the dividend: 17

Line 6: Enter the divisor: 8

Line 12: Quotient = 2

**Sample Run 2:** In this sample run, the user input is shaded.

Line 3: Enter the dividend: 34

Line 6: Enter the divisor: 0

Line 14: Division by 0.

This program works as follows. The statement in Line 1 declares the `int` variables *dividend*, *divisor*, and *quotient*. The `try` block starts at Line 2. The statement in Line 3 prompts the user to enter the value for the dividend; the statement in Line 4 stores this number in the variable dividend. The statement in Line 6 prompts the user to enter the value for the divisor, and the statement in Line 7 stores this number in the variable divisor. The statement in Line 9 checks whether the value of divisor is 0. If the value of divisor is 0, the statement in Line 10 throws the constant value 0. The statement in Line 11 calculates the quotient and stores it in quotient. The statement in Line 12 outputs the value of quotient.

The `catch` block starts in Line 13 and catches an exception of type `int`.

In Sample Run 1, the program does not throw any exception.

In Sample Run 2, the entered value of divisor is 0. Therefore, the statement in Line 10 throws 0, which is caught by the `catch` block starting in Line 13. The statement in Line 14 outputs the appropriate message.

The program in Example 15-6 is the same as the program in Example 15-5, except that the `throw` statement throws the value of the variable divisor.

# EXAMPLE 15-6

```
```cpp
// Handling division by zero exception.

#include <iostream>

using namespace std;
```
```