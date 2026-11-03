```
x = 100;
 y = 200;
 printf("Before exchange : x = %d\t y = %d\n\n", x, y);
 exchange(&x,&y);  /* call */
 printf("After exchange  : x = %d\t y = %d\n\n", x, y);
 }
 exchange (int *a, int *b)
 {
   int t;
   t = *a;   /* Assign the value at address a to t */
   *a = *b;  /* put b into a */
   *b = t;   /* put t into b */
 }

 Output

 Before exchange  : x = 100   y = 200
 After exchange   : x = 200   y = 100
```

# Fig. 6.11 Passing of pointers as function parameters

You may note the following points:

+   1. The function parameters are declared as pointers.
+   2. The dereferenced pointers are used in the function body.
+   3. When the function is called, the addresses are passed as actual arguments.

The use of pointers to access array elements is very common in C. We have used a pointer to traverse array elements in Example 6.4. We can also use this technique in designing user-defined functions discussed in Chapter 12. Let us consider the problem sorting an array of integers discussed in Example 5.6.

The function sort may be written using pointers (instead of array indexing) as shown:

```
void sort (int m, int *x)
{
  int i, j, temp;
  for (i=1; i<=m-1; i++)
    for (j=1; j<=m-i; j++)
      if (*(x+j-1) > *(x+j))
      {
        temp = *(x+j-1);
        *(x+j-1) = *(x+j);
        *(x+j) = temp;
      }
}

Note that we have used the pointer x (instead of array x[]) to receive the address of array passed and therefore the pointer x can be used to access the array elements (as pointed out in Section 6.10). This function can be used to sort an array of integers as follows:

int score[4] = {45, 90, 71, 83};
sort(4, score);  /* Function call */

The calling function must use the following prototype declaration.

void sort (int, int *);
```