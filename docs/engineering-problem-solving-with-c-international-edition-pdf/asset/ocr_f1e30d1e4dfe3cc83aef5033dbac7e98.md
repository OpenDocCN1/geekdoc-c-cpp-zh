# Refinement in Pseudocode

```
main: read resistor values and voltage values
    specify array coefficients. a[i] [j]
    set index to zero
    while index <= n - 2
        eliminate(a,n,index)
        increment index by 1
    back.substitute(a,n,soln)
    print current values
eliminate(a,index):
    set row to index + 1
    while row <= n-1
        set scale.factor to -a[row] [index]
                                 a[index] [index]
        set a[row] [index] to zero

        set col to index + 1
        while col <= n
            add a[index] [col] . scale.factor
                to a[row] [col]
            increment col by 1
        increment row by 1
back.substitute(a,n,soln):
    set soln[n-1] to   a[n-1] [n]
                       a[n-1] [n-1]
    set row to n-2
    while row >= 0
        set col to n-1
        while col => row + 1
            subtract soln[col] . a[row] [col]
                from a[row] [n]
            subtract 1 from col
        set soln[row] to   a[row] [n]
                           a[row] [row]
        subtract 1 from row
```

Once we are comfortable with the pseudocode, it is relatively straightforward to convert it to C++:

```
/* ...........................................*/
/* Program chapter8_6                        */
/*                                           */
/* This program uses Gauss elimination to    */
/* determine the mesh currents for a circuit. */
/*                                           */

#include <iostream>    //Required for cin, cout
using namespace std;

// Define global constant for number of unknowns.
const int N = 3;
```