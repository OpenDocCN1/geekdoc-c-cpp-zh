
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

## 4.7 Problems

The Python and C/C++ programs for the following problems may import the functions developed in this chapter from the modules `sort.py` and `sort.h`, respectively, which are available as supplementary material. For creating runtime plots, the graphical routines contained in the libraries `graphlib.py` and `graphlib.h` may be employed.

## PROBLEM 4.1

The four quartiles divide a ranked data set into four groups, composed of equal number of values (25% of the values, each). For example, for a set of length *n*, the second quartile includes the values ranked between ⌊*n*/4⌋ + 1 and ⌊*n*/2⌋ (the square brackets designate the integer part), or, in other words, having in the sorted sequence indexes between ⌊*n*/4⌋ + 1 and ⌊*n*/2⌋.

Generate index and rank tables for the ascending ordering of a sequence of *n* = 12 random numbers using the routines Index and Rank. Group the values by quartile and list them along with their index and rank.

# Solution

The implementations are given in Listings 4.12 and 4.13, and a typical output is shown in Listing 4.14.

## Listing 4.12 Sorting the Elements of an Array into Quartiles (Python Coding)

```python
# Sorting the elements of an array into quartiles
from sort import *
from random import *

# main
```

```
n = 12                                          # number of values to be sorted
x = [0]*(n+1)                                   # array to be sorted
ind = [0]*(n+1); rnk = [0]*(n+1)                # arrays of indexes and ranks

print("Original array:")
for i in range(1,n+1):
    x[i] = random()                             # random sub-unitary values
    print("{0:6.2f}".format(x[i]),end="")
print("\n")

Index(x,ind,n)                                  # create array of indexes
Rank(ind,rnk,n)                                 # create array of ranks

print("Quartile 1")
print("      i     ind     rnk         x")
for i in range(1,int(n/4)+1):
    indi = ind[i]
    print("{0:6d}{1:6d}{2:6d}{3:10.2f}".format(i,ind[i],rnk[indi],x[indi]))

print("Quartile 2")
print("      i     ind     rnk         x")
for i in range(int(n/4)+1,int(n/2)+1):
    indi = ind[i]
    print("{0:6d}{1:6d}{2:6d}{3:10.2f}".format(i,ind[i],rnk[indi],x[indi]))

print("Quartile 3")
print("      i     ind     rnk         x")
for i in range(int(n/2)+1,int(3*n/4)+1):
    indi = ind[i]
    print("{0:6d}{1:6d}{2:6d}{3:10.2f}".format(i,ind[i],rnk[indi],x[indi]))

print("Quartile 4")
print("      i     ind     rnk         x")
for i in range(int(3*n/4)+1,n+1):
    indi = ind[i]
    print("{0:6d}{1:6d}{2:6d}{3:10.2f}".format(i,ind[i],rnk[indi],x[indi]))
```

## Listing 4.13 Sorting the Elements of a Sequence into Quartiles (C/C++ Coding)

```
// Sorting the elements of an array into quartiles
#include <stdio.h>
#include <stdlib.h>
#include "sort.h"

int main()
{
    const int n = 12;                           // number of values to be sorted
    double x[n+1];                              // array to be sorted
    int ind[n+1], rnk[n+1];                     // arrays of indexes and ranks
    int i, indi;

    printf("Original array:\n");
    for (i=1; i<=n; i++) {
        x[i] = rand()/(RAND_MAX+1e0);           // random sub-unitary values
        printf("%6.2f",x[i]);
    }
    printf("\n");
```

```
Index(x,ind,n);                     // create array of indexes
Rank(ind,rnk,n);                     // create array of ranks

printf("Quartile 1\n");
printf("   i    ind    rnk        x\n");
for (i=1; i<=int(n/4); i++) {
    indi = ind[i];
    printf("%6i%6i%6i%10.2f\n",i,ind[i],rnk[indi],x[indi]);
}

printf("Quartile 2\n");
printf("   i    ind    rnk        x\n");
for (i=int(n/4)+1; i<=int(n/2); i++) {
    indi = ind[i];
    printf("%6i%6i%6i%10.2f\n",i,ind[i],rnk[indi],x[indi]);
}

printf("Quartile 3\n");
printf("   i    ind    rnk        x\n");
for (i=int(n/2)+1; i<=int(3*n/4); i++) {
    indi = ind[i];
    printf("%6i%6i%6i%10.2f\n",i,ind[i],rnk[indi],x[indi]);
}

printf("Quartile 4\n");
printf("   i    ind    rnk        x\n");
for (i=int(3*n/4)+1; i<=n; i++) {
    indi = ind[i];
    printf("%6i%6i%6i%10.2f\n",i,ind[i],rnk[indi],x[indi]);
}
}
```

## Listing 4.14 Typical Output of the Sorting Programs 4.12 and 4.13

```
Original array:
  0.00  0.56  0.19  0.81  0.58  0.48  0.35  0.90  0.82  0.75  0.17  0.86
Quartile 1
   i    ind    rnk        x
   1     1     1     0.00
   2    11     2     0.17
   3     3     3     0.19
Quartile 2
   i    ind    rnk        x
   4     7     4     0.35
   5     6     5     0.48
   6     2     6     0.56
Quartile 3
   i    ind    rnk        x
   7     5     7     0.58
   8    10     8     0.75
   9     4     9     0.81
Quartile 4
   i    ind    rnk        x
  10     9    10     0.82
  11    12    11     0.86
  12     8    12     0.90
```

## PROBLEM 4.2

Generate the index table for a sequence of n = 50 random numbers using the routine Index, and also sort the sequence using routine InsertSort. Plot the original sequence, along with the sorted sequence and the one ordered by means of the index table, as functions of the component index, using routine Plot from the library graphlib. Check visually, by the monotonous increase of the values, that the sequences are actually sorted.

# Solution

The implementations are shown in Listings 4.15 and 4.16, and the original/sorted sequences are plotted in Figure 4.2.

## Listing 4.15 Sorting and Indexing of a Random Sequence Using Direct Insertion (Python Coding)

```
# Ascending sort of an array
from random import *
from sort import *
from graphlib import *

# main

n = 50;                                   # number of values to be sorted
x = [0]*(n+1); x0 = [0]*(n+1)             # array to be sorted and copy
ix = [0]*(n+1)                           # array of sequential indexes
ind = [0]*(n+1)                           # array of indexes

for i in range(1,n+1):
    x[i] = x0[i] = random()               # array to be sorted
    ix[i] = float(i)

GraphInit(1200,600)

Plot(ix,x,n,"blue",3,0.06,0.32,0.25,0.80,"i","x","Initial array")

InsertSort(x,n)

Plot(ix,x,n,"blue",3,0.39,0.65,0.25,0.80,"i","x","Sorted array")

Index(x0,ind,n)
for i in range(1,n+1): x[i] = x0[ind[i]]  # sort by indexing

Plot(ix,x,n,"blue",3,0.72,0.98,0.25,0.80,"i","x","Indexed array")

MainLoop()
```

## Listing 4.16 Sorting and Indexing of a Random Sequence Using Direct Insertion (C/C++ Coding)

```
// Ascending sort of an array
#include "memalloc.h"
#include "sort.h"
#include "graphlib.h"

int main(int argc, wchar_t** argv)
{
    double *ix, *x, *x0;
    int *ind;
    int i, n;

n = 50;
 x = Vector(1,n); x0 = Vector(1,n);          // number of values to be sorted
 ix = Vector(1,n);                           // array to be sorted and copy
 ind = IVector(1,n);                         // array of sequential indexes
                                          // array of indexes
 for (i=1; i<=n; i++) {
     x[i] = x0[i] = rand();                  // array to be sorted
     ix[i] = double(i);
 }
 PyGraph c(argc, argv);
 c.GraphInit(1200,600);
 c.Plot(ix,x,n,"blue",3,0.06,0.32,0.25,0.80,"i","x","Initial array");
 InsertSort(x,n);
 c.Plot(ix,x,n,"blue",3,0.39,0.65,0.25,0.80,"i","x","Sorted array");
 Index(x0,ind,n);                           // sort by indexing
 for (i=1; i<=n; i++) x[i] = x0[ind[i]];
 c.Plot(ix,x,n,"blue",3,0.72,0.98,0.25,0.80,"i","x","Indexed array");
 c.MainLoop();
 }
```

## PROBLEM 4.3

Generate sequences of n = 100–10,000 random numbers and sort them using comparatively bubble sort, insert sort, and Quicksort.

- a. Modify the sorting functions BubbleSort, InsertSort, and QuickSort developed in the main text, in such a way as to separately return the total number of performed comparisons and save operations, respectively, and print these to a file.
- b. Add plotting capabilities to the implementations by using the routine MultiPlot from the library graphlib and plot the dependences for the three sorting methods on the same graph.
- c. Assess qualitatively the performance of the sorting algorithms for small and extensive sequences, respectively.

# Solution

The Python sorting routines, modified so as to return the operation counts, are given in Listing 4.17. The global variables ncomp and nsave are used to retrieve, respectively, the total number of comparisons and save operations from the sorting routines into the calling program.

## Listing 4.17 Python Sorting Routines Modified to Return Operation Counts (Python Coding)

```
#===============================================================================
def BubbleSort(x, n):
#-------------------------------------------------------------------------------
# Ascending sort of array x[1..n] by modified bubble sort
#-------------------------------------------------------------------------------
    global ncomp, nsave                     # no. of compares and saves
    ipass = 0                               # initialize pass counter
    swap = 1                                # initialize swap flag to enter loop
    while (swap):                           # perform passes while swaps occur
```
