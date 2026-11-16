# Figure 8.5 A pair of dice

![](bbox=[0.35, 0.16, 0.56, 0.31])

All algorithmic random number generators actually produce pseudorandom numbers, not true random numbers. A pseudorandom number generator has a particular period, based on the nature of the algorithm used. If the generator is used long enough, the pattern of numbers produced repeats itself exactly. A sequence of true random numbers would not contain such a repeating subsequence. The good news is that all practical algorithmic pseudorandom number generators have periods that are large enough for most applications.

C++ programmers can use two standard C functions for generating pseudorandom numbers: srand and rand:

```
void srand(unsigned)
int rand();
```

srand establishes the first value in the sequence of pseudorandom integer values. Each call to rand returns the next value in the sequence of pseudorandom values. Listing 8.10 (simplerandom.cpp) shows how a sequence of 100 pseudorandom numbers can be printed.

```
Listing 8.10: simplerandom.cpp

#include <iostream>
#include <cstdlib>

int main() {
    srand(23);
    for (int i = 0; i < 100; i++) {
        int r = rand();
        std::cout << r << " ";
    }
    std::cout << '\n';
}
```

The numbers printed by the program appear to be random. The algorithm is given a seed value to begin, and a formula is used to produce the next value. The seed value determines the sequence of numbers generated; identical seed values generate identical sequences. If you run the program again, the same sequence is displayed because the same seed value, 23, is used. In order to allow each program run to display different sequences, the seed value must be different for each run. How can we establish a different seed value for each run? The best way to make up a “random” seed at run time is to use the time function which is found in the ctime library. The call time(0) returns the number of seconds since midnight January 1, 1970.