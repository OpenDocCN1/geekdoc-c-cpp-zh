At this point, we have reached the base case for fact, and so the recursion begins to unwind. Each return from fact involves popping the stored value for n from the stack, along with the return address from the function call. The return value for fact is multiplied by the restored value for n, and the result is returned.

Because an activation record must be created and placed onto the stack for each subroutine call, making subroutine calls is a relatively expensive operation. While recursion is often used to make implementation easy and clear, sometimes you might want to eliminate the overhead imposed by the recursive function calls. In some cases, such as the factorial function of Section 2.5, recursion can easily be replaced by iteration.

# Example 4.2 As a simple example of replacing recursion with a stack, consider the following non-recursive version of the factorial function.

```
long fact(int n, Stack<int>& S) { // Compute n!
    // To fit n! in a long variable, require n <= 12
    Assert((n >= 0) && (n <= 12), "Input out of range");
    while (n > 1) S.push(n--);  // Load up the stack
    long result = 1;           // Holds final result
    while(S.length() > 0)
        result = result * S.pop();  // Compute
    return result;
}
```

Here, we simply push successively smaller values of n onto the stack until the base case is reached, then repeatedly pop off the stored values and multiply them into the result.

An iterative form of the factorial function is both simpler and faster than the version shown in Example 4.2. But it is not always possible to replace recursion with iteration. Recursion, or some imitation of it, is necessary when implementing algorithms that require multiple branching such as in the Towers of Hanoi algorithm, or when traversing a binary tree. The Mergesort and Quicksort algorithms of Chapter 7 are also examples in which recursion is required. Fortunately, it is always possible to imitate recursion with a stack. Let us now turn to a non-recursive version of the Towers of Hanoi function, which cannot be done iteratively.

# Example 4.3 The TOH function shown in Figure 2.2 makes two recursive calls: one to move n − 1 rings off the bottom ring, and another to move these n − 1 rings back to the goal pole. We can eliminate the recursion by using a stack to store a representation of the three operations that TOH must perform: two recursive calls and a move operation. To do so, we must first come up with a representation of the various operations, implemented as a class whose objects will be stored on the stack.