```
```c
}

//-----------------------------------------------------------------------------
void Index2(double x[], double y[], int ind[], int n)
//-----------------------------------------------------------------------------
// Ascending indexing of correlated arrays x[1..n] and y[1..n] in ind[] by
// insertion sort using x[] as primary key and y[] as secondary key
//-----------------------------------------------------------------------------
{
    double xpiv, ypiv;
    int i, ipiv;

    for (i=1; i<=n; i++) ind[i] = i;             // initialize index array

    for (ipiv=2; ipiv<=n; ipiv++) {              // loop over pivots
        xpiv = x[ipiv]; ypiv = y[ipiv];
        i = ipiv - 1;                            // initialize sublist counter
        while ((i > 0) &&                       // scan to the left of pivot
               (x[ind[i]] > xpiv || (x[ind[i]] == xpiv && y[ind[i]] > ypiv))) {
            ind[i+1] = ind[i];                  // item > pivot: shift to the right
            i--;
        }
        ind[i+1] = ipiv;                         // insert pivot into last freed location
    }
}

#endif
```
```

# 4.7 Problems

The Python and C/C++ programs for the following problems may import the functions developed in this chapter from the modules `sort.py` and `sort.h`, respectively, which are available as supplementary material. For creating runtime plots, the graphical routines contained in the libraries `graphlib.py` and `graphlib.h` may be employed.

# PROBLEM 4.1

The four quartiles divide a ranked data set into four groups, composed of equal number of values (25% of the values, each). For example, for a set of length *n*, the second quartile includes the values ranked between ⌊*n*/4⌋ + 1 and ⌊*n*/2⌋ (the square brackets designate the integer part), or, in other words, having in the sorted sequence indexes between ⌊*n*/4⌋ + 1 and ⌊*n*/2⌋.

Generate index and rank tables for the ascending ordering of a sequence of *n* = 12 random numbers using the routines Index and Rank. Group the values by quartile and list them along with their index and rank.

# Solution

The implementations are given in Listings 4.12 and 4.13, and a typical output is shown in Listing 4.14.

# Listing 4.12  Sorting the Elements of an Array into Quartiles (Python Coding)

```
```python
# Sorting the elements of an array into quartiles
from sort import *
from random import *

# main
```
```