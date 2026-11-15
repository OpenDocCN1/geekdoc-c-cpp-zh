
## 7.3 Statistical Measurements

Analyzing data collected from engineering experiments is an important part of evaluating the experiments. This analysis ranges from simple computations on the data, such as calculating the average value, to more complicated analysis. Many of the computations or measurements using data are **statistical measurements** because they have statistical properties that change from one set of data to another. For example, the sine of 60 degrees is an exact value that is the same value every time we compute it, but the number of miles to the gallon that we get with our car is a statistical measurement because it varies somewhat, depending on parameters such as the temperature, the speed that we travel, the type of road, and whether we are in the mountains or the desert.

### Simple Analysis

When evaluating a set of experimental data, we often compute the maximum value, minimum value, **mean** or average value, and the **median**. In this section, we develop functions that can be used to compute these values using an array as input. These functions (stored in a file `stat_lib.cpp`) will be useful in many of the programs that we develop later in the text and in solutions to problems at the end of the chapters. It is important to note that the functions assume that there is at least one value in the array. The functions also assume that the array contains `double` values.

### Maximum, Minimum.

A function for determining the maximum value in an array was presented in the previous section; a similar function for determining the minimum value is presented here:

```cpp
/*------------------------------------------------------------*/
/*  This function returns the minimum                         */
/*                                                            */
/*  value in an array x with n elements.                      */
/*------------------------------------------------------------*/
double minval(const double x[], int n)
{
   // Declare objects.
   double min_x;

   // Determine minimum value in the array.
   min_x = x[0];
   for (int k=1; k<n; ++k)
   {
      if (x[k] < min_x)
         min_x = x[k];
   }

   // Return minimum value.
   return min_x;
}
/*------------------------------------------------------------*/
```

### Average.

The Greek symbol \(\mu\) is used to represent the average, or mean, value, as shown in the following equation, which uses summation notation:

\(\mu = \frac{\sum_{k=0}^{n-1} x_k}{n}\)

where

\(\sum_{k=0}^{n-1} x_k = x_0 + x_1 + x_2 + \cdots + x_{n-1}.\)

This function computes the mean value of a double array of \(n\) values:

```cpp
/*-------------------------------------------------------------*/
/* This function returns the average or                        */
/* mean value of an array with n elements.                     */
/*-------------------------------------------------------------*/
double mean(const double x[], int n)
{
   // Declare and initialize objects.
   double sum(0);

   // Determine mean value.
   for (int k=0; k<n; ++k)
   {
      sum += x[k];
   }

   // Return mean value.
   return sum/n;
}
/*-------------------------------------------------------------*/
```

Note that the object sum was initialized to zero in the declaration statement. It could also have been initialized to zero with an assignment statement. In either case, the value of sum is initialized to zero when the function is referenced.

### Median.

The median is the value in the middle of a group of values, assuming that the values are sorted. If there is an odd number of values, the median is the value in the middle; if there is an even number of values, the median is the average of the values in the two middle positions. For example, the median of the values 1, 6, 18, 39, 86 is the middle value, or 18; the median of the values 1, 6, 18, 39, 86, 91 is the average of the two middle values, or (18+39)/2, or 28.5. Assume that a group of sorted values is stored in an array, and that n contains the number of values in the array. If n is odd, then the offset of the middle value can be represented by floor(n/2), as in floor(5/2), which is 2. If n is even, then the offsets of the two middle values can be represented by floor(n/2) - 1 and floor(n/2), as in floor(6/2) - 1 and floor(6/2), which are 2 and 3. The next function determines the median of a set of values stored in an array. We assume that the values are sorted (into either ascending or descending order). If the array is not sorted, a function developed later in this chapter can be referenced from the median function to sort the values.

```cpp
/*------------------------------------------------------------*/
/*  This function returns the median                          */
/*  value in an array x with n elements                       */
/*  The values in x are assumed to be ordered.                */
/*------------------------------------------------------------*/
double median(const double x[], int n)
{
   // Declare objects.
   double median_x;
   int k;

   // Determine median value.
   k = floor(n/2);
   if (n%2 == 0)
      median_x = x[k];
   else
      median_x = (x[k-1] + x[k])/2;

   // Return median value.
   return median_x;
}
/*------------------------------------------------------------*/
```

Go through this function by hand, using the two sets of data values given in this discussion.

### Variance and Standard Deviation

One of the most important statistical measurements for a set of data is the variance. Before we give the mathematical definition for variance, it is useful to develop an intuitive understanding. Consider the values of arrays data1 and data2 that are plotted in Figure 7.4. If we attempted to draw a horizontal line through the middle of the values in each plot, this line would be at approximately 3.0.

variance
standard deviation

Thus, both arrays have approximately the same average, or mean, value of 3.0. However, the data in the two arrays clearly have some distinguishing characteristics. The values in data2 vary more from the mean, or deviate more from the mean value. The variance of a set of values is defined to be the average squared deviation from the mean; the standard deviation is defined to be the square root of the variance. Thus, the variance and the standard deviation of the values in data2 are greater than the variance and standard deviation for the values in data1. Intuitively, the larger the variance (or the standard deviation), the further the values fluctuate around the mean value.

Mathematically, the variance is represented by \(\sigma^2\), where \(\sigma\) is the Greek symbol sigma. The variance for a set of data values (which we assume are stored in an array x) can be computed using the following equation:

\(\sigma^2 = \frac{\sum_{k=0}^{n-1}(x_k - \mu)^2}{n-1}.\) (7.1)

This equation is a bit intimidating at first, but if you look at it closely, it becomes much simpler. The term \(x_k - \mu\) is the difference between \(x_k\) and the mean, or the deviation of \(x_k\)

![](img/0235a4ea835dc4575bd036e024a533b3_386_0.png)

![](img/0235a4ea835dc4575bd036e024a533b3_386_1.png)

Figure 7.4 Random sequence.

from the mean. This value is squared so that we always have a positive value. We then add the squared deviations for all data points. This sum is then divided by $n - 1$, which approximates an average. The definition of variance has two forms: The denominator of a sample variance is $n - 1$, and the denominator of a population variance is $n$. Most engineering applications use the sample variance, as shown in Equation (7.1). Thus, Equation (7.1) computes the average squared deviation of the data from the mean. The standard deviation is defined to be the square root of the variance:

\(\sigma = \sqrt{\sigma^2}\).

Both the variance and the standard deviation are commonly used in analyzing engineering data, so we give the functions for computing both values. Note that the function for computing the standard deviation references the variance function and that the variance function references the mean function; thus, these functions must include the proper function prototype statements. Also, note that there must be at least two values in the array, or the variance function will attempt to perform a division by zero.

```cpp
/*
 * This function returns the variance
 * of an array with n elements.
 */
```
