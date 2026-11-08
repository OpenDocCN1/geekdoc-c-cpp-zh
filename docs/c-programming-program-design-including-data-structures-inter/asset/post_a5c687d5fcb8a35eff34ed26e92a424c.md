
![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1310_0.png)

**FIGURE 18-33** middle after traversing the list

It is now easy to divide the list into two sublists. First, using the link of middle, we assign a pointer to the node following middle. Then, we set the link of middle to NULL. Figure 18-34 shows the resulting sublists.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1310_1.png)

**FIGURE 18-34** List after dividing it into two lists

This discussion translates into the following C++ function, divideList:

```cpp
template <class Type>
void unorderedLinkedList<Type>::
                 divideList(nodeType<Type>* first1,
                            nodeType<Type>* &first2)
{
    nodeType<Type>* middle;
    nodeType<Type>* current;

    if (first1 == NULL)       //list is empty
        first2 = NULL;
    else if (first1->link == NULL)  //list has only one node
        first2 = NULL;
    else
    {
        middle = first1;
        current = first1->link;

        if (current != NULL)       //list has more than two nodes
            current = current->link;
        while (current != NULL)
```

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1312_0.png)

**FIGURE 18-36** Sublists after setting `newHead` and `lastMerged` and advancing `first1`

In Figure 18-36, `first1` points to the first node of the first sublist that is yet to be merged with the second sublist. So, we again compare the nodes pointed to by `first1` and `first2`, and adjust the link of the smaller node and the last node of the merged list so as to move the smaller node to the end of the merged list. For the sublists shown in Figure 18-36, after adjusting the necessary links, we have Figure 18-37.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1312_1.png)

**FIGURE 18-37** Merged list after putting the node with info 20 at the end of the merged list

We continue this process for the remaining elements of both sublists. Every time we move a node to the merged list, we advance either `first1` or `first2` to the next node. Eventually, either `first1` or `first2` becomes NULL. If `first1` becomes NULL, the first sublist is exhausted first, so we attach the remaining nodes of the second sublist at the end of the partially merged list. If `first2` becomes NULL, the second sublist is exhausted first, so we attach the remaining nodes of the first sublist at the end of the partially merged list.

Following this discussion, we can now write the C++ function `mergeList` to merge the two sorted sublists. The pointers of the first nodes of the sublists are passed as parameters to the function `mergeList`.

```cpp
template <class Type>
nodeType<Type>* unorderedLinkedList<Type>::
                 mergeList(nodeType<Type>* first1,
                           nodeType<Type>* first2)
{
    nodeType<Type> *lastSmall;  //pointer to the last node of
                               //the merged list
    nodeType<Type> *newHead;    //pointer to the merged list

    if (first1 == NULL)        //the first sublist is empty
        return first2;
    else if (first2 == NULL)    //the second sublist is empty
        return first1;
    else
    {
        if (first1->info < first2->info)  //compare the
                                          //first nodes
        {
            newHead = first1;
            first1 = first1->link;
            lastSmall = newHead;
        }
        else
        {
            newHead = first2;
            first2 = first2->link;
            lastSmall = newHead;
        }

        while (first1 != NULL && first2 != NULL)
        {
            if (first1->info < first2->info)
            {
                lastSmall->link = first1;
                lastSmall = lastSmall->link;
                first1 = first1->link;
            }
            else
            {
                lastSmall->link = first2;
                lastSmall = lastSmall->link;
                first2 = first2->link;
            }
        }  //end while

        if (first1 == NULL) //first sublist is exhausted first
            lastSmall->link = first2;
        else                //second sublist is exhausted first
            lastSmall->link = first1;

        return newHead;
    }
} //end mergeList
```

Finally, we write the recursive merge sort function, recMergeSort, which uses the divideList and mergeList functions to sort a list. The pointer of the first node of the list to be sorted is passed as a parameter to the function recMergeSort.

```cpp
template <class Type>
void unorderedLinkedList<Type>::recMergeSort(
                         nodeType<Type>* &head)
{
    nodeType<Type> *otherHead;

    if (head != NULL)    //if the list is not empty
        if (head->link != NULL)    //if the list has more than
                                    //one node
        {
            divideList(head, otherHead);
            recMergeSort(head);
            recMergeSort(otherHead);
            head = mergeList(head, otherHead);
        }
} //end recMergeSort
```

We can now give the definition of the function mergeSort, which should be included as a public member of the class unorderedLinkedList. (Note that the functions `divideList`, `mergeList`, and `recMergeSort` can be included as private members of the class unorderedLinkedList because these functions are used only to implement the function mergeSort.) The function mergeSort calls the function recMergeSort and passes first to this function. It also sets last to point to the last node of the list. The definition of the function mergeSort is:

```cpp
template <class Type>
void unorderedLinkedList<Type>::mergeSort()
{
    recMergeSort(first);

    if (first == NULL)
        last = NULL;
    else
    {
        last = first;
        while (last->link != NULL)
            last = last->link;
    }
} //end mergeSort
```

We leave it as an exercise for you to write a program to test the merge sort algorithm. See Programming Exercise 13 at the end of this chapter.

## Analysis: Merge Sort

Suppose that L is a list of n elements, where n > 0. Suppose that n is a power of 2, that is, n = 2^m for some nonnegative integer m, so that we can divide the list into two sublists, each of size:

n/2 = 2^m/2 = 2^(m−1).

Moreover, each sublist can also be divided into two sublists of the same size. Each call to the function recMergeSort makes two recursive calls to the function recMergeSort, and each call divides the sublist into two sublists of the same size. Suppose that $m = 3$, that is, $n = 2^3 = 8$. So, the length of the original list is 8. The first call to the function `recMergeSort` divides the original list into two sublists, each of size 4. The first call then makes two recursive calls to the function `recMergeSort`. Each of these recursive calls divides each sublist, of size 4, into two sublists, each of size 2. We now have four sublists, each of size 2. The next set of recursive calls divides each sublist, of size 2, into sublists of size 1. So we now have eight sublists, each of size 1. It follows that the exponent 3 in $2^3$ indicates the level of the recursion (see Figure 18-38).

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1315_0.png)

**FIGURE 18-38** Levels of recursion to recMergeSort for a list of length 8

Let us consider the general case when $n = 2^m$. Note that the number of recursion levels is $m$. Also, note that to merge a sorted list of size $s$ with a sorted list of size $t$, the maximum number of comparisons is $s + t - 1$.

Consider the function `mergeList`, which merges two sorted lists into a sorted list. Note that this is where the actual work (comparisons and assignments) is done. The initial call to the function `recMergeSort`, at level 0, produces two sublists, each of the size $n/2$. To merge these two lists, after they are sorted, the maximum number of comparisons is:

$\frac{n}{2} + \frac{n}{2} - 1 = n - 1 = O(n).$

At level 1, we merge two sets of sorted lists, in which each sublist is of the size $n/4$. To merge two sorted sublists, each of the size $n/4$, we need, at most:

$\frac{n}{4} + \frac{n}{4} - 1 = \frac{n}{2} - 1$
