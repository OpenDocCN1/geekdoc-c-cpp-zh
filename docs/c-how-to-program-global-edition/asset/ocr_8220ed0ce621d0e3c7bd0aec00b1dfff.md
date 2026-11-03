+   c) Initialize the 50 elements of integer array numbers to zero.
+   
+   d) Print the 10 values of integer array GPA in column format.

6.13 Find the error(s) in each of the following statements:

+   a) Assume: `int a[5];`
+      `scanf("%d", a[5]);`
+   
+   b) Assume: `int a[3][3];`
+      `printf("%d%d%d\n", a[0][1], a[0][2], a[0][3]);`
+   
+   c) `double f[3] = { 1.1, 10.01, 100.001, };`
+   
+   d) Assume: `double d[3][5];`
+      `d[2, 4] = 2.345;`

6.14 (Union of Sets) Use one-dimensional arrays to solve the following problem. Read in two sets of numbers, each having 10 numbers. After reading all values, display all the unique elements in the collection of both sets of numbers. Use the smallest possible array to solve this problem.

6.15 (Intersection of Sets) Use one-dimensional arrays to solve the following problem. Read in two sets of numbers, each having 10 numbers. After reading all values, display the unique elements common to both sets of numbers.

6.16 Label the elements of 3-by-5 two-dimensional array sales to indicate the order in which they're set to zero by the following program segment:

```
```c
for (row = 0; row <= 2; ++row) {
    for (column = 0; column <= 4; ++column) {
        sales[row][column] = 0;
    }
}
```
```

6.17 What does the following program do?

```
```c
// ex06_17.c
// What does this program do?
#include <stdio.h>
#define SIZE 6

int whatIsThis(const int b[], size_t p);
// function prototype

// function main begins program execution
int main(void)
{
    int x; // holds return value of function whatIsThis
    // initialize array a
    int a[SIZE] = { 1, 2, 3, 4, 5, 6 };
    x = whatIsThis(a, SIZE);
    printf("Result is %d\n", x);
}

// what does this function do?
int whatIsThis(const int b[], size_t p)
{
    // base case
    if (1 == p) {

        return b[0];
    }
```
```