![](bbox=[0.39, 0.04, 0.69, 0.1])

that an array is completely sorted. Now we should look into some practical aspects of bubble sort.

# ## Algorithm

We assume **list** is an array of **n** elements. We further assume that **swap** function swaps the values of the given array elements.

```
begin BubbleSort(list)
for all elements of list
if list[i] > list[i+1] swap(list[i], list[i+1]) end if
end for
return list end BubbleSort
```

# ## Pseudocode

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

# ## Implementation

One more issue we did not address in our original algorithm and its improvised pseudocode, is that, after every iteration the highest values settles down at the end of the