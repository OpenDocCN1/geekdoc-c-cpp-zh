
Deques are useful in algorithms where you have partial information about the priority of items. For example, you might know that some items are high priority and others are low priority, you might not necessarily know the exact relative priorities of every item. In that case, you can add high-priority items to one end of the deque and low-priority items to the other end of the deque. Deques are easy to build with doubly linked lists.

# Summary

This chapter explained stacks and queues, two data structures that are often used by other algorithms to store items. In a stack, items are added to and then removed from the same “end” of the data structure in last-in-first-out order. In a queue, items are added at one end and removed from the other in first-in-first-order.

You can use an array to build a stack fairly easily as long as it doesn't run out of space. If you build a stack with a linked list, you don't need to worry about the stack's running out of space.

You can also use an array to build a queue, although in that approach that the items move through the array until they reach the end and you need to resize the array. You can also solve that problem by using a circular array. You can also avoid the issue by using a doubly linked list to build a queue.

You can use stacks and queues to store items in O(N^2) although algorithms are more exercises in using stacks and queues in efficient sorting. The next chapter describes several sorting algorithms that give much better performance, with some running in O(N \log N) time and others running in O(N) time.

# Exercises

Asterisks indicate particularly difficult problems.

- + 1. When you use a double stack, what is the relationship between the variables NextIndex1 and NextIndex2 when one of the stacks is full?
- 2. Write an algorithm that takes as input a stack and returns a new stack containing the same items but in reverse order.
- 3. Write a program that implements insertionsort with stacks.
- 4. For each item, the stack insertionsort moves the unsorted items to the temporary stack. Then it moves all the items back to the original stack. Does it really need to move all the items back to the original stack? Can you improve the algorithm's performance by modifying that step? What does that do to the algorithm's Big O run time?
- + 5. What does the stack insertionsort algorithm mean in terms of train sorting?
- + 6. Write a program that implements selectionsort with stacks.
- + 7. What does the stack selectionsort algorithm mean in terms of train sorting?
- + 8. Write a program that implements a priority queue.
- + 9. Write a program that implements a deque.
- + 10. Consider a bank where customers enter a single line that is served by several tellers. You enter the line at the end, and when you go to the front of the line, you are served by the next available teller. You can model this “multiheaded queue” with a normal queue that serves multiple tellers. Make a program similar to the one shown in Figure 5-11 to simulate a multiheaded queue in a bank. Use the controls to adjust the number of tellers, the amount of time between customer arrivals, the amount of time each customer stays, and the speed of the simulation. After the user specifies parameters, run a simulation to see how the queue behaves. How does the number of tellers affect the wait time?

![](img/fefa42765c0b410af6705110aea7c0cb_152_0.png)

**Figure 5-11:** In a bank queue, customers stand in a single line and then are helped by the next available teller.

- + 11. Write a program that implements insertionsort with queues.
- + 12. Write a program that implements selectionsort with queues.

# CHAPTER 6 ## Sorting

There are several reasons why sorting algorithms are usually covered in great detail in algorithms books. First, they are interesting and demonstrate several useful techniques, such as recursion, problem subdivision, heaps, and trees.

Second, sorting algorithms are well studied and are some of the few algorithms for which exact run times are known. It can be shown that the fastest possible algorithm that uses comparisons to sort N items must use O(N \log N) time. Several sorting algorithms actually achieve that performance, in some sense they are optimal.

Finally, sorting algorithms are useful. Almost any data is useful when it is sorted in various ways, so sorting algorithms play an important role in many applications.

This chapter describes several different sorting algorithms. Some, such as insertionort, selectionsort, and bubblesort, are relatively simple but slow. Others, such as heapsort, quicksort, and mergesort, are more complicated but much faster. Still others, such as countsort, don't use comparisons to sort items, so they can break the O(N \log N) restriction and perform amazingly fast under the right circumstances.

The following sections categorize the algorithms by their run time performance.

> NOTE Many programming libraries include sorting tools, and they are usually quite fast. In practice, you may want to use those tools to save time writing and debugging the code. It is still important to understand how sorting algorithms work, however, because sometimes you can do better than the built-in tools. For example, a simple bubblesort algorithm may beat a more complicated library runtime or countsort often beats the tools if the data being sorted has certain characteristics.

## O(N²) Algorithms

O(N^2) algorithms are relatively slow but fairly simple. In fact, their simplicity sometimes lets them outperform faster than more complicated algorithms for very small arrays.

### Insertionsort in Arrays

Chapter 3 describes insertionsort with linked lists, and Chapter 4 describes insertionsort with stacks and queues. The basic idea is to take an item from the input and insert it into the sorted part. The following pseudocode shows:

```
Insertort(values[])
  For i = 0 To length of values
    // Find the first index j where values[j] > values[i]
    // Move the items between j and i one to the right to make room for the item at position j
    // Insert values[i] at j
```

As i goes through the array, the code moves the items that have been sorted to the right to make room for the item at position j. This can be a time-consuming step. Suppose the item's new index should be j. Figure 6-1 shows the algorithm's key steps. The image at the top shows the unsorted array. In the middle image, the first four items (outlined in bold) have been sorted, and the algorithm is preparing to insert the next item (which has value 3) into the sorted of of the array. the the of of the,, the has moved 5, 6, and 7 to the right to make room for value 3. The algorithm inserts 33 continues the the loop to insert the next item (which has value 2) into its correct position.

![](img/fefa42765c0b410af6705110aea7c0cb_156_0.png)

**Figure 6-1:** Insertion sort inserts items into the sorted part of the array.

This algorithm sorts the items in the original array (aside from a few variables to control loops and move items), so it doesn't need any additional storage. If the array contains N items, the algorithm considers each of the N positions in the array. For each position i, it must search the previously sorted items in the array to find the $i$th item's new position. It must then move the items between location and index one to the right. If the item should be moved to position $j$, it takes $j$ steps to find the new location $j$ and $i - j$ steps to move items over, resulting in a total of $i$ steps. That means in total it takes $i$ steps to move item into its new position. Adding up the steps required to position all items, the total run time is

$1 + 2 + 3 + \dots + N = (N^2 + N) / 2$

This means the algorithm has run time $O(N^2)$. This isn't a very fast run time, but it's fast enough for reasonably small arrays (fewer than 10,000 or so items). It's also a relatively simple algorithm, so it may sometimes be faster than more complicated algorithms for very small arrays. How small an array must be
