[https://www.sitesbay.com/data-structure/c-stack-example](https://www.sitesbay.com/data-structure/c-stack-example)

# 5.1.5 Binary Tree | Set 1 (Introduction)

**Trees:** Unlike Arrays, Linked Lists, Stack and queues, which are linear data structures, trees are hierarchical data structures.

**Tree Vocabulary:** The topmost node is called root of the tree. The elements that are directly under an element are called its children. The element directly above something is called its parent. For example, a is a child of f and f is the parent of a. Finally, elements with no children are called leaves.

```
tree
----
  j  <-- root
 / \\
 f   k
/ \\   \\
a  h   z  <-- leaves
```

# Why Trees?

+   1. One reason to use trees might be because you want to store information that naturally forms a hierarchy. For example, the file system on a computer:

```
file system
-----------
    /   <-- root
   / \\
 ...  home
      /   \\
   ugrad  course
      /    /  |  \\
    ...  cs101 cs112 cs113
```

+   2. Trees (with some ordering e.g., BST) provide moderate access/search (quicker than Linked List and slower than arrays).
+   3. Trees provide moderate insertion/deletion (quicker than Arrays and slower than Unordered Linked Lists).