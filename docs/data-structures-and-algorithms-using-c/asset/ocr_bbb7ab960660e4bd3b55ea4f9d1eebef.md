# InsertionBefore the Given Index of an Array

In this scenario we are given a location (index) of an array before which a new data element (value) has to be inserted. This time we seek till index-1, i.e., one location ahead of the given index. Rest of the activities are the same as in the previous example.

# Algorithm

We assume A is an array with N elements. The maximum numbers of elements it can store is defined by MAX.
begin
IF N = MAX, return ELSE
N = N + 1
SEEK Location index
For All Elements from A[index - 1] to A[N] Move to next adjacent location
A[index - 1] = New_Element end

# Implementation in C

```
#include <stdio.h> #define MAX 5
void main() {
int array[MAX] = {1, 2, 4, 5};

int N = 4;
int i = 0;
int index = 3; int value = 3; // number of elements in array
// loop variable
// index location before which value will be inserted // new data element to be inserted

// print array before insertion
printf("Printing array before insertion –\n"); for(i = 0; i < N; i++) {
printf("array[%d] = %d\n", i, array[i]); }
// now shift rest of the elements downwards for(i = N; i >= index + 1; i--) {
array[i + 1] = array[i];
}
// add new element at first position array[index + 1] = value;
// increase N to reflect number of elements N++;
// print to confirm
printf("Printing array after insertion –\n");
for(i = 0; i < N; i++) {
printf("array[%d] = %d\n", i, array[i]);
}
}
```

If we compile and run the above program, it will produce the following result –

Printing array before insertion – array[1] = 2