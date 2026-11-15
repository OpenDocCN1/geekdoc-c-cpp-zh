# MODIFY!

Modify program chapter6_8 such that it determines the number of thousands of contiguous values that can be stored for the data types indicated in the following:

+   1. long integers, 2. doubles, and 3. long doubles.

In the previous section, we developed a program that read a set of seismic data from a data file and determined possible seismic event locations within the data. The program used a symbolic constant MAX_SIZE to allocate an array to store the data. If the number of points in the data file exceeded MAX_SIZE, then the program terminated with an error message. In the following, we present statements that use dynamic memory allocation so that the maximum array size does not have to be allocated when the program is compiled (instead, the array memory is dynamically allocated based on the size of the seismic data file):

```
/*
 * Program chapter6_5mod
 *
 * This program reads a seismic data file and then
 * determines the times of possible seismic events.
 * Dynamic memory allocation is used.
 */
#include <stdio.h>
#define FILENAME "seismic1.txt"
#define THRESHOLD 1.5

int main(void)
{
    /* Declare variables and function prototypes. */
    int k, npts, short_window, long_window;
    double sensor, time_incr, short_power,
           long_power, ratio;

    FILE *file_ptr;
    double power_w(double *ptr,int n);

    /* Read data header and allocate memory. */
    file_ptr = fopen(FILENAME,"r");
    if (file_ptr == NULL)
        printf("Error opening input file. \n");
    else
    {
        fscanf(file_ptr,"%d %lf",&npts,&time_incr);
        sensor = (double *)malloc(npts*sizeof(double));
        if (sensor == NULL)
            printf("Not enough memory available. \n");
        else
            (no changes in the remainder of program chapter6_5 on page 312)
}
```