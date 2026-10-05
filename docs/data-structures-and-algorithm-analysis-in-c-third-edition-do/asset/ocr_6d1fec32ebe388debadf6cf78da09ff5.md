# Sec. 4.2 Stacks

# 125

![](bbox=[0.313, 0.187, 0.703, 0.233])

**Figure 4.20** Two stacks implemented within a single array, both growing toward the middle.

implementation. The only data member is **top**, a pointer to the first (top) link node of the stack. Method **push** first modifies the **next** field of the newly created node to point to the top of the stack and then sets **top** to point to the new link node. Method **pop** is also quite simple. Variable **itemp** stores the top node as it is removed from the stack. The stack is updated by setting **top** to point to the next link in the stack. The old node is returned to free store (or the freelist), and the element value is returned.

# 4.2.3 Comparison of Array-Based and linked Stacks

All operations for the array-based and linked stack implementations take constant time, from a time efficiency perspective, neither has a significant advantage. Another basis for comparison is the total space. The analysis is similar to that for list implementations. The array-based stack must declare a fixed-size array initially, and some of space is wasted whenever the stack is not full. The linked stack can shrink and grow but requires the overhead of a link field for every element.

When multiple stacks are to be implemented, it is possible to take advantage of the one-way growth of the array-based stack. This can be done by using a single array to store two stacks. One stack grows inward from each end as illustrated by Figure 4.20, hopefully leading to wasted space. However, this only works when the space requirements of the two stacks are inversely correlated. In other orders, when one stack grows, the other will shrink. This is particularly effective when elements are taken from one stack and given to the other. If both stacks grow at the same time, then the free space in the middle of the array will be exhausted quickly.

# 4.2.4 Implementing Recursion

The most common computer application that uses stacks is not visible to its users. This is the implementation of subroutine calls in most programming language runtime environments. A subroutine call is normally implemented by placing necessary information about the subroutine (including the return address, parameters, and local variables) onto a stack. This information is called an **activation record**. Further subroutine calls add to the stack. Each return from a subroutine pops the top activation record off the stack. Figure 4.21 illustrates the