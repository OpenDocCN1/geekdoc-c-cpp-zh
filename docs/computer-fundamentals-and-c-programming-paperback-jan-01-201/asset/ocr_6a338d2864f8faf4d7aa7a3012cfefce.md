```
Enter 1 for addition or 2 for subtraction: 3
Illegal choice
Enter 1 for addition or 2 for subtraction: 1
Matrix after addition:
  13  13  13  13
  13  13  13  13
  13  13  13  13
Enter 1 for addition or 2 for subtraction: 2
Matrix after subtraction:
 -11  -9  -7  -5
  -3  -1   1   3
   5   7   9  11
```

PROGRAM OUTPUT: `matrix_add_subtract.c`

# 10.15.3 `matrix_multiply.c`: Multiplying Two Matrices

Matrix multiplication is not as straightforward as addition and subtraction. An *m × n* matrix can only be multiplied with an *n × p* matrix, which means that the number of columns of the first matrix must equal the number of rows of the second matrix. The resultant matrix has the dimensions *m × p*.

Matrix multiplication is performed by using the *dot-product* technique. The dot-product of two sets of numbers containing the same number of elements is the sum of the products of the corresponding elements. For matrices, the dot-product applies to the row elements of the first matrix and the column elements of the second matrix (Fig. 10.3).

| Matrix 1 | Matrix 2 | Matrix 3 |
|---|---|---|
| 1  2<br>3  4<br>5  6 | 6  5  4<br>3  2  1 | 12  9  6<br>30  23  16<br>48  37  26 |

**FIGURE 10.3**  Multiplying Two Matrices

The data for the matrices are obtained from the output of Program 10.15. The first element of matrix 3 (12) is evaluated by computing the dot-product of the first row of matrix 1 and the first column of matrix 2. For the second element (9), the dot-product is applied to the same row of matrix 1 and the second column of matrix 2. Thus, the first row of matrix 3 is evaluated in the following manner:

```
1 × 6 + 2 × 3 = 12    (mat3[0][0])
1 × 5 + 2 × 2 =  9    (mat3[0][1])
1 × 4 + 2 × 1 =  6    (mat3[0][2])
```

The second and third rows of matrix 3 are computed in a similar manner. Program 10.15 performs this dot-product evaluation where the matrix values are supplied by user input. The program also performs a compatibility test of the two matrices.