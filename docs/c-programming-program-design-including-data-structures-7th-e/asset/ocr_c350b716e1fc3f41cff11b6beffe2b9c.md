Figure 8–11 shows the elements of list during the second iteration.

Now the unsorted list is list[1]...list[7]. So, we find the smallest element in the unsorted list. The smallest element is at position 3, as shown in Figure 8–11(a). Because the smallest element in the unsorted list is at position 3, it must be moved to position 1. So, we swap 7 (that is, list[3]) with 30 (that is, list[1]), as shown in Figure 8–11(b). After swapping 7 (that is, list[3]) with 30, the resulting list is as shown in Figure 8–11(c).

Now, the unsorted list is list[2]...list[7]. So, we repeat the preceding process of finding the (position of the) smallest element in the unsorted portion of the list and moving it to the beginning of the unsorted portion of the list. Selection sort thus involves the following steps.

+   In the unsorted portion of the list:
+   
+   a. Find the location of the smallest element.
+   
+   b. Move the smallest element to the beginning of the unsorted list.

Initially, the entire list (that is, list[0]...list[length − 1]) is the unsorted list. After executing Steps a and b once, the unsorted list is list[1]...list[length − 1]. After executing Steps a and b a second time, the unsorted list is list[2]...list[length − 1], and so on. In this way, we can keep track of the unsorted portion of the list and repeat Steps a and b with the help of a for loop, as shown in the following pseudocode:

```
for (index = 0; index < length − 1; index++)
{
    a. Find the location, smallestIndex, of the smallest element in
       list[index]...list[length − 1].
    b. Swap the smallest element with list[index]. That is, swap
       list[smallestIndex] with list[index].
}
```

The first time through the loop, we locate the smallest element in list[0]...list[length − 1] and swap the smallest element with list[0]. The second time through the loop, we locate the smallest element in list[1]...list[length − 1] and swap the smallest element with list[1], and so on.

Step a is similar to the algorithm for finding the index of the largest item in the list, as discussed earlier in this chapter. (Also see Programming Exercise 2a at the end of this chapter.) Here, we find the index of the smallest item in the list. The general form of Step a is:

```
smallestIndex = index;    //assume first element is the smallest

for (location = index + 1; location < length; location++)
    if (list[location] < list[smallestIndex])
        smallestIndex = location;    //current element in the list
                                      //is smaller than the smallest so
                                      //far, so update smallestIndex
```

Step b swaps the contents of list[smallestIndex] with list[index]. The following statements accomplish this task: