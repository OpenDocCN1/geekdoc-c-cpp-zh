# // QUIZ ANSWERS

1 Writing tests. You should, generally, write tests prior to writing code. The idea is to decide what your program needs to do by describing how it should perform on various tests before running the tests.

3 There are several possibilities, but here is one:

Pseudocode:

b Writing pseudocode. Pseudocode is part of the design process and can be used to create many of the comments in a program.

+   1 Collect information on assets

+   2 Collect information on debts

c Trick question! You should generally run tests while you write code: Some code, then test, write more code, then etc. Obviously, some code must be written before a test can be run over part of the code.

+   3 Collect information on credit history

+   4 Calculate loan amount eligible for and interest rate

+   5 Report information to user

d Generally, comments can be written before the code is written. It is especially true if the comments are taken from the pseudocode and describe the purpose of various parts of the code. But it is OK to write additional comments while writing code or after writing a piece of code.

Code:

```
// Calculate loan eligibility
#include<iostream>
using namespace std;
int main() {
    /* Collect Asset Information *
    /* Collect Debt Information *
    /* Collect Credit History Information *
    /* Calculate loan amount and rate */
    /* Report information to user */
}
```

2 Generally, you want to be sure to check your code special points where things change. For water, this would be 212* Fahrenheit. So, a thorough set of tests transition points would probably verify that the program works at the transition points, 32 and 212; a little on either side of the transition points (31, 33, 211, and 213); and a few points in the middle ranges, such as 10, 100, and 1000.

Click here to go back to the quiz.