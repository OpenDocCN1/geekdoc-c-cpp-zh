
```
trial_factor++)
    is_prime = (value % trial_factor != 0);
    if (is_prime)
        std::cout << value << " "; // Display the prime number
}
std::cout << '\n'; // Move cursor down to next line
end_time = clock();
// Print the elapsed time
std::cout << "Elapsed time: "
    << static_cast<double>(end_time - start_time)/CLOCKS_PER_SEC
    << " sec." << '\n';
}
```

On one system, the program took 93 seconds, on average, to print all the prime numbers up to 500,000. By comparison, the newer, more efficient version, Listing 8.5 (moreefficientprimes.cpp), which uses the square root optimization takes only 15 seconds to display all the primes up to 500,000. Exact times will vary depending on the speed of the computer.

As it turns out, much of the program's execution time is taken up printing the output, not computing the prime numbers to print. We can compare the algorithms better by redirecting the program's output to a file. If the executable program is named primes.exe, you can redirect its output at the command line by issuing the command

```
primes > run1.out
```

This creates a text file named run1.out that can be viewed with any text editor. Its contents are exactly what would have been printed to the screen if the redirection is not used.

When run using redirection, the time difference is even more dramatic: The unoptimized version generates the prime numbers up to 500,000 in 77 seconds, while the optimized square root version requires only 2 seconds to generate the same number of primes! An even faster prime generator can be found in Listing 11.25 (fasterprimes.cpp); it uses a completely different algorithm to generate prime numbers.

You must #include the <ctime> header to use the standard time function in a program.

## 8.5 Character Functions

The C library provides a number of character functions that are useful to C++ programmers. Listing 8.9 (touppercase.cpp) converts lowercase letters to uppercase letters.

```
Listing 8.9: touppercase.cpp

#include <iostream>
#include <cctype>

int main() {
    for (char lower = 'a'; lower <= 'z'; lower++) {
        char upper = toupper(lower);
        std::cout << lower << " = " << upper << '\n';
    }
}
```

The first lines printed by Listing 8.9 (touppercase.cpp) are

```
a = A
b = B
c = C
d = D
```

Interestingly, the `toupper` function returns an `int`, not a `char`. At the enhanced warning level 4 for Visual C++ a cast is required to assign the result to the variable `upper`:

```
char upper = static_cast<char>(toupper(lower));
```

Some of the more useful character functions are described in Table 8.2.

| Function | Description |
| --- | --- |
| int toupper(int ch) | Returns the uppercase version of the given character, returns the original character if no uppercase version exists (such as for punctuation or digits) |
| int tolower(int ch) | Returns the lowercase version of the given character; returns the original character if no lowercase version exists (such as for punctuation or digits) |
| int isupper(int ch) | Returns a nonzero value (true) if ch is an uppercase letter ('A'-'Z'); otherwise, it returns 0 (false) |
| int islower(int ch) | Returns a nonzero value (true) if ch is an lowercase letter ('a'-'z'); otherwise, it returns 0 (false) |
| int isalpha(int ch) | Returns a nonzero value (true) if ch is a letter from the alphabet ('A'-'Z' or 'a'-'z'); otherwise, it returns 0 (false) |
| int isdigit(int ch) | Returns a nonzero value (true) if ch is a digit ('0'-'9'); otherwise, it returns 0 (false) |

Table 8.2: A few of the functions from the cctype library

Other functions exist to determine if a character is a punctuation character like a comma or semicolon (`ispunct`), a space, tab, or newline character (`isspace`).

To use the standard C character functions in your C++ program, you must include the `<cctype>` header file.

## 8.6 Random Numbers

Some applications require behavior that appears random. Random numbers are useful particularly in games and simulations. For example, many board games use a die (one of a pair of dice) to determine how many places a player is to advance. (See Figure 8.5.) A die or pair of dice are used in other games of chance. A die is a cube containing spots on each of its six faces. The number of spots range from one to six. A player rolls a die or sometimes a pair of dice, and the side(s) that face up have meaning in the game being played. The value of a face after a roll is determined at random by the complex tumbling of the die. A software adaptation of a game that involves dice would need a way to simulate the random roll of a die.

### Figure 8.5 A pair of dice

![](img/e84ad11adb18201d71595b31ce6c9eff_205_0.png)

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

This value obviously differs between program runs, so each execution will use a different seed value, and the generated pseudorandom number sequences will be different. Listing 8.11 (betterrandom.cpp) incorporates the time function to improve its randomness over multiple executions.

### Listing 8.11: betterrandom.cpp

```
#include <iostream>
#include <cstdlib>
#include <ctime>

int main() {
   srand(static_cast<unsigned>(time(0)));
   for (int i = 0; i < 100; ++i) {
      int r = rand();
      std::cout << r << " ";
   }
   std::cout << '\n';
}
```

Each execution of Listing 8.11 (betterrandom.cpp) produces a different pseudorandom number sequence. The actual type of value that time returns is time_t, so the result from a call to time must be cast to unsigned int before being used with srand.

Notice that the numbers returned by rand can be rather large. The pseudorandom values range from 0 to a maximum value that is implementation dependent. The maximum value for Visual C++'s rand function is 32,767, which corresponds to the largest 16-bit signed int value. The cstdlib header defines the constant RAND_MAX that represents the largest value in the range. The following statement

```
std::cout << RAND_MAX << '\n';
```

would print the value of RAND_MAX for a particular system.

Ordinarily we need values in a more limited range, like 1..100. Simple arithmetic with the modulus operator can produce the result we need. If n is any nonnegative integer and m is any positive integer, the expression

```
n % m
```

produces a value in the range 0...m-1.

This means the statement

```
int r = rand() % 100;
```

can assign only values in the range 0..99 to r. If we really want values in the range 1..100, what can we do? We simply need only add one to the result:

```
int r = rand() % 100 + 1;
```

This statement produces pseudorandom numbers in the range 1..100.

We now have all we need to write a program that simulates the rolling of a die.

Listing 8.12 (die.cpp) simulates rolling die.
