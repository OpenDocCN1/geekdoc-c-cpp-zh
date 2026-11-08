```
~~~cpp
template <class elemType>
int partition(elemType list[], int first, int last)
{
    elemType pivot;

    int index, smallIndex;

    swap(list, first, (first + last) / 2);

    pivot = list[first];
    smallIndex = first;

    for (index = first + 1; index <= last; index++)
        if (list[index] < pivot)
        {
            smallIndex++;
            swap(list, smallIndex, index);
        }

    swap(list, first, smallIndex);

    return smallIndex;
} //end partition
~~~
```

Note that the formal parameters first and last specify the starting and ending indices, respectively, of the sublist of the list to be partitioned. If first = 0 and last = length - 1, the entire list is partitioned.

As you can see from the definition of the function partition, certain elements of the list need to be swapped. The following function, swap, accomplishes this task. (Notice that this swap function is the same as the one given earlier in this chapter for the selection sort algorithm.)

```
~~~cpp
template <class elemType>
void swap(elemType list[], int first, int second)
{
    elemType temp;

    temp = list[first];
    list[first] = list[second];
    list[second] = temp;
} //end swap
~~~
```

Once the list is partitioned into lowerSublist and upperSublist, we again apply the quick sort function to sort the two sublists. Because both sublists are sorted using the same quick sort algorithm, the easiest way to implement this algorithm is to use recursion. Therefore, this section gives the recursive version of the quick sort algorithm. As explained previously, after rearranging the elements of the list, the function partition returns the index of pivot so that the starting and ending indices of the sublists can be determined.