Figure 15 shows the algorithm in action.

+   1. Extract the root node value.
+   2. Move the value of the last node of the heap into the root node, and remove the last node. Now the heap property may be violated for the root node, because one or both of its children may be larger.
+   3. Promote the larger child of the root node. (See Figure 15 continued.) Now the root node again fulfills the heap property. Repeat this process with the demoted child. That is, promote the larger of its children. Continue until the demoted child has no larger children. The heap property is now fulfilled again. This process is called “fixing the heap”.

![](bbox=[0.245, 0.317, 0.891, 0.812])

**Figure 15** Removing the Maximum Element from a Heap