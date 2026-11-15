
The steps in the pseudocode are now detailed enough to convert into C.

```c
/*
 * Program chapter5_4
 *
 * This program computes the molecular weight of an amino
 * acid from its chemical formula.
 */
#include <stdio.h>
#include <ctype.h>
#define NEWLINE '\n'

int main(void)
{
    /* Declare variables and function prototypes. */
    int k=0, formula[20], n, current=0, done=0, d1, d2;
    double error=0, weight, total=0;
    double atomic_wt(int atom);

    /* Read chemical formula from keyboard. */
    printf("Enter chemical formula for amino acid: \n");
    while ((formula[k]=getchar()) != NEWLINE)
        k++;
    n = k;

    /* Identify individual elements and add weights. */
    while (current < (n-1) && done==0)
    {
        if (isalpha(formula[current]))
        {
            formula[current] = toupper(formula[current]);
            weight = atomic_wt(formula[current]);
            if (weight == 0)
                done = 1;
            else
            {
                if (current < n-1)
                    d1 = isdigit(formula[current+1]);
                else
                    d1 = 0;
                if (d1 && current<(n-2))
                    d2 = isdigit(formula[current+2]);
                else
                    d2 = 0;
                if (d1 && d2)
                {
                    weight *= ((formula[current+1]-'0')*10 +
                    (formula[current+2]-'0'));
                    current += 3;
                }
                else
                {
                    if (d1)
                    {
                        weight *= (formula[current+1]-'0');
                        current += 2;
                    }
                    else
                        current++;
                }
                total += weight;
            }
        }
        else
            done = 1;
    }
    /* Print formula and weight. */
    printf("Formula: ");
    for (k=0; k<=n; k++)
        putchar(formula[k]);
    printf("\n");
    if (done == 0)
        printf("Molecular Weight: %f \n",total);
    else
        printf("Error in formula. \n");
    /* Exit program. */
    return 0;
}
/*--------------------------------------------------*/
/*
 * This function returns the molecular weight of an element
 * in an amino acid.
 */
double atomic_wt(int atom)
{
    /* Declare and initialize variables. */
    int k=0, element[5]={'H', 'C', 'N', 'O', 'S'};
    double m_wt[5]={1.00794, 12.011, 14.00674,
    15.9994, 32.066}, weight;
    /* Search for element. */
    while (k<5 && element[k]!=atom)
        k++;
    /* Return corresponding atomic weight. */
    if (k < 5)
        weight = m_wt[k];
    else
        weight = 0;
    return weight;
}
/*--------------------------------------------------*/
```

## 5. TESTING

Using the data from the hand example, the output from the program is as follows:

```
Enter chemical formula for amino acid:
O2C3NH7
Molecular Weight: 89.094116
```

## MODIFY!

These problems relate to the program developed in this section for computing the molecular weight of an amino acid.

- 1. Test the program using an amino acid that has more than nine atoms of one of the elements.
- 2. Allow the user to compute the molecular weights for several amino acids. The program should stop when a period is entered. (Be sure to tell the user to enter a period when done.)

## 5.4 Statistical Measurements

Analyzing data collected from engineering experiments is an important part of evaluating the experiments. This analysis ranges from simple computations on the data, such as calculating the average value, to more complicated analyses. Many of the computations or measurements using data are statistical measurements because they have statistical properties that change from one set of data to another. For example, the sine of 60° is an exact value that is the same value every time we compute it, but the number of miles to the gallon that we get with our car is a statistical measurement, because it varies depending on parameters such as the temperature, the speed that we travel, the type of road, and whether we are in the mountains or the desert.

### Simple Analysis

When evaluating a set of experimental data, we often compute the maximum value, minimum value, mean or average value, and the median. In this section, we develop functions that can be used to compute these values using an array as input. These functions (stored in a file stat_lib.c) will be useful in many of the programs that we develop later in the text and in solutions to problems at the end of the chapters. However, it is important to note that these functions assume that there is at least one value in the array.

Maximum and Minimum. A function for determining the maximum value in an array was presented in the previous section; a similar function can be written to determine the minimum value. Both functions assume that the array contains double values; simple changes could be used to convert these functions to specify integer values.

Average. The Greek symbol $\mu$ (mu) is used to represent the average or mean value. An equation, which uses summation notation, is as follows:

\(\mu = \frac{\sum_{k=0}^{n-1} x_k}{n}, \quad (5.1)\)

where \(\sum_{k=0}^{n-1} x_k = x_0 + x_1 + x_2 + \cdots + x_{n-1}\).

The average of a set of values is always a floating-point value, even if all the data values are integers. To compute the mean value of a double array of n values, we will use the following function:

```c
/*-----------------------------------------------------*/
/* This function returns the average or mean value of   */
/* array x with n elements.                            */
/*-----------------------------------------------------*/
double mean(double x[], int npts)
{
    /* Declare and initialize variables. */
    int k;
    double sum=0;

    /* Determine mean value. */
    for (k=0; k<npts-1; k++)
        sum += x[k];

    /* Return mean value. */
    return sum/npts;
}
/*-----------------------------------------------------*/
```

Note that the variable sum was initialized to zero in the declaration statement. It could also have been initialized to zero with an assignment statement. In either case, the value of sum is initialized to zero when the function is referenced.

Median. The median is the value in the middle of a group of values, assuming that the values are sorted. If there is an odd number of values, the median is the value in the middle; if there is an even number of values, the median is the average of the values in the two middle positions. For example, the median of the values {1.6, 18, 39, 86} is the middle value, or 18; the median of the values {1.6, 18, 39, 86, 91} is the average of the two middle values, or (18 + 39)/2, or 28.5. Assume that a group of sorted values are stored in an array and that n contains the number of values in the array. If n is odd, then the subscript of the middle value can be represented by floor(n/2), as in floor(5/2), which is 2. If n is even, then the subscripts of the two middle values can be represented by floor(n/2)-1 and floor(n/2), as in floor(6/2)-1 and floor(6/2), which are 2 and 3, respectively.

The following function determines the median of a set of values stored in an array. We assume that the values are sorted (into either ascending or descending order). If the array is not sorted, a function developed later in this chapter can be referenced from the median function to sort the values.

```c
/*---------------------------------------------------------------*/
/* This function returns the median value in the sorted        */
/* array x with npts elements.                                 */
/*---------------------------------------------------------------*/
double median(double x[], int npts)
{
    /* Declare variables.    */
    int k;
    double median_x;

    /* Determine median value.    */
    k = floor(npts/2);
    if (npts % 2 != 0)
        median_x = x[k];
    else
        median_x = (x[k-1] + x[k])/2;
    /* Return median value.    */
    return median_x;
}
/*---------------------------------------------------------------*/
```

Go through this function by hand using the two sets of data values given in this discussion.

### Variance and Standard Deviation

Variance
Standard deviation

One of the most important statistical measurements for a set of data is the variance. Before we give the mathematical definition for variance, we should develop an intuitive understanding. Consider the values of arrays data1 and data2, which are plotted in Figure 5.1. If we attempted to draw a horizontal line through the middle of the values in each plot, this line would be at approximately 3.0. Thus, both arrays have approximately the same average or mean value of 3.0. However, the data in the two arrays clearly have some distinguishing characteristics. The values in data2 vary more from the mean, or deviate more from the mean value. The variance of a set of values is defined as the average squared deviation from the mean; the standard deviation is defined as the square root of the variance. Thus, the variance and the standard deviation of the values in data2 are greater than the variance and standard deviation for the values in data1. Intuitively, the larger the variance (or the standard deviation), the further the values fluctuate around the mean value.

Mathematically, the variance is represented by \(\sigma^2\), where \(\sigma\) is the Greek symbol sigma. The variance for a set of data values (which we assume are stored in an array x) can be computed using the following equation:

![](img/02c4582f051c5b51776411c92b079035_255_0.png)

This equation is a bit intimidating at first, but if you look at it closely, it becomes much simpler. The term \(x_k - \mu\) is the difference between \(x_k\) and the mean, or the deviation of \(x_k\) from
