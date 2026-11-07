```
```cpp
}
else if (num == 2)
{
    return true;
}
return isPrime(2, num);
}
```
```

Note that after taking care of the two special cases, the nonrecursive function calls the recursive function with divisor 2 to start. Program 17.12 shows the complete program using the two functions.

# **Program 17.12** Testing the primeness of an integer

```
```cpp
/********************************************************
 * A program to test the primeness of an integer        *
 ********************************************************/
#include <iostream>
#include <cmath>
using namespace std;

// Declaration of a non-recursive and a recursive function
bool isPrime(int num);
bool isPrime(int div, int num);

int main( )
{
    // Testing the primeness of some integers
    cout << "Is 1 prime?  " << boolalpha << isPrime(1) << endl;
    cout << "Is 2 prime?  " << boolalpha << isPrime(2) << endl;
    cout << "Is 7 prime?  " << boolalpha << isPrime(7) << endl;
    cout << "Is 21 prime? " << boolalpha << isPrime(21) << endl;
    cout << "Is 59 prime? " << boolalpha << isPrime(59) << endl;
    cout << "Is 97 prime? " << boolalpha << isPrime(97) << endl;
    cout << "Is 301 prime?" << boolalpha << isPrime(301) << endl;
    return 0;
}
// Definition of non-recursive function calling the recursive function
bool isPrime(int num)
{
    if (num <= 1)
    {
        return false;
    }
    else if (num == 2)
    {
```
```