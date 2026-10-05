```
// time how long it takes

// Largest potential prime considered
// const int MAX = 500000;
const int MAX = 500;

// Each position in the Boolean array indicates
// if the number of that position is not prime;
// false means "prime," and true means "composite."
// Initially all numbers are prime until proven otherwise
bool nonprimes[MAX]; // Global array initialized to all zeros

int main() {
    clock start_time = clock(); // Record start time
    // First prime number is 2; 0 and 1 are not prime
    nonprimes[0] = true;

    // Start at the first prime number, 2.
    for (int i = 2; i < MAX; i++) {
        if (!nonprimes[i]) {
            cout << i << ", \n            // It is prime, so eliminate all of its
            // multiples that cannot be prime
            for (int j = i+2; j < MAX; j += i)
                nonprimes[j] = true;
        }
    }
    cout << endl; // Move cursor down to next line
    // Print the elapsed time:
    cout << "Elapsed time: "
         << static_cast<double>(clock() - start_time)/CLOCKS_PER_SEC
         << " seconds" << endl;
}
```

Listing 8.8 (measuresprimespeed.cpp), which also prints all the prime numbers up to 500,000. Using reduction (Section 8.4), Listing 8.8 (measuresprimespeed.cpp) takes 77 seconds. In comparison, Listing F4 (fasterprimespeed.cpp) takes about two seconds to perform the same task on the system. This is comparable to the square root version, Listing 8.5 (moreefficientprimes.cpp), which takes two seconds to run. If the goal is to print the prime numbers up to 1,000,000, the original version averages 271 seconds, or about four and one half minutes. The square root version averages 4.5 seconds. The new, array-based version averages 25 seconds. For 5,000,000 the optimized original version takes over an hour and 33 minutes, the square root version takes a respectable 39 seconds, but array version averages 9 seconds to run.

# F.4 Multidimensional Arrays

The arrays we have so far have been one dimensional—simple sequences of values. C++ supports higher-dimensional arrays. A two-dimensional array is a block of memory that is visualized with rows and columns. The statement