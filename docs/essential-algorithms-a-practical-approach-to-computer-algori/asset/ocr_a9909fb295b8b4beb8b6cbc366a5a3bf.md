Deques are useful in algorithms where you have partial information about the priority of items. For example, you might know that some items are high priority and others are low priority, you might not necessarily know the exact relative priorities of every item. In that case, you can add high-priority items to one end of the deque and low-priority items to the other end of the deque. Deques are easy to build with doubly linked lists.

# Summary

This chapter explained stacks and queues, two data structures that are often used by other algorithms to store items. In a stack, items are added to and then removed from the same “end” of the data structure in last-in-first-out order. In a queue, items are added at one end and removed from the other in first-in-first order.

You can use an array to build a stack fairly easily as long as it doesn't run out of space. If you build a stack with a linked list, you don't need to worry about the stack's running out of space.

You can also use an array to build a queue, although in approach that the items move through the array until they reach the end and you need to resize the array. You can also solve that problem by using a circular array. You can also avoid the issue by using a doubly linked list to build a queue.

You can use stacks and queues to store items in O(N²) although algorithms are more exercises in using stacks and queues in efficient sorting. The next chapter describes several sorting algorithms that give much better performance, with some running in O(N log N) time and others running in O(N) time.

# Exercises

Asterisks indicate particularly difficult problems.

+   1. When you use a double stack, what is the relationship between the variables NextIndex1 and NextIndex2 when one of the stacks is full?
2. Write an algorithm that takes as input a stack and returns a new stack containing the same items but in reverse order.
3. Write a program that implements insertionsort with stacks.
4. For each item, the stack insertionsort moves the unsorted items to the temporary stack. Then it moves all the items back to the original stack. Does it really need to move all the items back to the original stack? Can