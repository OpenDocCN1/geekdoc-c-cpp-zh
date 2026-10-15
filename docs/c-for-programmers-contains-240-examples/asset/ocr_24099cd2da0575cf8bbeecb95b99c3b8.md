| C++ Standard Library header file | Explanation |
|---|---|
| <cstdio> | Contains function prototypes for the C-style standard input/output library functions and information used by them. This header file replaces header file <stdio.h>. |
| <locale> | Contains classes and functions normally used by stream processing to process data in the natural form for different languages (e.g., monetary formats, sorting strings, character presentation, etc.). |
| <limits> | Contains classes for defining the numerical data type limits on each computer platform. |
| <utility> | Contains classes and functions that are used by many C++ Standard Library header files. |

Fig. 6.6 | C++ Standard Library header files. (Part 3 of 3.)

# 6.7 Case Study: Random Number Generation

We now take a brief and hopefully entertaining diversion into a popular programming application, namely simulation and game playing. In this and the next section, we develop a game-playing program that includes multiple functions. The program uses many of the control statements and concepts discussed to this point.

The element of chance can be introduced into computer applications by using the C++ Standard Library function rand.

Consider the following statement:

```
i = rand();
```

The function rand generates an unsigned integer between 0 and RAND_MAX (a symbolic constant defined in the <cstdlib> header file). The value of RAND_MAX must be at least 32767—the maximum positive value for a two-byte (16-bit) integer. For GNU C++, the value of RAND_MAX is 2147483647; for Visual Studio, the value of RAND_MAX is 32767. If rand truly produces integers at random, every number between 0 and RAND_MAX has an equal chance (or probability) of being chosen each time rand is called.

The range of values produced directly by the function rand often is different than what a specific application requires. For example, a program that simulates coin tossing might require only 0 for “heads” and 1 for “tails.” A program that simulates rolling a six-sided die would require random integers in the range 1 to 6. A program that randomly predicts the next type of spaceship (out of four possibilities) that will fly across the horizon in a video game might require random integers in the range 1 through 4.

# Rolling a Six-Sided Die

To demonstrate rand, let us develop a program (Fig. 6.7) to simulate 20 rolls of a six-sided die and print the value of each roll. The function prototype for the rand function is in <cstdlib>. To produce integers in the range 0 to 5, we use the modulus operator (%) with rand as follows: