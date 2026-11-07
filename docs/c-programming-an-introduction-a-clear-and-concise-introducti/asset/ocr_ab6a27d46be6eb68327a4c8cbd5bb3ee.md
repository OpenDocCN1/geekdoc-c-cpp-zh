function is complete, the actual vector values will be the same as they were just before we called the function.

The answer, of course, is to pass the vector by reference to the function, just as we learned to do when we passed the arguments to the `swap()` function by reference. Let's create a function called `CurveGrades()` that adds 5 points to each grade in a vector:

```
void CurveGrades(vector<int> &n)
{
    for(int i = 0; i < n.size(); ++i)
    {
        n[i] += 5;  // add 5 to each vector element
    }
}
```

We pass the vector by reference by placing the reference operator `(&)` before the parameter name in the parameter list. Now when we make changes to the vector in the function, the changes will persist in the calling program.

Here is a complete program demonstrating how to pass a vector by reference:

```
// VectorFunctions.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <vector>
#include <cstdlib>
#include <ctime>
using namespace std;

void DisplayVector(vector<int> n)
{
    for(int i = 0; i < n.size(); ++i)
    {
```