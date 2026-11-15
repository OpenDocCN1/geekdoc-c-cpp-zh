```
```cpp
double variance(double x[],int npts)
{
	/* Declare variables and function prototypes. */
	int k;
	double sum=0, mu;
	double mean(double x[],int npts);

	/* Determine variance. */
	mu = mean(x,npts);
	for (k=0; k<n-1; k++)
		sum += (x[k] - mu)*(x[k] - mu);

	/* Return variance */
	return sum/(npts-1);
}
```
```

```
```cpp
/*----------------------------------------------*/
/* This function returns the standard deviation of an array x */
/* with npts elements.                        */
/*----------------------------------------------*/
double std_dev(double x[],int npts)
{
	/* Declare function prototypes. */
	double variance(double x[],int npts);

	/* Return standard deviation */
	return sqrt(variance(x,npts));
}
/*----------------------------------------------*/
```
```

# Custom Header File

The functions developed in this section are frequently used in solving engineering problems. To facilitate their use, we generate a custom header file that contains the prototype statements for these functions. Then, instead of including all the prototype statements in a main function, we can use a preprocessor directive that includes the custom header file.

The custom header file named stat_lib.h contains the following function prototype statements:

```
```cpp
double max(double x[],int n);
double min(double x[],int n);
double mean(double x[],int n);
double median(double x[],int n);
double variance(double x[],int n);
double std_dev(double x[],int n);
```
```

The statement that includes these function prototype statements in a main function is

```
```cpp
#include "stat_lib.h"
```
```

The use of this custom header is illustrated in the next section.

In addition to accessing the custom header file with the include statement, a program must also have access to the file stat_lib.c, which contains the statistical functions. The