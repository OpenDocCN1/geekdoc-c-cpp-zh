# 3.1 Definition and use of Function 91

```
...
fun1 ();
...
}
```

Here fun1 calls fun2 and fun2 in turn calls fun1. These two calls constitute an indirect recursive call.

The essence of recursion is that it decomposes the original problem into a new problem, which may use the solution of the original problem. Continue the decom-position to this principle, and each new problem emerged is a simplified subset of the original problem. The ultimately decomposed problem should be one whose solution is already known. The procedure above is a finite recursive call. Only a finite recursive call makes sense; an infinite recursive call will not get any results and it makes no sense.

The procedure of a recursive call consists of two parts:

**First stage: Recurrence.** Decompose the original problem continuously into subproblems until we reach a known situation, at which point the recurrence ends. For example, we can make a decomposition as follows:

5! = 5 × 4! → 4! = 4 × 3! → 3! = 3 × 2! → 2! = 2 × 1! → 1! = 1 × 0 → 0! = 1

Unknown ←

**Second stage: Regression.** Starting from the known situation, use the result of the decomposed problem to solve the previous (more complex) problem. Repeat this pro-gressively according to the reversed order of the recurrence stage, until we reach the start of the recursion. The regression then ends and the whole recursion finishes. The regression procedure of calculating 5! is:

5! = 5 × 4! = 120 ← 4! = 4 × 3! = 24 ← 3! = 3 × 2! = 6 ← 2! = 2 × 1! = 2 ← 1! = 1 × 0 = 0! = 1

Unknown ←

**Example 3.8:** Compute n!

Analysis: The formula for calculating n! is:

```
n! = { n = 0
n(n - 1)! (n > 0
```

This formula is recursive, since it calculates a factorial by using another factorial. The ending condition of the recursion is n=0.

Source code:

```
//3_8.cpp
#include <iostream>
using namespace std;
```