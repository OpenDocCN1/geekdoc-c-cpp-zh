![](bbox=[0.18, 0.09, 0.85, 0.28])

![](bbox=[0.18, 0.32, 0.88, 0.62])

# Figure 12.18 Example of the Deutsch-Schorr-Waite garbage collection algorithm. (a) The initial multilist structure. (b) The multilist structure of (a) at the instant when link node 5 is being processed by the garbage collection algorithm. A chain of pointers stretching from variable prev to the head node of the structure has been (temporarily) created by the garbage collection algorithm.

Fortunately, a clever technique allows DFS to be performed without requiring additional space for a stack. Instead, the structure being traversed is used to hold the stack. At each step deeper into the traversal, instead of storing a pointer on the stack, we “borrow” the pointer being followed. This pointer is set to point back to the node we just came from in the previous step, as illustrated by Figure 12.18. Each borrowed pointer stores an additional bit to tell us whether we came down the left branch or the right branch of the link node being pointed to. At any given instant we have passed down only one path from the root, and we can follow the trail of pointers back up. As we return (equivalent to popping the recursion stack), we set the pointer back to its original position so as to return the structure to its original condition. This is known as the Deutsch-Schorr-Waite garbage collection algorithm.

# 12.4 Further Reading

For information on LISP, see The Little LISPer by Friedman and Felleisen [FF89]. Another good LISP reference is Common LISP: The Language by Guy L. Steele [Ste90]. For information on Emacs, which is both an excellent text editor and a programming environment, see the GNU Emacs Manual by Richard Stallman