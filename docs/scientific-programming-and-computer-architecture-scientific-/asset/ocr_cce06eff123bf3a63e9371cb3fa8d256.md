is different. The storage format for the $4 	imes 200 	imes 4$ microkernel was assumed to be such as to lead to a high throughput of arithmetic operations. For the following rows of the table, the storage formats are chosen to allow for convenient and efficient invocation of the function that corresponds to the preceding row of the table.

The matrices are denoted using capitalized letters when they are in column-major order with a leading dimension that may exceed the number of rows. Lowercase letters are used for other storage formats.

So, for the arrays that store the arguments to the $4 	imes 200 	imes 4$ microkernel $a[]$, $b[]$, and $c[]$. The microkernel performs $4 	imes 200 	imes 4$ matrix multiplication as the sum of 200 outer products of $4 	imes 1$ and $1 	imes 4$ matrices. Accordingly, the array $a[]$ is assumed to store a $4 	imes 200$ matrix in column-major order. The array $b[]$ is assumed to store a $200 	imes 4$ matrix in row-major order. In both cases, the leading dimension is equal to 4. The $i$th outer product accesses the

```
$a[4i, \dots, i+3] \quad b[4i, \dots, i+3]$
```

The array $c[]$ is of length 16 and stores a $4 	imes 4$ matrix. In 3.3.4, we assumed that the storage format of $c[]$ was column-major with "skewing." The skewing can be done using a single step of unskewing, which introduces only an insignificant overhead at the end. Therefore, we ignore it, although skewing percolates down the rows of table 4.7, implying that the matrix $C$ of dimension 9,000 corresponding to the last row of the table needs to be skewed. Thus, the array $c[]$ is assumed to store a $4 	imes 4$ matrix in column-major format (with skimming, which we ignore here) with leading dimension equal to 4.

As we progress down rows of table 4.7, the implementation of each row re the lower case letters $a, b, c$, assuming whatever format is most suitable for its purposes.

Closely related to storage formats is the use of work space. To allow for changes in storage format, the matrix multiplication functions use extra memory stored in an array $scratch[]$. The size of this array in its original incarnation is

```
$600 \times 12 + 600 \times 200 + 200 \times 3000$
```

double-precision numbers. The three terms correspond to $c[]$, $a[]$, and $b[]$, respectively. The multiplication of square matrices of dimension 9000 is partitioned