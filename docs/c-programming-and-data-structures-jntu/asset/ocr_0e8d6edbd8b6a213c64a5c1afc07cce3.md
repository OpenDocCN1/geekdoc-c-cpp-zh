When handling arrays, instead of using array indexing, we can use pointers to access array elements. Note that *(p+3) gives the value of x[3]. The pointer accessing method is much faster than array indexing.

The example 11.4 illustrates the use of pointer accessing method.

# Example 11.4

Write a program using pointers to compute the sum of all elements stored in an array.
The program shown in Fig. 11.8 illustrates how a pointer can be used to traverse an array. Since incrementing an array pointer causes it to point to the next element, we need only to add one to p each time we go through the loop.

```
Program
/*---------------------------------------------------------------*/
/* POINTERS IN ONE-DIMENSIONAL ARRAY */
/*---------------------------------------------------------------*/
main()
{
    int *p, sum, i;
    static int x[5] = {5, 9, 6, 3, 7};
    i = 0;
    p = x;
    sum = 0;
    printf("Element  Value  Address\n\n");
    while(i < 5)
    {
        printf("%d\t%d\t %u\n", i, *p);
        sum = sum + *p;
        i++; p++;
    }
    printf("\n Sum = %d\n", sum);
    printf("&x[0] = %u\n", &x[0]);
    printf("p = %u\n", p);
}
```

Output
Element | Value | Address
x[0] | 5 | 166
x[1] | 9 | 168
x[2] | 6 | 170
x[3] | 3 | 172
x[4] | 7 | 174
Sum = 55
&x[0] = 165
p = 176

# Fig. 11.8 Accessing array elements using the pointer

It is possible to avoid the loop control variable i as shown below:

```
p = x;
while(p <= &x[4])
```