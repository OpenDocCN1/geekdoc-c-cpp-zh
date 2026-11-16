The code below randomly populates a 100-element array with integers. The array contents are displayed, qsort() is called, and the array contents are displayed again showing the sorted data items.

```
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#define SIZE 100
int compare(const void *p, const void *q);
void output(int num[], int size);
int main() {
    int i, num[SIZE];
    srand((unsigned)time(NULL));
    for (i = 0; i < SIZE; i++) {
        num[i] = (rand() % 50000);
    }
    printf("Before sort\n");
    output(num, SIZE);
    qsort(num, SIZE, sizeof(int), compare);
    printf("\nAfter sort\n");
    output(num, SIZE);
    return(0);
}
int compare(const void *p, const void *q) {
    if (*(int *)p < *(int *)q) {
        return -1;
    }
    return *(int *)p > *(int *)q;
}
void output(int num[], int size) {
    int i;
    for (i = 0; i < size; i++) {
        printf("%6d", num[i]);
        if (i % 10 == 9 || (i == size -1)) {
            printf("%c", '\n');
        }
        else {
            printf("%c", ' ');
        }
    }
}
```

# if array
qsort(x, &, sizeof(int), compare)
Compute(A, B)
if A=B, return
if B>A, -1
if A>B, 1

general type that has to be cleaned
giving directions to a new value assigned for comparison pointers
casting to
change from any type to a new type 'int'

Cause void* points to memory
that should not be modified.