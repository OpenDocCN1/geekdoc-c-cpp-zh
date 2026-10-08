# 13.6. Data Structures

![](bbox=[0.125, 0.085, 0.793, 0.273])

pop (removing the top element). Stacks are useful in algorithms like recursion, expression evaluation, and backtracking.

+   - **Queues**: Linear structures operating on the First In, First Out (FIFO) principle. They have two main operations: enqueue (adding an element to the rear) and dequeue (removing an element from the front). Queues find applications in simulations, scheduling, and graph traversal.

+   - **Lists**: Linear structures composed of elements, each with a data field and a reference to the next element. Unlike arrays, linked lists don't require contiguous memory allocation, enabling dynamic memory management. While insertion and deletion are efficient, accessing elements may be slower compared to arrays.

+   - **Trees**: Hierarchical structures with nodes connected by edges. They have a root node, parent-child relationships, and leaf nodes. Trees are commonly used in organizing hierarchical data, such as file systems and search trees.

+   - **Graphs**: Non-linear structures with vertices (nodes) connected by edges. They can be directed or undirected and are used to represent relationships in various applications like social networks and road networks.

Choosing the right structure is vital for efficient program execution and memory usage, especially for large amounts of data. In this section, we will explore several basic abstract data structures.

# 13.6.1 Linked Lists

A linked list is a way to store data in separate nodes, each containing data and a pointer to the next node. The initial node, known as the head, points to the first node, and the last node, called the tail, has its pointer set to NULL.

Linked lists can change their size dynamically, making them suitable for easily adding or removing elements. They are essential for structures like stacks and queues and are chosen for situations requiring changing sizes.