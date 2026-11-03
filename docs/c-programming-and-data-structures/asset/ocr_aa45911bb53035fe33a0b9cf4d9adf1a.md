# 2. Calculation of Standard Deviation

In statistics, standard deviation is used to measure deviation of data from its mean. The formula for calculating standard deviation of n items is

s = √variance

where

variance = 1/n Σᵢ₌₁ⁿ (xᵢ − m)²

and

m = mean = 1/n Σᵢ₌₁ⁿ xᵢ

The algorithm for calculating the standard deviation is as follows:

+   1. Read n items.
+   2. Calculate sum and mean of the items.
+   3. Calculate variance.
+   4. Calculate standard deviation.

Complete program with sample output is shown in Fig. 3.12.

```
Program
#include <math.h>
#define MAXSIZE 100
main()
{
    int i,n;
    float value [MAXSIZE], deviation,
    sum,sumsqr,mean,variance,stdcdeviation;
    sum = sumsqr = n = 0 ;
    printf("Input values: input -1 to end \n");
    for (i=1; i<= MAXSIZE ; i++)
    {
        scanf("%f",&value[i]);
        if (value[i] == -1)
            break;
        sum += value[i];
        n += 1;
    }
    mean = sum/(float)n;
    for (i = 1; i<= n; i++)
    {
        deviation = value[i] - mean;
        sumsqr += deviation * deviation;
    }
    variance = sumsqr/(float)n ;
    stddeviation = sqrt(variance) ;
    printf("\nNumber of items : %d\n",n);
    printf("Mean : %f\n", mean);
    printf("Standard deviation : %f\n", stddeviation);
}
```