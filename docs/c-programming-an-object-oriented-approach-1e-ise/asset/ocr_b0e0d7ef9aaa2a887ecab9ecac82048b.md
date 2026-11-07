![](bbox=[0.287, 0.083, 0.829, 0.196])

**Figure 6.6** Scaling and shifting a random number

introduce the random number generator inherited from the C language and defined in the `<cstdlib>` header file. The function is called *rand*. It generates a random integer between 0 and RAND_MAX, a value that is system dependent but is normally set to 32,767 (2<sup>15</sup> − 1), which means one of the 32,768 different values if we include 0.

This function is pseudorandom: It generates the same set of random numbers in each run of the program because it uses the same *seed* to start the random series. The seed is set to 1, which means that the same series is always generated. To get a different series in each run, we must give a different seed to the *rand* function each time we run the program. The best choice is to use the function *time(0)*, which is the number of seconds passed from the epoch, as we discussed before. Each time we run the program, the value of *time(0)* is different, which means we get a different set of random numbers. To do so, we simply pass the return value of *time(0)* to another function named *srand* (seed for random) and then call the *rand* function.

We often need to create a random number in the range *a* to *b* (inclusive). To do so, we must create a random number using the *rand* function. We then must scale it to the range 0 to (*b* – *a*). We finally shift it as shown in Figure 6.6.

# ### EXAMPLE 6.9

As an application of generating a random number, we have created a number-guessing game (see Program 6.7). We generate a random number between two limits (*low* and *high*) and let the user guess a limited number of times to find it. In each try, if the guess is not correct, we give a clue to the user.

# ### **Program 6.7** A guessing game

```
~~~cpp
/************************************************************
 * A program simulating a guessing game using a random number       *
 ************************************************************/
#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main ( )
{
  // Declaration and initialization
  int low = 5;
~~~
```