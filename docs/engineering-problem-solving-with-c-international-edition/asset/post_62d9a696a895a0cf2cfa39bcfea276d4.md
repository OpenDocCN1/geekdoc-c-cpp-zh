
![](img/02c4582f051c5b51776411c92b079035_256_0.png)

![](img/02c4582f051c5b51776411c92b079035_256_1.png)

Figure 5.1 Random sequences.

the mean. This value is squared so that we always have a positive value. We then add the squared deviations for all data points. This sum is then divided by n - 1, which approximates an average. The definition of variance has two forms. The denominator of a sample variance is n - 1, and the denominator of a population variance is n. Most engineering applications use the sample variance, as shown in Equation (5.2). Thus, Equation (5.2) computes the average squared deviation of the data from the mean. The standard deviation is defined to be the square root of the variance:

```
\sigma = \sqrt{\sigma^2}.
```

Both the variance and the standard deviation are commonly used in analyzing engineering data, so we give functions for computing both values. Note that the function for computing the standard deviation references the variance function and that the variance function references the mean function; thus, these functions must include the proper function prototype statements. Also, note that there must be at least two values in the array, or the variance function will attempt to divide by zero. Here are the two functions:

```cpp
/*-------------------------------------------------*/
/* This function returns the variance of an array x */
/* with npts elements.                             */
/*-------------------------------------------------*/
double variance(double x[],int npts)
{
	/* Declare variables and function prototypes. */
	int k;
	double sum=0, mu;
	double mean(double x[],int npts);

	/* Determine variance. */
	mu = mean(x,npts);
	for (k=0; k<npts-1; k++)
		sum += (x[k] - mu)*(x[k] - mu);

	/* Return variance */
	return sum/(npts-1);
}
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

## Custom Header File

The functions developed in this section are frequently used in solving engineering problems. To facilitate their use, we generate a custom header file that contains the prototype statements for these functions. Then, instead of including all the prototype statements in a main function, we can use a preprocessor directive that includes the custom header file.

The custom header file named stat_lib.h contains the following function prototype statements:

```cpp
double max(double x[],int n);
double min(double x[],int n);
double mean(double x[],int n);
double median(double x[],int n);
double variance(double x[],int n);
double std_dev(double x[],int n);
```

The statement that includes these function prototype statements in a main function is

```cpp
#include "stat_lib.h"
```

The use of this custom header is illustrated in the next section.

In addition to accessing the custom header file with the include statement, a program must also have access to the file stat_lib.c, which contains the statistical functions. The specific details of providing this access are system dependent and may involve adding a file name to the operating system command that performs the compilation and linking/loading operations.

## PRACTICE!

Assume that the array x is defined and initialized with the following statement:
double x[]={2.5,5.5,6.0,6.25,9.0};

Using a hand calculation, compute the values returned by the following function references:

- 1. max(x,5)
- 2. median(x,5)
- 3. variance(x,5)
- 4. std_dev(x,5)
- 5. min(x,4)
- 6. median(x,4)

## 5.5 Problem Solving Applied: Speech Signal Analysis

A speech signal is an acoustical signal that can be converted into an electrical signal with a microphone. The electrical signal can then be converted into a series of numbers that represents the amplitudes of the electrical signal values. These numbers can be stored in data files so that the speech signal can be analyzed using computer programs. Suppose that we are interested in analyzing speech signals for the words “zero,” “one,” “two,” ..., “nine.” The goal of this analysis is to develop ways of identifying the correct digit from a data file containing the utterance of an unknown digit.

### Utterance

Figure 5.2 contains a plot of an utterance of the digit “zero.” The analysis of this type of complicated signal often starts with computing some of the statistical measurements discussed in the last section. Other measurements used with speech signals include the average magnitude, or average absolute value, which is computed as

### Magnitude

Average magnitude = \(\frac{\sum_{k=0}^{n-1} |x_k|}{n}\) (5.4)

where n is the number of data values.

### Power

Another metric used in speech analysis is the average **power** of the signal, which is the average squared value:

Average power = \(\frac{\sum_{k=0}^{n-1} x_k^2}{n}\) (5.5)

### Zero crossings

The number of **zero crossings** in a speech signal is also a useful statistical measurement. This value is the number of times that the speech signal makes a transition from a negative to a positive value or from a positive to a negative value. A transition from a nonzero value to a zero value is not a zero crossing.

![](img/02c4582f051c5b51776411c92b079035_259_0.png)

Figure 5.2 Utterance of the word “zero.”

Write a program to read a speech signal from a data file named zero1.txt. This file contains values that represent an utterance of the word “zero.” Each line of the file contains a single value representing a measurement from the microphone taken in time increments of 0.000125 second, so 8000 measurements represent 1 second of data. The data file contains only valid data, with no header or trailer line; a maximum of 2500 values is contained in the file. Compute and print the following statistical measurements from the file: mean, standard deviation, variance, average power, average magnitude, and number of zero crossings.

### 1. PROBLEM DESCRIPTION

Compute the following statistical measurements for a speech utterance: mean, standard deviation, variance, average power, average magnitude, and number of zero crossings.

### 2. INPUT/OUTPUT DESCRIPTION

The I/O diagram shows the data file as the input and the statistical measurements as output.

![](img/02c4582f051c5b51776411c92b079035_259_1.png)

### 3. HAND EXAMPLE

For a hand example, assume that the file contains the following values:

2.5 8.2 -1.1 -0.2 1.5

Using a calculator, we can compute the following values:

Mean = \(\mu = \frac{(2.5 + 8.2 - 1.1 - 0.2 + 1.5)}{5}\)
= 2.18

Variance = \((2.5 - \mu)^2 + (8.2 - \mu)^2 + (-1.1 - \mu)^2 + (-0.2 - \mu)^2 + (1.5 - \mu)^2 / 4\)
= 13.307

Standard deviation = \(\sqrt{13.307}\)
= 3.648

Average power = \(\frac{[(2.5)^2 + (8.2)^2 + (-1.1)^2 + (-0.2)^2 + (1.5)^2]}{5}\)
= 15.398

Average magnitude = \(\frac{(|2.5| + |8.2| + |-1.1| + |-0.2| + |1.5|)}{5}\)
= 2.7

Number of zero crossings = 2.

### 4. ALGORITHM DEVELOPMENT

We first develop the decomposition outline because it divides the solution into a series of sequential steps:

### Decomposition Outline

- 1. Read the speech signal into an array.
- 2. Compute and print statistical measurements.

Step 1 involves reading the data file and determining the number of data points. Step 2 involves computing and printing the statistical measurements; use the functions already developed when possible. The structure chart shown in Figure 4.1 illustrates an example of a main function that references several programmer-defined functions. The refinement in pseudocode for the main function and for the necessary additional statistical functions follows:

### Refinement in Pseudocode

```
main: read speech signal from data file and
       determine the number of points, npts
       compute and print mean
       compute and print standard deviation
       compute and print variance
```
