+   - *Peek or Front* — Like in the stack, this function returns the value of the first element without deleting it.

Other supported functions include returning the size of the queue and checking whether the list is empty or full. The operating system of a computer uses queues for handling print jobs and servicing interrupts. The job that is scheduled first for printing is also printed first. An interrupt that is received first is also serviced first.

> **Takeaway:** The *pop* operation in a stack deletes the last element that was pushed. In contrast, the *dequeue* operation in a queue deletes the *first* element that was queued.

> **Note:** All programs that insert or delete elements in a stack or queue must first check whether the data structure is full or empty.

# 16.16.3 The Tree

Unlike a stack or queue which are linear data structures, a *tree* is a non-linear one. Elements in a tree are organized in a hierarchical manner, much like the file system used by MS DOS/Windows and UNIX/Linux systems. Thus, every tree has a single *root* node at the top from where multiple nodes emanate. Each of these nodes in turn generate further nodes and so on until the bottom of the tree is reached (Fig. 16.9). Nodes in trees have *levels*; the root node is at level 0.

Like with the file system, nodes have a *parent-child* relationship between them. However, the root node has no parent and the terminating nodes—also called *leaves*—have no children. All children having a common parent are known as *siblings* who are connected to their parent by pointers in the parent node.

![](bbox=[0.219, 0.594, 0.782, 0.855])

**FIGURE 16.9** An Ordered Binary Tree