# OTHER GENERATION METHODS

The only "new" feature here is the #include statement that brings in the class prototype in FM2. Notice that quotes appear instead of < > telling the preprocessor to look for the header file in the current directory. Finally, the code that actually uses the FM2 class is just the main function in Library 4.2 after having the initial statements

```
#include <iostream>
#include "FM2.h"
#include <new>
using std::cout; using std::cin; using std::endl;
```

at.g., being in the necessary header file. The corresponding code was collected in the file driverFM2.cpp.

At this point the original set of code in Library 4.2 has been split into three distinct parts. By doing this FM2 class has finished with an independent identity that allows it to be employed in other programs. All the pieces are cobbled together in a way that produces an executable program through the use of the myfile below.

```
driverFM2 : FM2.o driverFM2.o
gall -W2 driverFM2.o -o driverFM2

FM2.o : FM2.cpp FM2.h
gall -c FM2.cpp
ndriverFM2.o : driverFM2.cpp FM2.h
gall -Wall -c driverFM2.cpp
```

This produces the executable driverFM2 that can be used, as before, to obtain from the program.

# 4.5 Other generation methods

The periods of linear congruential generators are too small to be effective in many modern applications. This section describes PRNGs with much longer periods that are better suited for general use.

Before proceeding further it is worthwhile to clarify what we can mean by the phrase "longer period". To put this in proper context we can begin by thinking of linear congruential generators. This type of generator produces a sequence of integers (that are transformed into values in the unit interval) such that every number in the sequence is unique. If, for example, the modulus of a multiplicative generator is 2^{31}, having full period means from an initial seed the generator can march through 2^{31} numbers without ever repeating a previously generated value. In contrast, the generators discussed in this section have periods of 2^p where p is essentially arbitrary and, in particular, independent of a computer's storage format or word length. The maximum width is w bits (e.g., w = 64 in a 64-bit machine) the computer can only produce numbers that can be represented with w bits (e.g., the largest is 2^w-1 in a 64-bit storage environment). To achieve a period longer than 2^w-1 it is necessary that individual integer values appear multiple in the pseudo-random number stream. The result will be a sequence of integers in which the position (rather than value) of each number in the sequence is unique until the entire sequence begins again. The length of the sequence until it begins to repeat is what will be called the period of the generator.

Tauswort (1965) proposed a class of random number generators that are referred to as linear feedback shift register generators. Although these particular generators are not held in high regard, their extensions are widely used and provide some of what are arguably the best generators that are currently available.