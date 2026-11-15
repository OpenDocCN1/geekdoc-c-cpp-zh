| 0.4 | 163.2 |
| 0.5 | 158.2 |
| 0.6 | 169.3 |
| 0.7 | 148.2 |
| 0.8 | 137.6 |
| 0.9 | 135.9 |

The process of first reading the number of data points and then using that to specify the number of times to read data and accumulate information is easily described using a variable-controlled loop. In the following pseudocode and program, the first actual data value is used to initialize the min and max values. If we set the min value initially to zero and all the sensor values are greater than zero, the program will print the erroneous value of zero for the minimum sensor reading.

The pseudocode and program for this solution are as follows:

# Refinement in Pseudocode

```
main: set sum to zero
    if file cannot be opened
        print error message
    else
        read number of data points
        set k to 1
        while k <= number of data points
            read time, motion
            if k = 1
                set max to motion
                set min to motion
            add motion to sum
            if motion > max
                set max to motion
            if motion < min
                set min to motion
            increment k by 1
        set average to sum/number of data points
        print average, max, min
```

```
/**
 * Program chapter3_6
 *
 * This program generates a summary report from
 * a data file that has the number of data points
 * in the first record.
 */
#include <stdio.h>
#define FILENAME "sensor1.txt"
```