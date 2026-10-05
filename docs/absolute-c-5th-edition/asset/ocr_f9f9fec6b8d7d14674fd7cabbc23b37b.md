# Chapter Summary

+   - There are two kinds of functions in C++: functions that return a value and void functions.

+   - A function should be defined so that it can be used as a black box. The programmer who uses the function should not need to know any details about how the function is coded. All the programmer should need to know the function declaration and the accompanying comment that describes the value returned. This rule is sometimes called the principle of procedural abstraction.

+   - A good way to write a function declaration comment is to use a precondition and a postcondition. The precondition states what is assumed to be true when the function is called. The postcondition describes the effect of the function call; that is, the postcondition tells what will be true after the function is executed in a situation with the precondition holds.

+   - A variable that is declared in a function definition is said to be local to the function.

+   - A formal parameter is a kind of placeholder that is filled in with a function argument when the function is called. The details on this “filling in” process are covered in Chapter 4.

# Answers to Self-Test Exercises

+   1. 4.0 4.0 8.0
8.0 8.0 1.21
3 3 0
3.0 3.5 3.5
6.0 6.0 5.0
5.0 4.5 4.5
3 3.0 3

+   2. a. sqrt (x + y)
b. pow(x, y + 7)
c. sqrt (area+time)/nobody
d. sqrt ((b -± sqrt(b*b - 4*a*c))/(2*a))
e. abs (x - y) or labs (x - y) or fabs (x - y)

```
3. #include <iostream>
#include <cmath>
using namespace std;
int main()
{
    int i;
```