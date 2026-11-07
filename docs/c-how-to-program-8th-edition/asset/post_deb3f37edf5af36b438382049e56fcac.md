
| Standard Library header | Explanation |
|---|---|
| `<limits>` | Contains classes for defining the numerical data type limits on each computer platform. |
| `<utility>` | Contains classes and functions that are used by many C++ Standard Library headers. |

**Fig. 6.7** | C++ Standard Library headers. (Part 3 of 3.)

## 6.7 Case Study: Random Number Generation

We now take a brief and hopefully entertaining diversion into a popular programming application, namely simulation and game playing. In this and the next section, we develop a game-playing program that includes multiple functions.

The element of chance can be introduced into computer applications by using the C++ Standard Library function `rand`. Consider the following statement:

```
i = rand();
```

The function `rand` generates an unsigned integer between 0 and `RAND_MAX` (a symbolic constant defined in the `<cstdlib>` header). You can determine the value of `RAND_MAX` for your system simply by displaying the constant. If `rand` truly produces integers at random, every number between 0 and `RAND_MAX` has an equal chance (or probability) of being chosen each time `rand` is called.

The range of values produced directly by the function `rand` often is different than what a specific application requires. For example, a program that simulates coin tossing might require only 0 for “heads” and 1 for “tails.” A program that simulates rolling a six-sided die would require random integers in the range 1 to 6. A program that randomly predicts the next type of spaceship (out of four possibilities) that will fly across the horizon in a video game might require random integers in the range 1 through 4.

### Rolling a Six-Sided Die

To demonstrate this, Fig. 6.8 simulates 20 rolls of a six-sided die and displays the value of each roll. The function prototype for the `rand` function is in `<cstdlib>`. To produce integers in the range 0 to 5, we use the modulus operator (`%`) with `rand` as follows:

```
rand() % 6
```

This is called **scaling**. The number 6 is called the **scaling factor**. We then **shift** the range of numbers produced by adding 1 to our previous result. Figure 6.8 confirms that the results are in the range 1 to 6.

**Fig. 6.8** | Shifted, scaled integers produced by `1 + rand() % 6`. (Part 1 of 2.)

```cpp
// Fig. 6.8: fig06_08.cpp
// Shifted and scaled random integers.
#include <iostream>
#include <iomanip>
#include <cstdlib> // contains function prototype for rand
using namespace std;

int main()
{
   // loop 20 times
   for ( int counter = 1; counter <= 20; ++counter )
   {
      // pick random number from 1 to 6 and output it
      cout << setw( 10 ) << ( 1 + rand() % 6 );

      // if counter is divisible by 5, start a new line of output
      if ( counter % 5 == 0 )
         cout << endl;
   } // end for
} // end main
```

| 6 | 6 | 5 | 5 | 6 |
|---|---|---|---|---|
| 5 | 1 | 1 | 5 | 3 |
| 6 | 6 | 2 | 4 | 2 |
| 6 | 2 | 3 | 4 | 1 |

**Fig. 6.8** | Shifted, scaled integers produced by `1 + rand() % 6`. (Part 2 of 2.)

### Rolling a Six-Sided Die 6,000,000 Times

To show that the numbers produced by `rand` occur with approximately equal likelihood, Fig. 6.9 simulates 6,000,000 rolls of a die. Each integer in the range 1 to 6 should appear approximately 1,000,000 times. This is confirmed by the program’s output.

**Fig. 6.9** | Rolling a six-sided die 6,000,000 times. (Part 1 of 2.)

```cpp
// Fig. 6.9: fig06_09.cpp
// Rolling a six-sided die 6,000,000 times.
#include <iostream>
#include <iomanip>
#include <cstdlib> // contains function prototype for rand
using namespace std;

int main()
{
   int frequency1 = 0; // count of 1s rolled
   int frequency2 = 0; // count of 2s rolled
   int frequency3 = 0; // count of 3s rolled
   int frequency4 = 0; // count of 4s rolled
   int frequency5 = 0; // count of 5s rolled
   int frequency6 = 0; // count of 6s rolled

   int face; // stores most recently rolled value

   // summarize results of 6,000,000 rolls of a die
   for ( int roll = 1; roll <= 6000000; ++roll )
   {
      face = 1 + rand() % 6; // random number from 1 to 6

      // determine roll value 1-6 and increment appropriate counter
      switch ( face )
      {
         case 1:
            ++frequency1; // increment the 1s counter
            break;
         case 2:
            ++frequency2; // increment the 2s counter
            break;
         case 3:
            ++frequency3; // increment the 3s counter
            break;
         case 4:
            ++frequency4; // increment the 4s counter
            break;
         case 5:
            ++frequency5; // increment the 5s counter
            break;
         case 6:
            ++frequency6; // increment the 6s counter
            break;
         default: // invalid value
            cout << "Program should never get here!";
      } // end switch
   } // end for

   cout << "Face" << setw( 13 ) << "Frequency" << endl; // output headers
   cout << "\n    1" << setw( 13 ) << frequency1
        << "\n    2" << setw( 13 ) << frequency2
        << "\n    3" << setw( 13 ) << frequency3
        << "\n    4" << setw( 13 ) << frequency4
        << "\n    5" << setw( 13 ) << frequency5
        << "\n    6" << setw( 13 ) << frequency6 << endl;
} // end main
```

| Face | Frequency |
|---:|---:|
| 1 | 999702 |
| 2 | 1000823 |
| 3 | 999378 |
| 4 | 998898 |
| 5 | 1000777 |
| 6 | 1000422 |

**Fig. 6.9** | Rolling a six-sided die 6,000,000 times. (Part 2 of 2.)

As the output shows, we can simulate the rolling of a six-sided die by scaling and shifting the values produced by `rand`. The program should never get to the default case (lines 45–46) in the switch structure, because the switch’s controlling expression (`face`) always has values in the range 1–6; however, we provide the default case as a matter of good practice. After we study arrays in Chapter 7, we show how to replace the entire switch structure in Fig. 6.9 elegantly with a single-line statement.

### Error-Prevention Tip 6.2

Provide a default case in a switch to catch errors even if you are absolutely, positively certain that you have no bugs!

![](img/bfd978e7e9b192bab46ec2a89e481263_243_0.png)

### Randomizing the Random Number Generator

Executing the program of Fig. 6.8 again produces

|   |   |   |   |   |
|---|---|---|---|---|
| 6 | 6 | 5 | 5 | 6 |
| 5 | 1 | 1 | 5 | 3 |
| 6 | 6 | 2 | 4 | 2 |
| 6 | 2 | 3 | 4 | 1 |

The program prints exactly the *same sequence* of values shown in Fig. 6.8. How can these be random numbers? *When debugging a simulation program, this repeatability is essential for proving that corrections to the program work properly.*

Function `rand` actually generates **pseudorandom numbers**. Repeatedly calling `rand` produces a sequence of numbers that appears to be random. However, the sequence repeats itself each time the program executes. Once a program has been thoroughly debugged, it can be conditioned to produce a different sequence of random numbers for each execution. This is called **randomizing** and is accomplished with the C++ Standard Library function `srand`. Function `srand` takes an unsigned integer argument and **seeds** the `rand` function to produce a different sequence of random numbers for each execution. The new C++ standard provides additional random number capabilities that can produce **nondeterministic random numbers**—a set of random numbers that can’t be predicted. Such random number generators are used in simulations and security scenarios where predictability is undesirable.

### Using Function srand

Figure 6.10 demonstrates function `srand`. The program uses the data type `unsigned`, which is short for `unsigned int`. An `int` is stored in at least two bytes of memory (typically four bytes on 32-bit systems and as much as eight bytes on 64-bit systems) and can have positive and negative values. A variable of type `unsigned int` is also stored in at least two bytes of memory. A two-byte `unsigned int` can have only nonnegative values in the range 0–65535. A four-byte `unsigned int` can have only nonnegative values in the range 0–4294967295. Function `srand` takes an `unsigned int` value as an argument. The function prototype for the `srand` function is in header `<cstdlib>`.

```cpp
// Fig. 6.10: fig06_10.cpp
// Randomizing the die-rolling program.
#include <iostream>
#include <iomanip>
#include <cstdlib> // contains prototypes for functions srand and rand
using namespace std;

int main()
{
   unsigned seed; // stores the seed entered by the user
```

**Fig. 6.10** | Randomizing the die-rolling program. (Part 1 of 2.)
