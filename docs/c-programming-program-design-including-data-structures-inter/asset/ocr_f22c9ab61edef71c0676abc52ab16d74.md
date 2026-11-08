Repeat Steps c.2 through c.5 until the Fibonacci number you want is calculated.

The following while loop executes Steps c.2 through c.5 and determines the nth Fibonacci number.

```
```cpp
while (counter <= nthFibonacci)
{
    current = previous2 + previous1;
    previous1 = previous2;
    previous2 = current;
    counter++;
}
```
```

+   7. Output the nthFibonacci number, which is current.

# COMPLETE PROGRAM LISTING

```
```cpp
/************************************************************
// Authors: D.S. Malik
//
// Program: nth Fibonacci number
// Given the first two numbers of a Fibonacci sequence, this
// program determines and outputs the desired number of the
// Fibonacci sequence.
/************************************************************/

#include <iostream>

using namespace std;

int main()
{
            //Declare variables
            int previous1;
            int previous2;
            int current;
            int counter;
            int nthFibonacci;

            cout << "Enter the first two Fibonacci "
                 << "numbers: ";                         //Step 1
            cin >> previous1 >> previous2;                 //Step 2
            cout << endl;
            cout << "The first two Fibonacci numbers are "
                 << previous1 << " and " << previous2
                 << endl;                                  //Step 3
            cout << "Enter the position of the desired "  //Step 4
                 << "Fibonacci number: ";
            cin >> nthFibonacci;                            //Step 5
            cout << endl;

            if (nthFibonacci == 1)                          //Step 6.a
                current = previous1;
```
```