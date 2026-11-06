+   34. Which elements are on the diagonal joining the upper-left and the lower-right corners of the tic-tac-toe board?

**Practice It** Now you can try these exercises at the end of the chapter: R6.23, P6.19, P6.20.

# Common Error 6.2

# Omitting the Column Size of a Two-Dimensional Array Parameter

![](bbox=[0.133, 0.229, 0.187, 0.291])

When passing a one-dimensional array to a function, you specify the size of the array as a separate parameter variable:

```
```cpp
void print(double values[], int size)
```
```

This function can print arrays of any size. However, for two-dimensional arrays you cannot simply pass the numbers of rows and columns as parameter variables:

```
```cpp
void print(double table[][], int rows, int cols) // NO!
```
```

The function must know at compile time how many columns the two-dimensional array has. You must specify the number of columns with the array parameter variable. This number must be a constant:

```
```cpp
const int COLUMNS = 3;
void print(const double table[][COLUMNS], int rows) // OK
```
```

This function can print tables with any number of rows, but the column size is fixed.

# WORKED EXAMPLE 6.2

# A World Population Table

![](bbox=[0.095, 0.507, 0.183, 0.559])

This Worked Example shows how to print world population data in a table with row and column headers, and with totals for each of the data columns.

# 6.7 Vectors

A vector stores a sequence of values whose size can change.

When you write a program that collects values from user input, you don't always know how many values you will have. Unfortunately, the size of the array has to be known *when the program is compiled*.

In Section 6.1.3, you saw how you can address this problem with partially filled arrays. The vector construct, which we discuss in the following sections, offers a more convenient solution. A vector collects a sequence of values, just like an array does, but its size can change.

![](bbox=[0.654, 0.665, 0.894, 0.902])

*A vector expands to hold as many elements as needed.*