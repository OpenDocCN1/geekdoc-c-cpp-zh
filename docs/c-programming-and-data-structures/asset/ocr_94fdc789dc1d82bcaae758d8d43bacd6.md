```
for( i = 0 ; i < 10 ; i++ )
    total = total + x[i] * x[i] ;

/* . . . PRINTING OF x[i] VALUES AND TOTAL . . . */

printf("\n");
for( i = 0 ; i < 10 ; i++ )
    printf("[x%2d] = %5.2f\n", i+1, x[i]) ;

printf("\nTotal = %.2f\n", total) ;
}
```

Output
ENTER 10 REAL NUMBERS

1.1 2.2 3.3 4.4 5.5 6.6 7.7 8.8 9.9 10.10

x[ 1] = 1.10
x[ 2] = 2.20
x[ 3] = 3.30
x[ 4] = 4.40
x[ 5] = 5.50
x[ 6] = 6.60
x[ 7] = 7.70
x[ 8] = 8.80
x[ 9] = 9.90
x[10] = 10.10
Total = 446.86

Fig. 3.1 Program to illustrate one-dimensional array

NOTE: C99 permits arrays whose size can be specified at run time. See Appendix 'C99 Features'.

# 3.4 INITIALIZATION OF ONE-DIMENSIONAL ARRAYS

After an array is declared, its elements must be initialized. Otherwise, they will contain "garbage". An array can be initialized at either of the following stages:

+   - At compile time
+   - At run time

# 3.4.1 Compile Time Initialization

We can initialize the elements of arrays in the same way as the ordinary variables when they are declared. The general form of initialization of arrays is:

```
type array_name[size]={ column_size };
```