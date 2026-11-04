# Bubble Sort Algorithm

The bubble sort algorithm is based on sequential comparisons between adjacent array elements. Each element “bubbles” up and is stored in the proper position. For example, suppose that we want to sort an array in ascending order.

At first, the last element is compared against the last but one. If it is less, the elements are swapped, so the smaller value bubbles up. Then, the last by one element is compared against the last but two. Like before, if it is less, the elements are swapped, so the smaller value keeps bubbling up. The comparisons continue up to the beginning of the array, and eventually the smallest value “bubbles” to the top of the array and it is stored at its first position.

This procedure is repeated from the second element and up to the last one, so the second smallest value of the array bubbles to the top and stored in the second position. The same is repeated for the part of the array from its third element and up to the last one, and so forth. The algorithm terminates when no element bubbles to the top.

To sort the array in descending order, the bubbling value is the greatest and not the smallest one. In the following program, the bubble_sort() function implements the bubble sort algorithm to sort an array in ascending order.

# Exercises

C12.10 Write a function that takes as parameter an array of integers and uses the bubble sort algorithm to sort it in ascending order. Write a program that reads five integers, stores them in an array, and uses the function to sort it.

```
```c
#include <stdio.h>

#define SIZE 5

void bubble_sort(int arr[]);

int main(void)
{
    int i, a[SIZE];
    for(i = 0; i < SIZE; i++)
    {
        printf("Enter number: ");
        scanf("%d", &a[i]);
    }
    bubble_sort(a);
    printf("\n**** Sorted array ****\n");
    for(i = 0; i < SIZE; i++)
        printf("%d\n", a[i]);
    return 0;
}

void bubble_sort(int arr[])
{
```
```