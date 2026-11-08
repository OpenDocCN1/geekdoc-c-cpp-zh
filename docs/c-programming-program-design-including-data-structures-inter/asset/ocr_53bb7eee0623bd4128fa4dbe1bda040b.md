![](bbox=[0.118, 0.094, 0.813, 0.257])

**FIGURE 18-36** Sublists after setting `newHead` and `lastMerged` and advancing `first1`

In Figure 18-36, `first1` points to the first node of the first sublist that is yet to be merged with the second sublist. So, we again compare the nodes pointed to by `first1` and `first2`, and adjust the link of the smaller node and the last node of the merged list so as to move the smaller node to the end of the merged list. For the sublists shown in Figure 18-36, after adjusting the necessary links, we have Figure 18-37.

![](bbox=[0.274, 0.466, 0.789, 0.632])

**FIGURE 18-37** Merged list after putting the node with info 20 at the end of the merged list

We continue this process for the remaining elements of both sublists. Every time we move a node to the merged list, we advance either `first1` or `first2` to the next node. Eventually, either `first1` or `first2` becomes NULL. If `first1` becomes NULL, the first sublist is exhausted first, so we attach the remaining nodes of the second sublist at the end of the partially merged list. If `first2` becomes NULL, the second sublist is exhausted first, so we attach the remaining nodes of the first sublist at the end of the partially merged list.

Following this discussion, we can now write the C++ function `mergeList` to merge the two sorted sublists. The pointers of the first nodes of the sublists are passed as parameters to the function `mergeList`.

```
```cpp
template <class Type>
nodeType<Type>* unorderedLinkedList<Type>::
                 mergeList(nodeType<Type>* first1,
                           nodeType<Type>* first2)
```
```