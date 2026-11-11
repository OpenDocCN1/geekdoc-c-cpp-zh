```
1       3       3       1
1       4       6       4       1
1       5       10      10      5       1
-       -       -       -       -       -
-       -       -       -       -       -       -
```

If we denote rows by i and columns by j, then any element (except the boundary elements) in the triangle is given by
P_ij = P_{i-1, j-1} + P_{i-1, j}

Write a program to calculate the elements of the Pascal triangle for 10 rows and print the results.

5. The annual examination results of 100 students are tabulated as follows:

![](bbox=[0.64, 0.31, 0.71, 0.33])

| Roll No. | Subject 1 | Subject 2 | Subject 3 |
|---|---|---|---|
| . | | | |
| . | | | |

Write a program to read the data and determine the following:

+   (a) Total marks obtained by each student.
+   (b) The highest marks in each subject and the Roll No. of the student who secured it.
+   (c) The student who obtained the highest total marks.

6. Given are two one-dimensional arrays A and B which are sorted in ascending order. Write a program to merge them into a single sorted array C that contains every item from arrays A and B, in ascending order.

![](bbox=[0.64, 0.49, 0.71, 0.51])

7. Two matrices that have the same number of rows and columns can be multiplied to produce a third matrix. Consider the following two matrices.

![](bbox=[0.64, 0.55, 0.71, 0.57])

```
        a11 a12 .... a1n
        a12 a22 .... a2n
    A = .                 .
        .                 .
        an1 .... .... ann
```

```
        b11 b12 .... b1n
        b12 b22 .... b2n
    B = .                 .
        .                 .
        bn1 .... .... bnn
```

The product of A and B is a third matrix C of size n x n where each element of C is given by the following equation: