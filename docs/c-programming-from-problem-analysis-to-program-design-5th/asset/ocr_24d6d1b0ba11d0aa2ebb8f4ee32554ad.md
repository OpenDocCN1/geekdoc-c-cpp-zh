![](bbox=[0.182, 0.107, 0.912, 0.633])

**FIGURE 17-1** Execution of `fact(4)`

The output of the previous cout statement is:

24

In Figure 17–1, the down arrow represents the successive calls to the function `fact`, and the upward arrows represent the values returned to the caller, that is, the calling function.

Let us note the following from the preceding example, involving the factorial function.

+   - Logically, you can think of a recursive function as having an unlimited number of copies of itself.
+   - Every call to a recursive function—that is, every recursive call—has its own code and its own set of parameters and local variables.