the variables but only prints them, the formal parameters are value parameters. The definition of this function is:

```
void printResults(int zeroCount, int oddCount, int evenCount)
{
    cout << "There are " << evenCount << " evens, "
         << "which includes " << zeroCount << " zeros"
         << endl;

    cout << "The number of odd numbers is: " << oddCount
         << endl;
} //end printResults
```

We now give the main algorithm and show how the function main calls these functions.

# MAIN ALGORITHM

+   1. Call the function initialize to initialize the variables.
+   2. Prompt the user to enter 20 numbers.
+   3. For each number in the list:
+      a. Call the function getNumber to read a number.
+      b. Output the number.
+      c. Call the function classifyNumber to classify the number and increment the appropriate count.
+   4. Call the function printResults to print the final results.

# COMPLETE PROGRAM LISTING

```
////////////////////////////////////////////////////////////
// Author: D.S. Malik
//
// Program: Classify Numbers
// This program reads 20 numbers and outputs the number of
// zeros, odd, and even numbers.
////////////////////////////////////////////////////////////

#include <iostream>
#include <iomanip>

using namespace std;

const int N = 20;

        //Function prototypes
void initialize(int& zeroCount, int& oddCount, int& evenCount);
void getNumber(int& num);
void classifyNumber(int num, int& zeroCount, int& oddCount,
                   int& evenCount);
void printResults(int zeroCount, int oddCount, int evenCount);
```