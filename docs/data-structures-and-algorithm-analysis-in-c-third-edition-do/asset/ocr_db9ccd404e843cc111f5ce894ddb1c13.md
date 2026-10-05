242

Chap. 7 Internal Sorting

| 36 | 20 | 17 | 13 | 28 | 14 | 23 | 15 |
|---|---|---|---|---|---|---|---|
| 20 | 36 | 13 | 17 | 28 | 15 | 23 | |
| 13 | 17 | 20 | 36 | 14 | 15 | | 28 |
| | | 13 | 14 | 15 | 17 | 20 | 23 | 28 | 36 |

**Figure 7.8** Illustration of Mergesort. The first row shows eight numbers that are to be sorted. Mergesort will recursively subdivide the list into sublists of one element, then recombine them. The second row shows the four sublists of size 2 created by the first merging pass. The third row shows the two sublists of size 4 created by the next merging pass on the sublists of 2. The last row shows the final list created by merging the two sublists of 3.

Mersort is one of the simplest sorting algorithms conceptually, and has good performance in the asymptotic sense and in empirical running. Surprisingly, even though it is based on a simple concept, it is relatively difficult to implement. Figure 7.8 illustrates Mergesort. A pseudocode sketch of Mergesort as follows:

```
List mergesort(List inlist)
if (inlist.length() <= 1) return inlist;
List1 = half of the items from inlist;
List2 = other half of the items from inlist;
return merge(mergesort(L1), mergesort(L2));
```

Before discussing how to implement Merget, we will first examine the merge function. Merging two sorted sublists is simple. Function merge examines the first element of each sublist and picks the smaller value overall. This smaller value is removed from its sublist and placed into the output list. Merging continues in this way, comparing the front elements of the sublists and continually appending the smaller to the output list until no more elements remain.

Implementing Mergesort presents a number of technical difficulties. The first decision is how to represent the list. Mergesort lends itself to sorting a linked list because merging does not require random access to the elements. Thus, Mergesort is the method of choice when the merge is in the form of a linked list. Implementing mergesort for linked lists is straightforward, because we only need to remove items from the front of the input list and append them to the output list. Breaking the input list into two halves presents some difficulty. Ideally we would just break the list into front and back halves. However, even if we know the length of the list in advance, it would still be necessary to traverse halfway down the linked list to reach the beginning of the second half. A simpler method, which does not rely on knowing the length of the list in advance, assigns elements of the