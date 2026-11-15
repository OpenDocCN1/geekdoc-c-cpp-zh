Average. The Greek symbol \(\mu\) is used to represent the average, or mean, value, as shown in the following equation, which uses summation notation:

\(\mu = \frac{\sum_{k=0}^{n-1} x_k}{n}\)

where

\(\sum_{k=0}^{n-1} x_k = x_0 + x_1 + x_2 + \cdots + x_{n-1}.\)

This function computes the mean value of a double array of \(n\) values:

```
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

Median. The median is the value in the middle of a group of values, assuming that the values are sorted. If there is an odd number of values, the median is the value in the middle; if there is an even number of values, the median is the average of the values in the two middle positions. For example, the median of the values 1, 6, 18, 39, 86 is the middle value, or 18; the median of the values 1, 6, 18, 39, 86, 91 is the average of the two middle values, or (18+39)/2, or 28.5. Assume that a group of sorted values is stored in an array, and that n contains the number of values in the array. If n is odd, then the offset of the middle value can be represented by floor(n/2), as in floor(5/2), which is 2. If n is even, then the offsets of the two middle values can be represented by floor(n/2) - 1 and floor (n/2), as in floor (6/2) - 1 and floor (6/2), which are 2 and 3. The next function determines the median of a set of values stored in an array. We assume that the values are sorted (into either ascending or descending order). If the array is not sorted, a function developed later in this chapter can be referenced from the median function to sort the values.