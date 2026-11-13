+   17. set_data, set_link, list_insert, list_locate, list_remove, and list_search functions should not be used in the stack class, because only the top item of the stack can be accessed.

+   18. Our size implementation calls list_size, which is linear time. For a constant time implementation, you could maintain another private member variable to continually keep track of the list length. This variable would be updated each time an item is pushed or popped, and the size function can simply return the current value of this variable.

+   19. See the discussion of the Koenig lookup on page 374.

+   20. 42

+   21. There is no need for a second stack of operation symbols, because each operation is used as soon as it is read.

+   22. Prefix: + * 7 3 2 Postfix: 7 3 + 2 *

+   23. The trace is the same as the computation at the bottom of Figure 7.10 on page 380, except that the numbers are three times as large.

+   24. The trace is much the same as the computation in Figure 7.13 on page 386, except that the operations are different.

# PROGRAMMING PROJECTS

For more in-depth projects, please see www.cs.colorado.edu/~main/projects/

+   1. In our first case study on evaluating arithmetic expressions we used two stacks that held different types of data. In two other applications, we might need two stacks with the same type of data. If we implement the stacks as arrays, there is a chance that one array (and hence one stack) becomes filled, causing our computation to end prematurely. This might be a shame, since the other array (stack) might have plenty of room. One way around this problem is to implement two stacks as one large array rather than two smaller arrays. Write a class for a pair of stacks. A pair of stacks is simply an object with two stacks. Call these stacks StackA and StackB. There should be separate operations for each stack, for example, pop_a and pop_b. Implement the stack pair as a single array. The two stacks grow from the two ends of the array, so for example, one stack could fill up one quarter of the array while the other fills up three quarters.

+   2. The top member function of the STL stack returns a reference to the top item. This is similar to the way that our node class from Chapter 6 has a data function that returns a reference to the item in the node (see page 323). For this project, modify both of the stack implementations

+   from Section 7.3 so that the top function returns a reference to the top item. With this modification, the prototype of the top function changes:

```
Item& top ();
```

Note that top is no longer a const function because its return value can now be used to change the top item on a stack. For example, if s is a non-empty stack of integers, we can change the top item to 42 by the assignment:

```
s.top() = 42;
```

In the case of the Chapter 6 node class, we fixed this problem by adding a second version of the data function, and this second version is a const member function (see page 325). Your solutions for this project should do a similar thing for the stack implementations, also providing a const version of the top function with this prototype:

```
const Item& top() const;
```

This prototype indicates that the return value is a reference to a constant item (and therefore it cannot be used to change the stack). Since the stack cannot be changed, this version of the top function is now a const member function.