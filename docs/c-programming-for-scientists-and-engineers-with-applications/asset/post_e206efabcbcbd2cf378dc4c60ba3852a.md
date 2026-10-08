
# Pointers and Dynamic Storage

Allocate storage for the table.

Calculate the stress from the formula

$\sigma = p/area$;

Where $\sigma$ is the stress in pounds per square inch,
$p$ is the load in pounds, andarea is the cross-sectional area of the bar subject to tensile load.

Output the load and the stress.

# Pseudocode

```
input the cross sectional dimensions width w and thickness t
area = w* t
input load minimum and maximum increment
table size = (loadmax - loadmin) / increment + 1
for minimum to load maximum at requested
stress = load / area
end
print the table
stop
```

# Program

```
/******************************************************/
/* main: Computes the Stress in Rectangular Cross */
/* Section Steel Bar using Array Pointer */
/*
/******************************************************/
/* Defined Constants: */
/* --none-- */
/*
/* Input Variables: */
/* width -- cross sectional width of steel bar */
/* thick -- cross sectional thickness of steel bar */
/* minload -- minimum load applied */
/* maxload -- maximum load applied */
/* inc -- load increments */
```

```
/*
* Computed Variables:
* area - cross sectional area
* stress - stress in the column
*/
/*
* Output Variables:
* load - load on the column
* stress - tensile stress in pounds
* per square inch
************************************************

#include <stdio.h>

int main() {
    int i, n;
    float width, thick, area, minload, maxload, inc, stress;
    float *loadptr, *stressptr;
    scanf("%f %f", &width, &thick);
    scanf("%f %f", &minload, &maxload, &inc);
    area = width * thick;
    n = (maxload - minload)/ inc + 1;
    loadptr = (float *) calloc(n, sizeof(float));
    stressptr = (float *) calloc(n, sizeof(float));
    for(i = 0; i < n; i++) {
        *loadptr = minload + i * inc;
        *stressptr = *loadptr / area;
        loadptr++;
        stressptr++;
    }

    loadptr -= n;
    stressptr -= n;

    for(i = 0; i < n; i++) {
        printf("%8.2f      %8.2f\n", *loadptr, *stressptr);
        loadptr++;
        stressptr++;
    }
    return 0;
}
```

# Pointers and Dynamic Storage

# Input

3 4
1000 10000 1000

# Output

1000.00 83.33
2000.00 166.67
3000.00 250.00
4000.00 333.33
5000.00 416.67
6000.00 500.00
7000.00 583.33
8000.00 666.67
9000.00 750.00
10000.00 833.33

# 10.6.2 Days of Above Average Temperature

This program uses an array pointer to manipulate a one-dimensional array.

# Problem

- Input the name of the month and display average temperatures for the
month. Determine the number of days that the average temperature was
above the monthly average.

# Data

The name of the month.

# Method

- Input month name.
- Look the month up in a table to find out how many days it has (ignore
leap year).
- Allocate space for the daily average temperatures.
- Input average temperatures.
- Compute the monthly average.
- Print the monthly average.
- Print the number of days above average.

# Pseudocode

```
input month name
locate month name in an array of month names and get the number of days
allocate array storage
for each day
    input average temperature and store in an array
    add average temperature to sum
end
naverage = sum / ndays
output average
```

```
for each day
    compare the average temp to average
    counting those that are above average
end
output count
stop
```

> Program
/********************************************************************/
/*  main: Compute the Sum and Average Temperatures                  */
/*    Using Array Pointer                                     */
/* *********************************************************************/\
/*  Defined Constants:                                            */
/*    --none--                                                  */
/*  Input Variables:                                              */
/*    month[] - name of month                               */
/*    dacnt - number of numbers of type float               */
/*  Computed Variables:                                            */
/*    sum - sum of numbers                                     */
/*    average - average of numbers                             */
/*    ndays - number of days in month                        */
/* */

```
/*
 * Output Variables:
 */
 * count - number of above average days
 */
 * sum - sum of the numbers
 */
 * average - average of numbers
 */
/*
 * function called:
 * funcmonth - return number of days in the month
 */
 ************************************************************************************

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int funcmonth(char []);

int main()
{
    int i, ndays, count;
    char month[10];
    float sum, average;
    float *avgtemp;

    scanf("%s", month);

    ndays = funcmonth(month);

    avgtemp = (float*)calloc(ndays, sizeof(float));

    sum = 0.0;
    for(i = 0; i < ndays; i++)
    {
        scanf("%f", avgtemp);
        sum += *avgtemp;
    }

    avgtemp = avgtemp - ndays;
    average = sum / ndays;
    printf("average temperature for %s is %.2f\n", month, average);

    count = 0;
    for(i = 0; i < ndays; i++)
    {
        if(*avgtemp > average)
            count++;
        avgtemp++;
    }

```

```
avgtemp = avgtemp - ndays;
printf("%d above average\n", count);
return 0;
```

```
/**********************************************************************************/
/* * funcmonth: Returns the Number of Days in the Month */
/**********************************************************************************/
/* Input Parameters:                               */
/*   datamoth - name of month                     */
/* Output Parameters:                               */
/*   --none--                                       */
/* Local Variables:                                */
/*   days[] - number of days in each month         */
/*   month[][] - an array with name of each month */
/*                                                  
/* Return Variables:                               */
/*   ndays - number of days in data month         */
/**********************************************************************************/
```

```
int funcmonth(char datamoth[])
{
  int days[12] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
  char month[12][10] = {"January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"};

  int k, ndays;
  for (k = 0; k < 12; k++)
    if(strcmp(month[k], datamoth) == 0)
      ndays = days[k];
  return ndays;
}
```

# Pointers and Dynamic Storage

# Input

- February
3 4
1000 10000 1000

# Output

1000.00 83.33
2000.00 166.67
3000.00 250.00
4000.00 333.33
5000.00 416.67
6000.00 500.00
7000.00 583.33
8000.00 666.67
9000.00 750.00
10000.00 833.33

# 10.6.2 Days of Above Average Temperature

This program uses an array pointer to manipulate a one-dimensional array.

# Problem

- Input the name of the month and display average temperatures for the
month. Determine the number of days that the average temperature was
above the monthly average.

# Data

The name of the month.

# Method

- Input month name.
- Look the month up in a table to find out how many days it has (ignore
leap year).
- Allocate space for the daily average temperatures.
- Input average temperatures.
- Compute the monthly average.
- Print the monthly average.
- Print the number of days above average.

# Pseudocode

```
input month name
locate month name in an array of month names and get the number of days
allocate array storage
for each day
    input average temperature and store in an array
    add average temperature to sum
end
naverage = sum / ndays
output average
```

```
for each day
    compare the average temp to average
    counting those that are above average
end
output count
stop
```

> Program
/********************************************************************/
/*  main: Compute the Sum and Average Temperatures                  */
/*    Using Array Pointer                                     */
/* *********************************************************************/\
/*  Defined Constants:                                            */
/*    --none--                                                  */
/*  Input Variables:                                              */
/*    month[] - name of month                               */
/*    dacnt - number of numbers of type float               */
/*  Computed Variables:                                            */
/*    sum - sum of numbers                                     */
/*    average - average of numbers                             */
/*    ndays - number of days in month                        */
/* */

```
/*
 * Output Variables:
 */
 * count - number of above average days
 */
 * sum - sum of the numbers
 */
 * average - average of numbers
 */
/*
 * function called:
 * funcmonth - return number of days in the month
 */
 ************************************************************************************

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int funcmonth(char []);

int main()
{
    int i, ndays, count;
    char month[10];
    float sum, average;
    float *avgtemp;

    scanf("%s", month);

    ndays = funcmonth(month);

    avgtemp = (float*)calloc(ndays, sizeof(float));

    sum = 0.0;
    for(i = 0; i < ndays; i++)
    {
        scanf("%f", avgtemp);
        sum += *avgtemp;
    }

    avgtemp = avgtemp - ndays;
    average = sum / ndays;
    printf("average temperature for %s is %.2f\n", month, average);

    count = 0;
    for(i = 0; i < ndays; i++)
    {
        if(*avgtemp > average)
            count++;
        avgtemp++;
    }

```

```
avgtemp = avgtemp - ndays;
printf("%d above average\n", count);
return 0;
```

```
/**********************************************************************************/
/* * funcmonth: Returns the Number of Days in the Month */
/**********************************************************************************/
/* Input Parameters:                               */
/*   datamoth - name of month                     */
/* Output Parameters:                               */
/*   --none--                                       */
/* Local Variables:                                */
/*   days[] - number of days in each month         */
/*   month[][] - an array with name of each month */
/*                                                  
/* Return Variables:                               */
/*   ndays - number of days in data month         */
/**********************************************************************************/
```

```
int funcmonth(char datamoth[])
{
  int days[12] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
  char month[12][10] = {"January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"};

  int k, ndays;
  for (k = 0; k < 12; k++)
    if(strcmp(month[k], datamoth) == 0)
      ndays = days[k];
  return ndays;
}
```

# Pointers and Dynamic Storage

# Input

- February
3 4
1000 10000 1000

# Output

1000.00 83.33
2000.00 166.67
3000.00 250.00
4000.00 333.33
5000.00 416.67
6000.00 500.00
7000.00 583.33
8000.00 666.67
9000.00 750.00
10000.00 833.33

# 10.6.2 Days of Above Average Temperature

This program uses an array pointer to manipulate a one-dimensional array.

# Problem

- Input the name of the month and display average temperatures for the
month. Determine the number of days that the average temperature was
above the monthly average.

# Data

The name of the month.

# Method

- Input month name.
- Look the month up in a table to find out how many days it has (ignore
leap year).
- Allocate space for the daily average temperatures.
- Input average temperatures.
- Compute the monthly average.
- Print the monthly average.
- Print the number of days above average.

# Pseudocode

```
input month name
locate month name in an array of month names and get the number of days
allocate array storage
for each day
    input average temperature and store in an array
    add average temperature to sum
end
naverage = sum / ndays
output average
```

```
for each day
    compare the average temp to average
    counting those that are above average
end
output count
stop
```

> Program
/********************************************************************/
/*  main: Compute the Sum and Average Temperatures                  */
/*    Using Array Pointer                                     */
/* *********************************************************************/\
/*  Defined Constants:                                            */
/*    --none--                                                  */
/*  Input Variables:                                              */
/*    month[] - name of month                               */
/*    dacnt - number of numbers of type float               */
/*  Computed Variables:                                            */
/*    sum - sum of numbers                                     */
/*    average - average of numbers                             */
/*    ndays - number of days in month                        */
/* */

# 10.6.3 Sorting Dynamically Stored Character Strings

Problem

Write a program to sort the strings in dynamic storage in alpha-order. Print the unsorted and sorted strings.

# Method

Use buffer for input.
Allocate dynamic storage for each string.
Store the addresses of the strings in a pointer array.
Output the unsorted strings.
Sort the strings in alphabetical order, rearranging their pointers.
Output the sorted strings.

# Data

Input 10 strings.

# Pseudocode

```
main())
  call funcinput
  call funcoutput
  call funcsort
  call funcoutput
stop
```

```
funcinput()
```

```
  input the number of strings (at most 20)
  for each string
    input string into a buffer
    allocate dynamic storage
    assign the address to a pointer array element
    copy the string from the buffer to dynamic storage
  end for
  return
```
end
```

```
funcsort()
```

```
  for each string i
    for each string j, j > i
```

```
if ( string i is greater the string j )
    swap the string pointers
end if
end for
end for
return
end
```

```
funcoutput()
```

```
  for each string
    output strings
end for
return
end
```

# Program

```
/********************************************************************/
/* Sort the Character String in Alphabetical Order */
/********************************************************************/
/* Working Variables: */
/* *strptr[NUMSTR] - character pointer array */
/* to store pointers */
/* to character strings */
/* Output Variables: */
/* *strptr[NUMSTR] - character pointer array */
/* to store dynamic pointers */
/* to character strings */
/* Functions Called: */
/* funcinput - function to input data */
/* funcsort - function to sort the strings */
/* funcoutput - function to output strings */
/* Files Used: */
/* sorting.dat - input data file */ /
```
