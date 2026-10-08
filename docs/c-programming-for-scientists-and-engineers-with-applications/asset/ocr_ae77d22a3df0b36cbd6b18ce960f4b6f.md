# 510 Multidimensional Arrays

```
Find the maximum and the minimum in the row and their locations
End for
For each row
Check the row maximum to see whether it is also a column minimum
If so, print the position
Check the row minimum to see whether it is also a column maximum.
If so, print the position
End
```

Stop

# Program

```
********************************************************************
/*
* Locate the Saddle Point in an Array                  *
*/********************************************************************
/*
* Input Variables:                                     *
* elevation[IMAX] [JMAX]- values of elevation         *
* Computed Variables:                                 *
* rowmax -- maximum elevation in row                  *
* rowmin -- minimum elevation in row                  *
* colmax -- maximum elevation in column               *
* colmin -- minimum elevation in column               *
* jmax[IMAX] -- location of rowmax                     *
* jmin[IMAX] -- location of rowmin                     *
* icmax[IMAX] -- location of colmax                    *
* icmin[JMAX] -- location of colmin                   *
********************************************************************
#include<stdio.h>
#define IMAX 5
#define FILE 4
#define *inptr;

FILE
int main()
nfloat elevation[IMAX] [JMAX];
float rowmax, rowmin, colmax, colmin;
int jmax[IMAX], jmin[IMAX], icmax[JMAX],icmin[JMAX];
```