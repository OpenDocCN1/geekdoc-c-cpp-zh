+   • Formal parameters
+   • Local variables
+   • Return address

This information, collectively, is referred to as a stack frame. The stack frame for each method call will be different. For example, the stack frame for a parameterless or no local variable method will contain just a return address. The compiler will take care of the entire above required stack maintenance when a call to a recursive method is made.

The following strategy can be used to remove the recursion from a recursive routine, although not elegantly. There might be a far more pleasing method for a particular routine, but this technique is very instructional. It allows one to simulate the stack by deciding user's own stack structure and manage the recursion. This is accomplished as follows:

+   i. Each time a recursive call is made in the algorithm, push the necessary information onto the stack.
+   ii. When the process is completed at this deeper level, pop the simulated stack frame and continue processing in the higher level at the point indicated by the return address popped from the stack.
+   iii. Use an iterative control structure that loops until there are no return addresses left to pop from the stack.

```
Algorithm 6.7: FACT (n)
1. If (n==0) then set fact=1 and return
2. else p=n-1
3. q=fact (p)
4. fact=*q;
5. End
```

The use of the stack in performing recursion is explained through a simple recursive program. Consider the recursive program for a factorial as shown in Figure 6.8.

Examine the recursive call in Step 3. To avoid an endless series of calls to fact(), a base case n=0 is used in Step 1. The function fact() (a calling itself) is based on the value of n. The function fact() has normal termination only when the base case is executed or recursive calls have successfully ended.

While executing, to maintain the record of values of parameters and to keep track of calls made by itself, the stack is used.

![](bbox=[0.15, 0.65, 0.9, 0.95])