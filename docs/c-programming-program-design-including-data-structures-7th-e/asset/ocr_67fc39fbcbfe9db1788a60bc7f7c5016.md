What is stored in `beta` after each of the following statements executes?

+   a.
+   ```cpp
+   for (i = 0; i < 3; i++)
+       for (j = 0; j < 3; j++)
+           beta[i][j] = 0;
+   ```

+   b.
+   ```cpp
+   for (i = 0; i < 3; i++)
+       for (j = 0; j < 3; j++)
+           beta[i][j] = i + j;
+   ```

+   c.
+   ```cpp
+   for (i = 0; i < 3; i++)
+       for (j = 0; j < 3; j++)
+           beta[i][j] = i * j;
+   ```

+   d.
+   ```cpp
+   for (i = 0; i < 3; i++)
+       for (j = 0; j < 3; j++)
+           beta[i][j] = 2 * (i + j) % 4;
+   ```

+   e.
+   ```cpp
+   for (int i = 2; i >= 0; i--)
+       for (int j = 0; j < 3; j++)
+           beta[i][j] = (i * j) % 3;
+   ```

44. Suppose that you have the following declarations: (15)

```
```cpp
int times[30][7];
int speed[15][7];
int trees[100][7];
int students[50][7];
```
```

+   a. Write the definition of the function `print` that can be used to output the contents of these arrays.

+   b. Write the C++ statements that calls the function `print` to output the contents of the arrays `times`, `speed`, `trees`, and `students`.

# PROGRAMMING EXERCISES

+   1. Write a C++ program that declares an array `alpha` of 50 components of type `double`. Initialize the array so that the first 25 components are equal to the square of the index variable, and the last 25 components are equal to three times the index variable. Output the array so that only 10 elements per line are printed.

+   2. Write a C++ function, `smallestIndex`, that takes as parameters an `int` array and its size and returns the index of the first occurrence of the smallest element in the array. Also, write a program to test your function.

+   3. Write a C++ function, `lastLargestIndex`, that takes as parameters an `int` array and its size and returns the index of the last occurrence of the largest element in the array. Also, write a program to test your function.

+   4. Write a program that reads a file consisting of students’ test scores in the range 0–200. It should then determine the number of students having scores in each of the following ranges: 0–24, 25–49, 50–74, 75–99, 100–124, 125–149, 150–174, and 175–200. Output the score ranges and the number of students. (Run your program with the following input data: 76, 89, 150, 135, 200, 76, 12, 100, 150, 28, 178, 189, 167, 200, 175, 150, 87, 99, 129, 149, 176, 200, 87, 35, 157, 189.)