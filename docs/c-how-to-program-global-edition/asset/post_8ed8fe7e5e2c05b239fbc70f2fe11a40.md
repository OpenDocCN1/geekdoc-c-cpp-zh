
## 6.5
- a) Error: Semicolon at the end of the `#define` preprocessor directive.
  Correction: Eliminate semicolon.
- b) Error: Assigning a value to a symbolic constant using an assignment statement.
  Correction: Assign a value to the symbolic constant in a `#define` preprocessor directive without using the assignment operator as in `#define SIZE 10`.
- c) Error: Referencing an array element outside the bounds of the array (b[10]).
  Correction: Change the final value of the control variable to 9.
- d) Error: Semicolon at the end of the `#include` preprocessor directive.
  Correction: Eliminate semicolon.
- e) Error: Array indexing done incorrectly.
  Correction: Change the statement to `a[1][1] = 5;`
- f) Error: Assigning a value to a symbolic constant using an assignment statement.
  Correction: Assign a value to the symbolic constant in a `#define` preprocessor directive without using the assignment operator as in `#define VALUE 120`.

## Exercises

### 6.6 Fill in the blanks in each of the following:
- a) Arrays are ______ entities as they remain the same size during program execution.
- b) An array is a ______ group of memory locations that share the same ______.
- c) The first element in every array is the ______ element, for example, the first element of an array is referred to as ______.
- d) Array elements are referred by ______ followed by the ______ of the element.
- e) Arrays are passed to functions by ______.
- f) C has no array ______, which means a program can accidentally store data passing the bound of the array.
- g) The ______ operator cannot be used directly with arrays for copying data from one array to another.
- h) Every string contains a special string-termination character called the ______ character, represented by the character constant ______.
- i) A 5-by-7 array contains ______ rows, ______ columns and ______ elements
- j) The name of the element in the second row and third column of an array would be ______.

### 6.7 State which of the following are true and which are false. If false, explain why.
- a) If there are fewer initializers in an initializer list than the number of elements in the array, the remaining elements will contain garbage values.
- b) A static local variable in a function definition exists for the duration of the program.
- c) The type `size_t` represents an unsigned integral type
- d) If the array size is omitted from a definition with an initializer list, the number of elements in the array will not be defined.
- e) To calculate the amount of memory used by an array, multiply the number of elements by the size in bytes each element occupies.
- f) When individual array elements are passed to a function, they are passed by reference and their modified value is retained in the calling function.

### 6.8 Write statements to accomplish each of the following:
- a) Multiply the value of element 4 of an integer array `n` with 3 and display it.
- b) Write a loop that adds all the elements of the array `n[10]` and stores the result in `total`.
- c) Initialize each of the 9 elements of a two-dimensional integer array `n[3][3]` to 3, using loops.
- d) Find the largest and smallest element of a two dimensional array `sales[4][5]`.
- e) Copy a 100-element array into a 200-element array, starting from the 100th position of the larger array.
- f) Determine and store the sum and difference of the values contained in two, 100-element double arrays a1 and a2, into double arrays sum and difference.

### 6.9 Consider a 5-by-20 integer array grades:
- a) Write a declaration for grades.
- b) How many rows does the array have?
- c) How many columns does the array have?
- d) How many elements does the array have?
- e) Write the names of all elements in the first column of the array.
- f) Write the name of the element in the third row and second column of the array.
- g) Write a single statement to assign the value 100 to the element in the first row and second column.
- h) Write a nested loop to get all the elements from the keyboard.
- i) Write a nested for statement to initialize all elements to zero.
- j) Write a statement that copies the values from an array double mathGrades[20] into the elements of the first row of grades.
- k) Write a series of statements that determine and print the highest value in the first row of grades.
- l) Write a statement to display the elements in column 2 of the array.
- m) Write a statement to calculate the average of the elements in the first row.
- n) Write a series of statements that prints the array grades in a tabular format. List the column subscripts as headings across the top and list the row subscripts at the left of each row.

### 6.10 (Sales Commissions) Use a one-dimensional array to solve the following problem.
A company pays its salespeople on a commission basis. The salesperson receive $200 per week plus 9% of their gross sales for that week. For example, a salesperson who grosses $3,000 in sales in a week receives $200 plus 9% of $3,000, or a total of $470. Write a C++ program (using an array of counters) that determines how many of the salespeople earned salaries in each of the following ranges (assume that each salesperson's salary is truncated to an integer amount):
- a) $200–299
- b) $300–399
- c) $400–499
- d) $500–599
- e) $600–699
- f) $700–799
- g) $800–899
- h) $900–999
- i) $1000 and over

### 6.11 (Selection Sort) A selection sort algorithm for a one-dimensional array has the following steps:
- a) The smallest value in the array is found.
- b) It is swapped with the value in the first position of the array.
- c) The above steps are repeated for the rest of the array starting at the second position and advancing each time.

Eventually the entire array is divided into two parts: the sub-array of items already sorted which is built up from left to right and is found at the beginning, and the sub-array of items remaining to be sorted, occupying the remainder of the array. Write a program that sorts an array of 10 integers using this algorithm.

### 6.12 Write loops that perform each of the following one-dimensional array operations:
- a) Read the 20 elements of double array sales from the keyboard.
- b) Add 1000 to each of the 75 elements of double array allowance.
- c) Initialize the 50 elements of integer array numbers to zero.
- d) Print the 10 values of integer array GPA in column format.

### 6.13 Find the error(s) in each of the following statements:
- a) Assume: `int a[5];`
  `scanf("%d", a[5]);`
- b) Assume: `int a[3][3];`
  `printf("%d%d%d\n", a[0][1], a[0][2], a[0][3]);`
- c) `double f[3] = { 1.1, 10.01, 100.001, };`
- d) Assume: `double d[3][5];`
  `d[2, 4] = 2.345;`

### 6.14 (Union of Sets) Use one-dimensional arrays to solve the following problem. Read in two sets of numbers, each having 10 numbers. After reading all values, display all the unique elements in the collection of both sets of numbers. Use the smallest possible array to solve this problem.

### 6.15 (Intersection of Sets) Use one-dimensional arrays to solve the following problem. Read in two sets of numbers, each having 10 numbers. After reading all values, display the unique elements common to both sets of numbers.

### 6.16 Label the elements of 3-by-5 two-dimensional array sales to indicate the order in which they're set to zero by the following program segment:
```c
for (row = 0; row <= 2; ++row) {
    for (column = 0; column <= 4; ++column) {
        sales[row][column] = 0;
    }
}
```

### 6.17 What does the following program do?
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
