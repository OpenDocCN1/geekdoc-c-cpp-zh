> **NOTE.** You can declare a reference (formal) parameter as a constant by using the keyword `const`. This will prevent the formal parameter from being able to change the value of the corresponding actual parameter. Chapters 9 and 10 discuss constant reference parameters. Until then, the reference parameter that you use will be nonconstant as defined in this chapter. From the definition of a reference parameter, it follows that a constant value or an expression cannot be passed to a nonconstant reference parameter. If a formal parameter is a nonconstant reference parameter, during a function call, its corresponding actual parameter must be a variable.

# EXAMPLE 6-13

# Calculate Grade

The following program takes a course score (a value between 0 and 100) and determines a student’s course grade. This program has three functions: `main`, `getScore`, and `printGrade`, as follows:

+   1. `main`
+      a. Get the course score.
+      b. Print the course grade.
+   
+   2. `getScore`
+      a. Prompt the user for the input.
+      b. Get the input.
+      c. Print the course score.
+   
+   3. `printGrade`
+      a. Calculate the course grade.
+      b. Print the course grade.

The complete program is as follows:

```
```cpp
//This program reads a course score and prints the
//associated course grade.
#include <iostream>
using namespace std;

void getScore(int& score);
void printGrade(int score);

int main()
{
    int courseScore;
```
```