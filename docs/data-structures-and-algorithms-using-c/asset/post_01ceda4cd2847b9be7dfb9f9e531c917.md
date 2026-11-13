
## 21. Bubble Sort Algorithm Data Structures & Algorithms

Bubble sort is a simple sorting algorithm. This sorting algorithm is comparison-based algorithm in which each pair of adjacent elements is compared and the elements are swapped if they are not in order. This algorithm is not suitable for large data sets as its average and worst case complexity are of O(n²) where n is the number of items.

### How Bubble Sort Works?

We take an unsorted array for our example. Bubble sort takes O(n²) time so we're keeping it short and precise.

| 14 | 33 | 27 | 35 | 10 |
|---|---|---|---|---|

Bubble sort starts with very first two elements, comparing them to check which one is greater.

| 14 | 33 | 27 | 35 | 10 |
|---|---|---|---|---|

In this case, value 33 is greater than 14, so it is already in sorted locations. Next, we compare 33 with 27.

| 14 | 33 | 27 | 35 | 10 |
|---|---|---|---|---|

We find that 27 is smaller than 33 and these two values must be swapped.

| 14 | 33 | 27 | 35 | 10 |
|---|---|---|---|---|

The new array should look like this –

| 14 | 27 | 33 | 35 | 10 |
|---|---|---|---|---|

Next we compare 33 and 35. We find that both are in already sorted positions.

| 14 | 27 | 33 | 35 | 10 |
|---|---|---|---|---|

Then we move to the next two values, 35 and 10.

| 14 | 27 | 33 | 35 | 10 |
|---|---|---|---|---|

We know then that 10 is smaller than 35. Hence they are not sorted.

| 14 | 27 | 33 | 35 | 10 |
|---|---|---|---|---|

We swap these values. We find that we have reached the end of the array. After one iteration, the array should look like this –

| 14 | 27 | 33 | 10 | 35 |
|---|---|---|---|---|

To be precise, we are now showing how an array should look like after each iteration. After the second iteration, it should look like this –

| 14 | 27 | 10 | 33 | 35 |
|---|---|---|---|---|

Notice that after each iteration, at least one value moves at the end.

| 14 | 10 | 27 | 33 | 35 |
|---|---|---|---|---|

And when there’s no swap required, bubble sort learns that an array is completely sorted. Now we should look into some practical aspects of bubble sort.

### Algorithm

We assume **list** is an array of **n** elements. We further assume that **swap** function swaps the values of the given array elements.

```
begin BubbleSort(list)
for all elements of list
if list[i] > list[i+1] swap(list[i], list[i+1]) end if
end for
return list end BubbleSort
```

### Pseudocode

We observe in algorithm that Bubble Sort compares each pair of array element unless the whole array is completely sorted in an ascending order. This may cause a few complexity issues like what if the array needs no more swapping as all the elements are already ascending.

To ease-out the issue, we use one flag variable **swapped** which will help us see if any swap has happened or not. If no swap has occurred, i.e. the array requires no more processing to be sorted, it will come out of the loop.

Pseudocode of BubbleSort algorithm can be written as follows –

```
procedure bubbleSort( List : array of items )
loop = list.count;
for i = 0 to loop-1 do: swapped = false
for j = 0 to loop-1 do:
/*compare the adjacent elements */if list[j] > list[j+1] then
/* swap them */
swap( list[j], list[j+1] )
swapped = true end if
end for
/*if no number was swapped that means array is sorted now, break the loop.*/
if(not swapped) then break
end if
end for end procedure return list
```

### Implementation

One more issue we did not address in our original algorithm and its improvised pseudocode, is that, after every iteration the highest values settles down at the end of the array. Hence, the next iteration need not include already sorted elements. For this purpose, in our implementation, we restrict the inner loop to avoid already sorted values.

To know about bubble sort implementation in C programming language, please click here.

### Bubble Sort Program in C

We shall see the implementation of **bubble sort** in C programming language here.

### Implementation in C

```c
#include <stdio.h>
#include <stdbool.h>
#define MAX 10
int list[MAX] = {1,8,4,6,0,3,5,2,7,9};
void display(){
   int i;
   printf("["); // navigate through all items
   for(i = 0; i < MAX; i++){
      printf("%d ",list[i]);
   }
   printf("]\n");
}
void bubbleSort() {
   int temp;
   int i,j;
   bool swapped = false;
   // loop through all numbers
   for(i = 0; i < MAX-1; i++) {  swapped = false;
      // loop through numbers falling ahead
      for(j = 0; j < MAX-1-i; j++) {
         printf("Items compared: [ %d, %d ] ",list[j],list[j+1]);
         // check if next number is lesser than current no  //swap the numbers.
         // (Bubble up the highest number)
         if(list[j] > list[j+1]) {
            temp = list[j];
            list[j] = list[j+1];
            list[j+1] = temp;
            swapped = true;
            printf("=> swapped [%d, %d]\n",list[j],list[j+1]);
         } else {
            printf("=> not swapped\n");
         }
      }
      // if no number was swapped that means  // array is sorted now, break the loop.
      if(!swapped) {
         break;
      }
      printf("Iteration %d#: ",(i+1));
      display();
   }
}
main(){
   printf("Input Array: ");
   display();
   printf("\n");
   bubbleSort();
   printf("\nOutput Array : "); display();
}
```

```
Input Array: [1 8 4 6 0 3 5 2 7 9]
Items compared: [ 1, 8 ] => not swapped Items compared: [ 8, 4 ] => swapped [4, 8] Items compared: [ 8, 6 ] => swapped [6, 8] Items compared: [ 8, 0 ] => swapped [0, 8] Items compared: [ 8, 3 ] => swapped [3, 8] Items compared: [ 8, 5 ] => swapped [5, 8] Items compared: [ 8, 2 ] => swapped [2, 8] Items compared: [ 8, 7 ] => swapped [7, 8] Items compared: [ 8, 9 ] => not swapped
Iteration 1#: [1 4 6 0 3 5 2 7 8 9]
Items compared: [ 1, 4 ] => not swapped Items compared: [ 4, 6 ] => not swapped Items compared: [ 6, 0 ] => swapped [0, 6] Items compared: [ 6, 3 ] => swapped [3, 6] Items compared: [ 6, 5 ] => swapped [5, 6] Items compared: [ 6, 2 ] => swapped [2, 6] Items compared: [ 6, 7 ] => not swapped Items compared: [ 7, 8 ] => not swapped
Iteration 2#: [1 4 0 3 5 2 6 7 8 9]
Items compared: [ 1, 4 ] => not swapped Items compared: [ 4, 0 ] => swapped [0, 4] Items compared: [ 4, 3 ] => swapped [3, 4] Items compared: [ 4, 5 ] => not swapped Items compared: [ 5, 2 ] => swapped [2, 5] Items compared: [ 5, 6 ] => not swapped Items compared: [ 6, 7 ] => not swapped
Iteration 3#: [1 0 3 4 2 5 6 7 8 9]
Items compared: [ 1, 0 ] => swapped [0, 1] Items compared: [ 1, 3 ] => not swapped Items compared: [ 3, 4 ] => not swapped Items compared: [ 4, 2 ] => swapped [2, 4] Items compared: [ 4, 5 ] => not swapped Items compared: [ 5, 6 ] => not swapped
Iteration 4#: [0 1 2 3 4 5 6 7 8 9]
Items compared: [ 0, 1 ] => not swapped Items compared: [ 1, 3 ] => not swapped Items compared: [ 3, 2 ] => swapped [2, 3] Items compared: [ 3, 4 ] => not swapped Items compared: [ 4, 5 ] => not swapped
Iteration 5#: [0 1 2 3 4 5 6 7 8 9]
Items compared: [ 0, 1 ] => not swapped Items compared: [ 1, 2 ] => not swapped Items compared: [ 2, 3 ] => not swapped Items compared: [ 3, 4 ] => not swapped
Output Array: [0 1 2 3 4 5 6 7 8 9 ]
```

## 22. Insertion Sort Data Structures & Algorithms

This is an in-place comparison-based sorting algorithm. Here, a sub-list is maintained which is always sorted. For example, the lower part of an array is maintained to be sorted. An element which is to be ‘insert’ed in this sorted sub-list, has to find its appropriate place and then it has to be inserted there. Hence the name, **insertion sort**.

The array is searched sequentially and unsorted items are moved and inserted into the sorted sub-list (in the same array). This algorithm is not suitable for large data sets as its average and worst case complexity are of O(n²), where n is the number of items.

### How Insertion Sort Works?

We take an unsorted array for our example.

![](img/30fc9e3f8ee01facfae8d1c9621936b3_166_0.png)

Insertion sort compares the first two elements.

![](img/30fc9e3f8ee01facfae8d1c9621936b3_166_1.png)

It finds that both 14 and 33 are already in ascending order. For now, 14 is in sorted sublist.

![](img/30fc9e3f8ee01facfae8d1c9621936b3_166_2.png)

Insertion sort moves ahead and compares 33 with 27.

![](img/30fc9e3f8ee01facfae8d1c9621936b3_166_3.png)

And finds that 33 is not in the correct position.

![](img/30fc9e3f8ee01facfae8d1c9621936b3_166_4.png)

It swaps 33 with 27. It also checks with all the elements of sorted sub-list. Here we see that the sorted sub-list has only one element 14, and 27 is greater than 14. Hence, the sorted sub-list remains sorted after swapping.

![](img/30fc9e3f8ee01facfae8d1c9621936b3_166_5.png)

By now we have 14 and 27 in the sorted sub-list. Next, it compares 33 with 10.

![](img/30fc9e3f8ee01facfae8d1c9621936b3_166_6.png)

These values are not in a sorted order.

![](img/30fc9e3f8ee01facfae8d1c9621936b3_166_7.png)

So we swap them.

![](img/30fc9e3f8ee01facfae8d1c9621936b3_166_8.png)

However, swapping makes 27 and 10 unsorted.

![](img/30fc9e3f8ee01facfae8d1c9621936b3_166_9.png)

Hence, we swap them too.

![](img/30fc9e3f8ee01facfae8d1c9621936b3_166_10.png)

Again we find 14 and 10 in an unsorted order.
