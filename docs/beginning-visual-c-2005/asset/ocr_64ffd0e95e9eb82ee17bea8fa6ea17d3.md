# Arrays, Strings, and Pointers

is equivalent to this:

```
data[3] = data[4];
```

When you want to de-reference a pointer after incrementing the address it contains, the parentheses are necessary because the precedence of the indirect operator is higher than that of the arithmetic operators, + or -. If you write the expression *pdata + 1, instead of *(pdata + 1), this adds one to the value stored at the address contained in pdata, which is equivalent to executing data[2] + 1. Because this isn't an lvalue, its use in the previous assignment statement causes the compiler to generate an error message.

You can use an array name as though it were a pointer for addressing elements of an array. If you have the same one-dimensional array as before, declared as

```
long data[5];
```

using pointer notation, you can refer to the element data[3] for example as *(data + 3). This kind of notation can be applied generally so that, corresponding to the elements data[0], data[1], data[2], you can write *data, *(data + 1), *(data+2), and so on.



# Array Names as Pointers

You could exercise this aspect of array addressing with a program to calculate prime numbers (a prime number is divisible only by itself and one).

```
// Ex4_09.cpp
// Calculating primes
#include <iostream>
#include <cmath>
using std::cout;
using std::endl;
using std::setw;

int main()
{
  const int MAX = 100; // Number of primes required
  long primes[MAX] = { 2,3,5 }; // First three primes defined
  long trial = 5; // Candidate prime
  int count = 3; // Count of primes found
  int found = 0; // Indicates when a prime is found

  do
  {
    trial += 2; // Next value for checking
    found = 0; // Set found indicator
    for(int i = 0; i < count; i++) // Try division by existing primes
    {
      found = (trial % *(primes + i)) == 0; // True for exact division
      if(found) // If division is exact
        break; // it's not a prime
    }
    if (found == 0) // We got one...
  }
```