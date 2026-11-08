+   d. Store 5 in the first column, and make sure that the value in each subsequent column is twice the value in the previous column.
+   e. Print the array alpha one row per line.
+   f. Print the array alpha one column per line.

41. Consider the following declaration:

```
int beta[3][3];
```

What is stored in beta after each of the following statements executes?

```
a. for (i = 0; i < 3; i++)
        for (j = 0; j < 3; j++)
            beta[i][j] = 0;

b. for (i = 0; i < 3; i++)
        for (j = 0; j < 3; j++)
            beta[i][j] = i + j;

c. for (i = 0; i < 3; i++)
        for (j = 0; j < 3; j++)
            beta[i][j] = i * j;

d. for (i = 0; i < 3; i++)
        for (j = 0; j < 3; j++)
            beta[i][j] = 2 * (i + j) % 4;
```

42. Suppose that you have the following declarations:

```
int times[30][7];
int speed[15][7];
int trees[100][7];
int students[50][7];
```

+   a. Write the definition of the function print that can be used to output the contents of these arrays.
+   b. Write the C++ statements that calls the function print to output the contents of the arrays times, speed, trees, and students.

# PROGRAMMING EXERCISES

+   1. Write a C++ program that declares an array alpha of 50 components of type double. Initialize the array so that the first 25 components are equal to the square of the index variable, and the last 25 components are equal to three times the index variable. Output the array so that 10 elements per line are printed.
+   2. Write a C++ function, smallestIndex, that takes as parameters an int array and its size and returns the index of the first occurrence of the smallest element in the array. Also, write a program to test your function.
+   3. Write a C++ function, largestIndex, that takes as parameters an int array and its size and returns the index of the last occurrence of the largest element in the array. Also, write a program to test your function.