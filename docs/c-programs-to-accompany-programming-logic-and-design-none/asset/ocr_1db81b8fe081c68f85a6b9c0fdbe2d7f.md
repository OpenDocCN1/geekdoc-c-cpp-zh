```
```cpp
// Telephone.cpp - This program determines telephone call
// charges.
#include <iostream>
using namespace std;
int main()
{
    int custAC, custNumber;
    int calledAC, calledNumber;
    int callMinutes;
    double callCharge;
    const int MAX_MINS = 20;
    const double CHARGE_1 = .15;
    const double CHARGE_2 = .20;
    custAC = 630;
    custNumber = 5551234;
    calledAC = 219;
    calledNumber = 5557890;
    callMinutes = 35;
    if(calledAC != custAC && callMinutes > MAX_MINS)
        callCharge = callMinutes * CHARGE_1;
    else
        callCharge = callMinutes * CHARGE_2;
    cout << "Customer Number: " << custAC << "-" << custNumber
         << endl;
    cout << "Called Number: " << calledAC << "-" << calledNumber
         << endl;
    cout << "The charge for this call is $" << callCharge << endl;
    return 0;
}
```
```

+   1. What is the exact output when this program executes?

+   2. What is the exact output if the value of `callMinutes` is changed to 20?

+   3. What is the exact output if the expression in the `if` statement is changed to `callMinutes >= MAX_MINS`?