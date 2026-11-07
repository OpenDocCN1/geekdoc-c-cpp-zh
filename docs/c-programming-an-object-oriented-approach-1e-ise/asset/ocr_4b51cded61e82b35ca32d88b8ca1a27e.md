function, *findMultiplier*, to calculate the *multiplier*. The *multiplier* is a number that must be multiplied by the original investment to give the future value at the end of the period. It can be defined as (multiplier = factor^period), in which the factor is (1 + rate / 100).

The **output** function The *output* function calls two functions, *printData* and *printResult*, to show what was input by the user and what was calculated.

# Write the Program

Program 6.26 shows the **main** function and the three functions called by *main*: *input*, *process*, and *output*. It also gives the definition of the *getInput* (called by *input*), *findMultiplier* (called by *process*), and *printData* and *printResult* (called by *output*).

# **Program 6.26**  Finding the future value of a fixed investment

```
```cpp
/************************************************************
 * The program shows how to use functions to calculate the future *
 * value of an investment that earns compound interest.         *
 ************************************************************/
#include <iostream>
#include <iomanip>
#include <cmath>
using namespace std;

// Declaration of top-level functions
void input (double& invest, double& rate, double& term);
void process (double invest, double rate, double term,
             double& multiplier, double& futureValue);
void output (double invest, double rate, double term,
             double multiplier, double& futureValue);
// Declaration of low-level functions
double getInput (string message);
double findMultiplier (double rate, double period);
void printData (double invest, double rate, double term);
void printResult (double multiplier, double value);

int main ( )
{
    // Variable Declaration
    double invest, rate, term;        // For input
    double multiplier, futureValue;   // For Result
    // Call first level functions
    input (invest, rate, term);
    process (invest, rate, term, multiplier, futureValue);
    output (invest, rate, term, multiplier, futureValue);
    return 0;
}
```
```