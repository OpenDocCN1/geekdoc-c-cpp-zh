# Introduction to Arrays

provided with initializers are initialized to zero. However, arrays with no initializers and other variables declared within a function definition, including the main function of a program, may not be initialized. Although array indexed variables (and other variables) may sometimes be automatically initialized to zero, you cannot and should not count on it.

If you initialize an array when it is declared, you can omit the size of the array, and the array will automatically be declared to have the minimum size needed for the initialization value. For example, the following declaration

```
int b[] = {5, 12, 11};
```

is equivalent to

```
int b[3] = {5, 12, 11};
```

# Self-Test Exercises

+   1. Describe the difference in the meaning of int a[5]; and the meaning of a[4]. What is the meaning of the [5] and [4] in each case?

+   2. In the array declaration
double score[5];nidentify the following:
a. The array name
b. The base type
c. The declared size of the array
d. The range of values an index accessing this array can have
e. One of the indexed variables (or elements) of this array

+   3. Identify any errors in the following array declarations.
int x[4] = {8, 7, 6, 4, 3};
int x[] = {8, 7, 6, 4};
const int SIZE = 4;
 x[SIZE];

+   4. What is the output of the following code?
char symbol[3] = {'a', 'b', 'c'};nfor(int index = 0; index < 3; index++)
cout << symbol[index];

(continued)