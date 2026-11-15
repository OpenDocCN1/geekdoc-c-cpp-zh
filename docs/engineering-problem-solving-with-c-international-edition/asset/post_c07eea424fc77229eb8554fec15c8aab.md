
**Factorials.** The following set of problems relates to computing factorials. If you did not cover the section on recursion, read the material on pages 200-201 for the definition of a factorial and then review the nonrecursive function for computing the factorial.

31. A convenient approximation for computing the factorial $n!$ for large values of $n$ is given by the Stirling formula

$$n! = \sqrt{2\pi n} \left(\frac{n}{e}\right)^n$$

where $e$ is the base for natural logarithms, or approximately 2.718282. Write an integer function for computing this approximation to a factorial. Assume that the corresponding prototype is

```
int n_fact(int n);
```

## Permutations

32. Suppose that we have $n$ distinct objects. There are many different orders that we can select to line up the objects in a row. In fact, there are $n!$ orderings, or **permutations**, that can be obtained with $n$ objects. If we have $n$ objects, and select $k$ of the objects, then there are $n!/(n - k)!$ possible orderings of $k$ objects. That is, the number of different permutations of $n$ different objects taken $k$ at a time is $n!/(n - k)!$. Write a function named `permute` that receives values for $n$ and $k$, and then returns the number of permutations of the $n$ objects taken $k$ at a time. (If we consider the set of digits $\{1, 2, 3\}$, the different permutations of two digits are $\{1, 2\}$, $\{2, 1\}$, $\{1, 3\}$, $\{3, 1\}$, $\{2, 3\}$, and $\{3, 2\}$.) Assume that the corresponding prototype is

```
int permute(int n, int k);
```

## Combinations

33. Whereas permutations (Problem 32) are concerned with order, combinations are not. Thus, given $n$ distinct objects, there is only one combination of $n$ objects taken $n$ at a time, but there are $n!$ permutations of $n$ distinct objects taken $n$ at a time. The number of **combinations** of $n$ objects, taken $k$ at a time is equal to $n!/((k!)(n - k)!)$. Write a function named `combine` that receives values for $n$ and $k$ and then returns the number of combinations of the $n$ objects taken $k$ at a time. (If we consider the set of digits $\{1, 2, 3\}$, the different combinations of two digits are $\{1, 2\}$, $\{1, 3\}$, and $\{2, 3\}$.) Assume that the corresponding prototype is

```
int combine(int n, int k);
```

34. The cosine of an angle can be computed from the following infinite series:

$$\cos x = 1 - \frac{x^2}{2!} + \frac{x^4}{4!} - \frac{x^6}{6!} + \cdots$$

Write a program that reads an angle $x$ (in radians) from the keyboard. Then, in a function, compute the cosine of the angle using the first five terms of this series. Print the value computed along with the value of the cosine computed using the C library function.

35. Modify the program in Problem 34 so that the approximation uses terms from the series as long as the absolute value of a term is greater than 0.0001. Print the number of terms used in the series approximation.

![](img/02c4582f051c5b51776411c92b079035_234_0.png)

## Crime Scene Investigation: Speech Analysis and Speech Recognition

In the four-color insert in Chapter 1 on biometrics, we discussed the use of speech recognition as a biometric. We also pointed out that speaker recognition (identifying people by their speech signals) is a very challenging problem. Some of the challenges relate to the fact that things that can cause a voice to change. For example, when you have a cold, your voice is different; when you are emotional or stressed, your voice is different. Current research has advanced enough that there are some examples of speech recognition (identifying the words in the speech, but not who is speaking) in commercial systems. A new fifth-generation fighter aircraft, the Joint Strike Fighter, is being designed with special speech recognition capabilities. In the initial checkout before a flight, the pilot will load the characteristics of his/her speech, and then during missions, the pilot will be able to verbally ask for information from the on-board computers. Speech analysis is a very common part of both commercial systems and crime scene investigations. For example, speech analysis can include analyzing audio signals to reduce the noise in the signals. It can also isolate background sounds such as sirens or aircraft noise to attempt to determine the location where the signal was collected. If there are a lot of speech data to analyze, automated routines can be written to do a number of things such as convert speech signals to text, determine the language being spoken, determine if the speaker is male or female, and even identify a regional dialect in the speech. In this chapter, we will develop a C program to perform some common speech analysis routines.

## ARRAYS AND MATRICES

### CHAPTER OUTLINE

- 5.1 One-Dimensional Arrays
- 5.2 Problem Solving Applied: Hurricane Categories
- 5.3 Problem Solving Applied: Molecular Weights
- 5.4 Statistical Measurements
- 5.5 Problem Solving Applied: Speech Signal Analysis
- 5.6 Sorting Algorithms
- 5.7 Search Algorithms
- 5.8 Two-Dimensional Arrays
- 5.9 Problem Solving Applied: Terrain Navigation
- 5.10 Matrices and Vectors*
- 5.11 Numerical Technique: Solution to Simultaneous Equations*
- 5.12 Problem Solving Applied: Electrical Circuit Analysis*
- 5.13 Higher Dimensional Arrays*
- Summary, Key Terms, C Statement Summary, Style Notes, Debugging Notes, Problems

### OBJECTIVES

In this chapter, we develop problem solutions containing:

- one-dimensional arrays.
- programmer-defined modules for the statistical analysis of data,
- functions that sort information and search for information,
- two-dimensional arrays,
- vector and matrix computations, and
- techniques for solving a system of simultaneous equations.

## 5.1 One-Dimensional Arrays

When solving engineering problems, it is important to be able to visualize the data related to the problem. Sometimes the data consist of just a single number, such as the radius of a circle. At other times, the data may be a coordinate in a plane that can be represented as a pair of numbers, with one number representing the x-coordinate and the other number representing the y-coordinate. There are also times when we want to work with a set of similar data values, but we do not want to give each value a separate name. For example, suppose that we have a set of 100 temperature measurements that we want to use to perform several computations.

*Optional section.

### Array

### One-Dimensional Array

Obviously, we do not want to use 100 different names for the temperature measurements, so we need a method for working with a group of values using a single identifier. One solution to this problem uses a data structure called an **array**. A **one-dimensional array** can be visualized as a list of values arranged in either a row or a column, as follows:

| 5 | 0 | -1 | 2 | 15 | 2 |
|---|---|---|---|---|---|
| s[0] | s[1] | s[2] | s[3] | s[4] | s[5] |

| t[0] | 0.0 |
|---|---|
| t[1] | 0.1 |
| t[2] | 0.2 |
| t[3] | 0.3 |

| 'a' | 'e' | 'i' | 'o' | 'u' |
|---|---|---|---|---|
| v[0] | v[1] | v[2] | v[3] | v[4] |

![](img/02c4582f051c5b51776411c92b079035_236_0.png)

### Elements Subscripts

We assign an identifier to an array, and then we distinguish between **elements** or values in the array using **subscripts**. In C, the subscripts always start with 0 and increment by 1. Thus, by using the example arrays, the first value in the `s` array is referenced by `s[0]`, the third value in the `t` array is referenced by `t[2]`, and the last value in the array `v` is referenced by `v[4]`.

Arrays are convenient for storing and handling large amounts of data, so there is a tendency to use them in algorithms when they are not necessary. Arrays are more complicated to use than simple variables, and thus make programs longer and more difficult to debug. Therefore, use arrays only when it is necessary to have the complete set of data available in memory.

### Definition and Initialization

An array is defined using declaration statements. The identifier is followed by an integer expression in brackets that specifies the number of elements in the array. Note that all elements in an array must be the same data type. The declaration statements for the three example arrays are as follows:

```
int s[6];
char v[5];
double t[4];
```

An array can be initialized with declaration statements or with program statements. To initialize the array with a declaration statement, the values are specified in a sequence that is separated by commas and enclosed in braces. To define and initialize the sample arrays `s`, `v`, and `t`, use the following statements:

```
int s[6]={5,0,-1,2,15,2};
char v[5]={'a','e','i','o','u'};
double t[4]={0.0,0.1,0.2,0.3};
```

If the initializing sequence is shorter than the array, then the rest of the values are initialized to zero. Hence, if we want to define an integer array of 100 values, where each value is also initialized to zero, we would use the following statement:

```
int s[100]={0};
```
