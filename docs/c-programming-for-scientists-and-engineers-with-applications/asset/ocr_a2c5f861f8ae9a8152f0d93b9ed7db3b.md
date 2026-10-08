# 7.3 Output of One-Dimensional Arrays 403

The elements of an array can be printed vertically in a column, as is done by the following code.

```
#define N 5
int i;
int a[N] = {12, 13, 25, 16, 43};

for(i = 0; i < N; i++)
{
    printf("%d\n", a[i]);
}
```

12
13
25
16
43

Output to a Data File "myfile.data"

```
#define A 5
FILE *outptr;
int i;
int a[A] = {12, 13, 25, 16, 43};

outptr = fopen("myfile.dat", "w");

for(i = 0; i < A; i++)
    fprintf(outptr, "%d", a[i]);
```

The output of the array elements will be written to a data file "myfile.dat" on a line with four blank spaces between each element as shown:

| myfile.dat |
| outptr -> 12 13 25 16 43 |

Notice that the integer number 12 is from the storage of element a[0], 13 is from the storage of element a[1], and so on, are written horizontally along a line to a data file "myfile.dat".