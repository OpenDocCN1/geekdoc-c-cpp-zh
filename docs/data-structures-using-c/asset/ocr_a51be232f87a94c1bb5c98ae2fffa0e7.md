# 12.7.2 Operations on Fibonacci Heaps

There are various operations of binomial heaps. They are as follows:

+   1. CreateFHeap—Creates an empty Fibonacci Heap, that is, simply allocates and returns an object H, where min[H]=null
+   2. FindMinimumKey—Returns min[H], a pointer to the node with the minimum key in an n-node Fibonacci heap H
+   3. UnitingTwoFHeap—Takes the union of the two Fibonacci heaps
+   4. InsertNode—Inserts a node into Fibonacci heap H
+   5. ExtractMinimumKeyNode—Extracts the node with minimum key from Fibonacci heap H and returns the pointer to the extracted node
+   6. DecreaseKey—Decreases the key of a node in a Fibonacci heap H to a new value k.
+   7. DeleteKey—Deletes the specified key from Fibonacci heap H.

# RECAPITULATION

+   * A complete or nearly complete binary tree where each node is greater or equal to its children with each subtree satisfying this property is called as heap.
+   * The basic operations on heap are insert, delete, reheapUp, and reheapDown.
+   * Heap can be implemented using an array as it is a complete binary tree. It is easy to maintain fixed relationship between a node and its children.
+   * Among many applications of heap, the key ones are priority queue, sorting, and selection.

+   * Priority queue is implemented using heap by maintaining its relationship of element with other members in a list.
+   * One of the popular sorting techniques is heap sort that uses heaps.
+   * The heap is popularly used in applications where at each stage, the largest element is to be picked up for processing known as selection problem.

# KEY TERMS

+   **Delete from heap** A key can be deleted from a heap if it is the root value. After deletion, the heap without root is repaired by the reheapDown operation. The last node key is placed at the root and then reheapDown operation places it at the proper location.
+   **Heap** A heap is a complete binary tree (or nearly complete binary tree) having the key in a node greater than the key in its entire subtree. Each subtree is also a heap.
+   **Insert into heap** A new key can be inserted into a heap. Initially, a new key is inserted by locating

+   the first empty leaf location in an array, and the reheapUp operation places it in a proper location in the heap.
+   **ReheapDown** When a key is pushed down the heap, the reheapDown operation ensures that it is less than its children (may be one or more), and if it is, exchanges it with larger key.
+   **ReheapUp** A broken heap is repaired using the reheapUp operation by floating the last element up the tree until it reaches its correct location in the heap.