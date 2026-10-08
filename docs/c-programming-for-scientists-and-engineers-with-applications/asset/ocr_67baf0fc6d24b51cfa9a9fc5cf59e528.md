the function returns control to the main program, the array z already contains the values assigned to the array s.

# 7.5.2 Passing Array Elements

Arrays can be passed to functions element-by-element either by value or by address, scalar variables. When an element of an array is passed to a function from the calling program, the index of the element must be specified. The following-code shows the passing of array elements by value and by address.

When array elements are passed to the function by value they are copied into temporary storage and the function parameter can only access the value in temporary storage. The following code shows array elements of an array passed by value and of array b passed by address a. The subfunction adds the elements of the two arrays plus two, one-by-one and returns the sums to the array b.

```
#include <stdio.h>
#define ARSIZE 5

void funcscalar(int, int *);

int main() {
{
    int i;
    int a[] = {1, 2, 3, 4, 5};
    int b[] = {6, 7, 8, 9, 10};

    for (i = 0; i < ARSIZE; i++) {
        funcscalar(a[i], &b[i]);
    }

    for (i = 0; i < ARSIZE; i++) {
        printf("%d %d\n", a[i], b[i]);
    }

    return 0;
}

void funcscalar(int x, int *y) {
{
    x = x + 2;
    *y = x + *y;
    return;
}
```