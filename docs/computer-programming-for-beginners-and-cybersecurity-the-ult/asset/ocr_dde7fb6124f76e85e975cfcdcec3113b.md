![](bbox=[0.126, 0.094, 0.201, 0.181])

It can be helpful to walk through the code manually on a few trees, so you can see it much clearer.

Deleting from trees is a great example of a recursive algorithm that’s not easy to do as an iterative implementation. First, you need a loop that can deal with both sides of the tree at the same time. You need to be able to delete a subtree while simultaneously tracking the next one, and that needs to be done for every level. With the stack, you can keep your place much more easily. The best way of visualizing this is to say that each stack frame will store the tree branch that has been deleted or destroyed already:

```
destroy_tree( )
```

destroy_tree( ) — knows whether the subtree was the left or right

Each of the stack frames knows which bits of the tree have to be destroyed because it knows what point in the function execution should continue. When the first call to destroy the tree is made, the program is notified by the stack frame to continue executing when the second call is made to destroy_tree. When that second call is made, the program is told to continue with the delete tree. Because every function has a stack frame of its own, it can track the entire state of the tree’s destruction at the current time, one tree level at a time.

To implement this in a non-recursive way would require having a data structure that retains the same amount and type of information. You could, for example, write a function that holds a linked list as a way of simulating the list. That linked list would have subtrees that were being destroyed and trees left for destruction. Then a loop-based algorithm could be written to add the subtrees to the list and remove them after they were destroyed fully. Basically, recursion lets