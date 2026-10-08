# 494 Multidimensional Arrays

The following program shows the passing of two-dimensional arrays as arguments and parameters to functions that input, add, and output them.

```
#include <stdio.h>
#define IMAX 3
#define JMAX 4

void funcinput(int [][JMAX]);
void funcadd(int [][JMAX], int [][JMAX], int [][JMAX]);
void funcoutput(int [][JMAX]);

int main ()
{
    int a[IMAX][JMAX], b[IMAX][JMAX], c[IMAX][JMAX];
    funcinput(a);
    funcoutput(b);
    funcadd(a, b, c);
    printf("Array a:\n\n");
    funcoutput(a);
    printf("Array b:\n\n");
    funcoutput(b);
    printf("Array c:\n\n");
    funcoutput(c);
    return 0;
}

void funcinput (int arr[][JMAX])
{
    int i, j;
    for(i=0; i < IMAX; i++{
        for(j=0; j < JMAX; j++){
            scanf("%d", &arr[i][j]); /* assume IMAX*JMAX values are /* found for each array */
        }
    }
    return;
}
```