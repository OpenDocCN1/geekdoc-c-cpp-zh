
| Header | Description |
|---|---|
|  | Deeper Look. |
| `<cmath>` | Contains function prototypes for math library functions (Section 6.3). |
| `<cstdlib>` | Contains function prototypes for conversions of numbers to text, text to numbers, memory allocation, random numbers and various other utility functions. Portions of the header are covered in Section 6.7; Chapter 11, Operator Overloading; Class `string`; Chapter 17, Exception Handling: A Deeper Look; Chapter 22, Bits, Characters, C Strings and `struct`s; and Appendix F, C Legacy Code Topics. |
| `<ctime>` | Contains function prototypes and types for manipulating the time and date. This header is used in Section 6.7. |
| `<array>`, `<vector>`, `<list>`, `<forward_list>`, `<deque>`, `<queue>`, `<stack>`, `<map>`, `<unordered_map>`, `<unordered_set>`, `<set>`, `<bitset>` | These headers contain classes that implement the C++ Standard Library containers. Containers store data during a program’s execution. The `<vector>` header is first introduced in Chapter 7, Class Templates `array` and `vector`; Catching Exceptions. We discuss all these headers in Chapter 15, Standard Library Containers and Iterators. `<array>`, `<forward_list>`, `<unordered_map>` and `<unordered_set>` were all introduced in C++11. |
| `<cctype>` | Contains function prototypes for functions that test characters for certain properties (such as whether the character is a digit or a punctuation), and function prototypes for functions that can be used to convert lowercase letters to uppercase letters and vice versa. These topics are discussed in Chapter 22, Bits, Characters, C Strings and `struct`s. |
| `<cstring>` | Contains function prototypes for C-style string-processing functions. |
| `<typeinfo>` | Contains classes for runtime type identification (determining data types at execution time). This header is discussed in **Section 12.9**. |
| `<exception>`, `<stdexcept>` | These headers contain classes that are used for exception handling (discussed in **Chapter 17**, Exception Handling: A Deeper Look). |
| `<memory>` | Contains classes and functions used by the C++ Standard Library to allocate memory to the C++ Standard Library containers. This header is used in **Chapter 17**, Exception Handling: A Deeper Look. |
| `<fstream>` | Contains function prototypes for functions that perform input from and output to files on disk (discussed in **Chapter 14**, File Processing). |
| `<string>` | Contains the definition of class `string` from the C++ Standard Library (discussed in **Chapter 21**, Class `string` and String Stream Processing). |
| `<sstream>` | Contains function prototypes for functions that perform input from strings in memory and output to strings in memory (discussed in **Chapter 21**, Class `string` and String Stream Processing). |
| `<functional>` | Contains classes and functions used by C++ Standard Library algorithms. This header is used in **Chapter 16**. |
| `<iterator>` | Contains classes for accessing data in the C++ Standard Library containers. This header is used in **Chapter 15**. |
| `<algorithm>` | Contains functions for manipulating data in C++ Standard Library containers. This header is used in **Chapter 15**. |
| `<cassert>` | Contains macros for adding diagnostics that aid program debugging. This header is used in **Appendix E**, Preprocessor. |
| `<cfloat>` | Contains the floating-point size limits of the system. |
| `<climits>` | Contains the integral size limits of the system. |
| `<cstdio>` | Contains function prototypes for the C-style standard input/output library functions. |
| `<locale>` | Contains classes and functions normally used by stream processing to process data in the natural form for different languages (e.g., monetary formats, sorting strings, character presentation, etc.). |
| `<limits>` | Contains classes for defining the numerical data type limits on each computer platform—this is C++’s version of `<climits>` and `<cfloat>`. |
| `<utility>` | Contains classes and functions that are used by many C++ Standard Library headers. |

## 6.7 Case Study: Random-Number Generation²

². In Section 6.9, we’ll present C++11’s random-number capabilities for building more secure applications.

We now take a brief and hopefully entertaining diversion into a popular programming application, namely simulation and game playing. In this and the next section, we develop a game-playing program that includes multiple functions.

The element of chance can be introduced into computer applications by using the C++ Standard Library function `rand`. Consider the following statement:

```cpp
i = rand();
```

The function `rand` generates an unsigned integer between 0 and `RAND_MAX` (a symbolic constant defined in the `<cstdlib>` header). You can determine the value of `RAND_MAX` for your system simply by displaying the constant. If `rand` truly produces integers at random, every number between 0 and `RAND_MAX` has an equal *chance* (or probability) of being chosen each time `rand` is called.

The range of values produced directly by the function `rand` often is different than what a specific application requires. For example, a program that simulates coin tossing might require only 0 for “heads” and 1 for “tails.” A program that simulates rolling a six-sided die would require random integers in the range 1 to 6. A program that randomly predicts the next type of spaceship (out of four possibilities) that will fly across the horizon in a video game might require random integers in the range 1 through 4.

### 6.7.1 Rolling a Six-Sided Die

To demonstrate `rand`, **Fig. 6.6** simulates 20 rolls of a six-sided die and displays the value of each roll. The function prototype for the `rand` function is in `<cstdlib>`. To produce integers in the range 0 to 5, we use the remainder operator (`%`) with `rand` as follows:

```c
rand() % 6
```

This is called **scaling**. The number 6 is called the **scaling factor**. We then **shift** the range of numbers produced by adding 1 to our previous result. **Figure 6.6** confirms that the results are in the range 1 to 6. If you execute this program more than once, you’ll see that it produces the same “random” values each time. We’ll show how to fix this in **Figure 6.8**.

```cpp
// Fig. 6.6: fig06_06.cpp
// Shifted, scaled integers produced by 1 + rand() % 6.
#include <iostream>
#include <iomanip>
#include <cstdlib> // contains function prototype for rand
using namespace std;

int main() {
   // loop 20 times
   for (unsigned int counter{}; counter <= 20; ++counter) {
      // pick random number from 1 to 6 and output it
      cout << setw(10) << (1 + rand() % 6);

      // if counter is divisible by 5, start a new line of output
      if (counter % 5 == 0) {
         cout << endl;
      }
   }
}
```

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_730_0.png)

Fig. 6.6 Shifted, scaled integers produced by `1 + rand() % 6`.

### 6.7.2 Rolling a Six-Sided Die 60,000,000 Times

To show that values produced by `rand` occur with approximately equal likelihood, **Fig. 6.7** simulates 60,000,000 rolls of a die. Each integer in the range 1 to 6 should appear approximately 10,000,000 times (one-sixth of the rolls). This is confirmed by the program’s output.

```cpp
// Fig. 6.7: fig06_07.cpp
// Rolling a six-sided die 60,000,000 times.
#include <iostream>
#include <iomanip>
#include <cstdlib> // contains function prototype for rand
using namespace std;

int main() {
   unsigned int frequency1{0}; // count of 1s rolled
   unsigned int frequency2{0}; // count of 2s rolled
   unsigned int frequency3{0}; // count of 3s rolled
   unsigned int frequency4{0}; // count of 4s rolled
   unsigned int frequency5{0}; // count of 5s rolled
   unsigned int frequency6{0}; // count of 6s rolled
   int face; // stores each roll of the die

   // summarize results of 60,000,000 rolls of a die
   for (unsigned int roll{1}; roll <= 60'000'000; ++roll) {
      face = 1 + rand() % 6; // random number from 1 to 6

      // determine roll value 1-6 and increment appropriate counter
      switch (face) {
         case 1:
            ++frequency1; // increment the 1s counter
            break;
         case 2:
            ++frequency2; // increment the 2s counter
            break;
         case 3:
            ++frequency3; // increment the 3s counter
            break;
```
