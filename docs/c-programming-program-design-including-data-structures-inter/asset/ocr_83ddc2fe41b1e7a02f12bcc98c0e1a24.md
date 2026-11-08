The following C++ function implements the previous algorithm:

```
```cpp
template <class elemType>
void insertionSort(elemType list[], int length)
{
    for (int firstOutOfOrder = 1; firstOutOfOrder < length;
                                firstOutOfOrder++)
        if (list[firstOutOfOrder] < list[firstOutOfOrder - 1])
        {
            elemType temp = list[firstOutOfOrder];
            int location = firstOutOfOrder;

            do
            {
                list[location] = list[location - 1];
                location--;
            }
            while (location > 0 && list[location - 1] > temp);

            list[location] = temp;
        }
} //end insertionSort
```
```

We leave it as an exercise for you to write a program to test the insertion sort algorithm. (See Programming Exercise 8 at the end of this chapter.)

> > An insertion sort can also be applied to linked lists. The general algorithm is the same, and the details are left as an exercise for you. See Programming Exercise 9 at the end of this chapter.

# ## Analysis: Insertion Sort

Let L be a list of length n. Suppose L is to be sorted using insertion sort. The for loop executes n − 1 times. In the best case, when the list is already sorted, for each iteration of the for loop, the if statement evaluates to false, so there are n − 1 key comparisons. Thus, in the best case, the number of key comparisons is n − 1 = O(n). Let us consider the worst case. In this case, for each iteration of the for loop, the if statement evaluates to true. Moreover, in the worst case, for each iteration of the for loop, the do...while loop executes firstOutOfOrder − 1 times. It follows that in the worst case, the number of key comparisons is:

1 + 2 + ⋯ + (n − 1) = n(n − 1)/2 = O(n²).

It can be shown that the average number of key comparisons and the average number of item assignments in an insertion sort algorithm are:

(1/4)n² + O(n) = O(n²).