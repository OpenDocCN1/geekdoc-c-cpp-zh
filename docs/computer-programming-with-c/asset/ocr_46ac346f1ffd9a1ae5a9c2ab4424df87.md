Since addition is performed in parenthesis, the address 1014 will be added with constant 3 before resolving the indirection operator *. Remember, 1014 is an address of a 2 bytes location, therefore 1014+3 is actually evaluated as `1014+3*2=1020`. Hence, Equation 3 is simplified as:

`* (1020) - Equation 4`

Applying indirection operator on address 1020 will fetch the contents of memory locations 1020 which is an integer value 80.

Hence we have proved that, `*(*(p+1)+3)` gives the value 80, which is actually `a[1][3]`.

Similarly, every element of an array `a[i][j]` can be accessed as `*(*(p+i)+j)`.

> **CONCLUSION**
> 
> Given an 2D array `a` and a 2D pointer `p` such that,
> `p = (int**)a;`
> then every element `a[i][j]` can be accessed using pointer `p` as `*(*(p+i)+j)`
> Needless to say that if you drop the outermost `*` operator, you will get the **address** of `a[i][j]`. Hence `&a[i][j]` is equivalent to `*(p+i)+j`.

# 8.11.1  Program to perform addition of 2 matrices using pointers: An example

As we have already implemented the solution to perform matrix operations in the Chapter 6, we will reuse the same solution to add the two matrices using **pointers**. As discussed in Chapter 6, we created three 2-D arrays a, b, and res, such that the result of addition of matrix a with matrix b is stored in matrix res. As there are three 2-D arrays we create three ‘pointer to pointer’ variables p, q, and r such that the pointer p points to matrix, pointer q points to matrix b, and pointer r points to matrix res as shown in the lines below:

```
/*Create three pointer to pointer variables*/
int **p, **q, **r;
/*make p,q, and r point to matrices a, b and "res" respectively*/
p=(int**)a;
q=(int**)b;
r=(int**) res;
```

The following code is same as that of Chapter 6, except every access to element `a[i][j]` is now done using an expression `*(*(p+i)+j)`.

Following substitutions are required to be applied on the solution discussed in Chapter 6, to solve the same program using pointers:

+   1. Every occurrence of `a[i][j]` in the code should be replaced by `*(*(p+i)+j)`
+   2. Every occurrence of `&a[i][j]` in the code should be replaced by `*(p+i)+j`
+   3. Every occurrence of `b[i][j]` in the code should be replaced by `*(*(q+i)+j)`
+   4. Every occurrence of `&b[i][j]` in the code should be replaced by `*(q+i)+j`
+   5. Every occurrence of `res[i][j]` in the code should be replaced by `*(*(r+i)+j)`