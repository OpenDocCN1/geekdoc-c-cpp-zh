they are stored in the memory. They are stored in the order of planes, rows, and columns.

Array Assignment The following code shows the assignment of a scalar
5.8 to each of the elements of a three-dimensional array.

```
#define KMAX 3
#define IMAX 4
#define JMAX 5

int main ()
{
    float x[KMAX][IMAX][JMAX];
    int i, j, k;

    for(k = 0; k < KMAX; k++)
    {
        for(i = 0; i < IMAX; i++)
        {
            for(j = 0; j < JMAX; j++)
            {
                x[k][i][j] = 5.8;
            }
        }
    }
    return 0;
}
```

The following code shows the assignment of array y to array x.

```
#define KMAX 3
#define IMAX 4
#define JMAX 5

int main ()
{
    float x[KMAX][IMAX][JMAX], y[KMAX][IMAX][JMAX];
    int i, j, k;

    for(k = 0; k < KMAX; k++)
    {
        for(i = 0; i < IMAX; i++)
        {
            for(j = 0; j < JMAX; j++)
            {
            }
        }
    }
}
```