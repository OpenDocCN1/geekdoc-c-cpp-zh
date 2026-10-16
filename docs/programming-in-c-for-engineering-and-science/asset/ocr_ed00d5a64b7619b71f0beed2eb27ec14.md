error results if an attempt is made to use them outside the function. One consequence of this is that an identifier outside the function may have the same name as a parameter or a local variable or constant inside the function.

# 6.3.5 Control Structures in Functions

Thus far, sequence has been the only control structure used in our examples of functions. However, selection and repetition structures may also be used. The program in Example 6.5 illustrates this by encapsulating in a function the code in Section 5.5 that used a for loop to calculate factorials.

# Example 6.5 Computing Factorials

```
/* This is a driver program to test the factorial() function.
--------------------------------------------------------------------------*/

#include <iostream>    // cin, cout, <<, >>
using namespace std;

unsigned factorial(unsigned n);    // prototype

int main()
{
    unsigned number;    // integer whose factorial is computed

    cout << "Enter a nonnegative integer: ";
    cin >> number;
    cout << number << "! = " << factorial(number) << endl;
}

/* factorial computes the factorial of a nonnegative integer

   Receive: n, a nonnegative integer
   Return:  n!
--------------------------------------------------------------------------*/

unsigned factorial(unsigned n)    // definition
{
    unsigned nfact = 1;
    for (unsigned i = 1; i <= n; i++)
        nfact *= i;

    return nfact;
}
```

# SAMPLE RUNS:

```
Enter a nonnegative integer: 0
0! = 1
```