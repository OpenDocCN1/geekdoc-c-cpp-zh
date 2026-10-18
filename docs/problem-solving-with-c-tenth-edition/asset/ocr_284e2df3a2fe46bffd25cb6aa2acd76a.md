With this change, x can be initialized to any number and the loop will still terminate.

A program that is in an infinite loop will run forever unless some external force stops it. Since you can now write programs that contain an infinite loop, it is a good idea to learn how to force a program to terminate. The method for forcing a program to stop varies from system to system. The keystrokes Control-C will terminate a program on many systems. (To type a Control-C, hold down the Control key while pressing the C key.)

# DISPLAY 2.16  Charge Card Program

```
```cpp
#include <iostream>
using namespace std;
int main( )
{
    double balance = 50.00;
    int count = 0;
    cout << "This program tells you how long it takes\n"
         << "to accumulate a debt of $100, starting with\n"
         << "an initial balance of $50 owed.\n"
         << "The interest rate is 2% per month.\n";

    while (balance < 100.00)
    {
        balance = balance + 0.02 * balance;
        count++;
    }

    cout << "After " << count << " months,\n";
    cout.setf(ios::fixed);
    cout.setf(ios::showpoint);
    cout.precision(2);
    cout << "your balance due will be $" << balance << endl;
    return 0;
}
```
```

# Sample Dialogue

> This program tells you how long it takes
> to accumulate a debt of $100, starting with
> an initial balance of $50 owed.
> The interest rate is 2% per month.
> After 36 months,
> your balance due will be $101.99