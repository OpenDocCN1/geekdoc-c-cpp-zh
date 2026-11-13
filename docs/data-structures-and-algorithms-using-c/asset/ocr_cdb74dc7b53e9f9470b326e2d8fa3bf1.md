# Insertion at the Beginning of an Array

When the insertion happens at the beginning, it causes all the existing data items to shift one step downward. Here, we design and implement an algorithm to insert an element at the beginning of an array.

# Algorithm

We assume A is an array with N elements. The maximum numbers of elements it can store is defined by MAX. We shall first check if an array has any empty space to store any element and then we proceed with the insertion process.

```
begin
IF N = MAX, return ELSE
N = N + 1
For All Elements in A
Move to next adjacent location
A[FIRST] = New_Element end
```

# Implementation in C

```
#include <stdio.h> #define MAX 5

void main(){
int array[MAX] = { 2, 3, 4, 5};
int N = 4; // number of elements in array int i = 0; // loop variable
int value = 1; // new data element to be stored in array

// print array before insertion
printf("Printing array before insertion \n"); for(i = 0; i < N; i++) {
printf("array[%d] = %d \n", i, array[i]); }

// now shift rest of elements downwards for(i = N; i >= 0; i--) {
array[i+1] = array[i];
}

// add new element at first position array[0] = value;
// increase N to reflect number of elements N++;
// print to confirm
printf("Printing array after insertion \n");

for(i = 0; i < N; i++) {
printf("array[%d] = %d\n", i, array[i]);
}
}
```

This program should yield the following output –

```
Printing array before insertion – array[0] = 2
array[1] = 3
array[2] = 4
```