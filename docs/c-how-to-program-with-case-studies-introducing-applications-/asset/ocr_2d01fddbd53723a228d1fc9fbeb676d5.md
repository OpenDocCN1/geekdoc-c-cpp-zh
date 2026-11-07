![](bbox=[0.145, 0.083, 0.855, 0.339])

Note that the rightmost leaf node appears at the top of the output in the rightmost column, and the root node appears at the left of the output. Each column of output starts five spaces to the right of the previous column. Function outputTree should receive as arguments a pointer to the tree’s root node and an integer totalSpaces representing the number of spaces preceding the value to output. This variable should start at zero so that the root node is output at the left of the screen. The function uses a modified inorder traversal to output the tree. The algorithm is as follows:

```
While the pointer to the current node is not NULL,
    Recursively call outputTree with the current node’s right subtree and
        totalSpaces + 5.
    Use a for statement to count from 1 to totalSpaces and output spaces.
    Output the value in the current node.
    Recursively call outputTree with the current node’s left subtree and
        totalSpaces + 5.
```

# Special Section: Systems Software Case Study—Building Your Own Compiler

In Exercise 7.28, we introduced the made-up Simpleton Machine Language (SML). In Exercise 7.29, you used simulation to create the Simpleton computer—a virtual machine—to execute programs written in SML. In this challenge section, you’ll build a compiler that converts programs written in Simple—a made-up, concise, high-level programming language—to SML. This section “ties” together key pieces of the programming process. You’ll:

+   - **write** several Simple high-level language programs,
+   - **compile** the programs using the compiler you’ll build, generating SML machine-language code into a file,