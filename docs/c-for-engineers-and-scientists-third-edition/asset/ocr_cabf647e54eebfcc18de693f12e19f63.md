# Chapter 11

# 11.5 A Case Study: Random Numbers and Simulations

There are many scientific and engineering problems in which probability must be considered or statistical sampling techniques must be used. For example, to simulate automobile flow or telephone usage patterns, statistical models are required. In addition, applications such as computer games and more involved gaming scenarios can only be described statistically. All these statistical models require generating random numbers—a series of numbers whose order cannot be predicted.

In practice, finding random numbers is hard. Dice are rare, cards are never shuffled completely and digital computers can handle only numbers in a finite range and with limited precision. The best we can do in most cases is pseudorandom numbers, which are random enough for the type of applications being programmed.

Some computers contain a library function that produces random numbers; all C++ compilers provide a general-purpose function, named rand() and defined in the Math class, for creating random numbers. This function produces a series of double-precision random numbers in the range 0.0 up to, but not including, RAND_MAX, a compiler-defined maximum constant.

Program 11.2 shows the general procedure for creating a series of N random numbers in C++. It uses the rand() function to generate a series of 10 random numbers.

![](bbox=[0.109, 0.452, 0.183, 0.492])

# Program 11.2

```
#include <iostream>
#include <ctime>
#include <cmath>
using namespace std;

int main()
{
    double randValue;
    int i;
    srand(NULL); // this generates the first "seed" value
    for (i = 1; i <= 10; i++)
    {
        randValue = rand();
        cout << randValue << endl;
    }
    return 0;
}
```