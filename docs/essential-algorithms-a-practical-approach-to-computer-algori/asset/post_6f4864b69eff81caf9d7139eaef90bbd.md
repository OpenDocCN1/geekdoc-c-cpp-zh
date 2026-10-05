
# Appendix A Summary of Algorithmic Concepts 479

## Chapter 4: Arrays

Array is a contiguous piece of memory that holds items.
Array packing—You can pack items into a piece of memory by mapping array indices to memory locations. For example, to save space you may need a triangular array by mapping indices in the triangular array into a one-dimensional array. Similarly, you can make arrays with nonzero lower bounds by mapping the bounds to a regular zero-based array.

Sparse arrays—You can use linked structures to build space-efficient sparse arrays or matrices.

## Chapter 5: Stacks and Queues

A stack is a data structure that provides last-in-first-out(LIFO) access to items. You can implement a stack in a linked list or array, although you may need to resize the array if it becomes full.
- queue is a data structure that provides first-in-first-out (FIFO) access to items. You can implement a stack in a linked list or circular array, although you may need to resize the array if it becomes full.
- priority queue, items are retrieved in priority order.
Pronounced “deck,” a deque is a queue that allows you to add or remove items from either end.
- Uses—Other algorithms use stacks and queues to hold items while they are being processed.

## Chapter 6: Sorting

Insertion—As in insertionsort, the algorithm takes an item and inserts it into the correct position in some data structure.
- Selection—As in selectsort, the algorithm examines the items that have not yet been processed, finds the best one at that moment, and adds it to some data structure.
- Decreasing range—As in bubblesort, the algorithm keeps track of the range of interest and restricts that range over time to reduce the number of items it must consider.
- A heap is a tree in which every node has value at least as large as its children's values. A heap can be used as a priority queue.
- Storing a complete tree—An algorithm can store a complete tree in an array.
Divide and conquer—An algorithm breaks the problem into smaller pieces and solves the pieces, usually recursively.
- Randomization—Quicksort can use randomization to reduce worst-case behavior because of items initially in a particular order. (This doesn't protect it if there are many duplicate items.)
Parallelization—Quicksort, mergesort, and bucketsort can be parallelized.
External sorting—Because it moves through memory, mergesort performs external sorting well.

Counting—If items have a limited range, you may be able to count them instead of sorting them as countsort.

Partitioning—Bucketsort partitions items into buckets to simplify the problem.
Picking the right algorithm—Sorting algorithms provide a good example of when it is important to pick the right algorithm for the problem. Picking the right algorithm can mean the difference between solving a problem in seconds, minutes, or years.

## Chapter 7: Searching

A linear (exhaustive) search loops through all the possible items, looking for a target, giving it O(n) runtime. If the list is sorted, the algorithm can stop early if it passes the point where the item would be.

A binary search divides in half the area to be searched at each step, giving O(log n) runtime. This concept applies to many problems.

An interpolation search uses interpolation to guess where a target item is, giving it O(log n) runtime.

## Chapter 8: Hash Tables

Hashing requirements—Hashing requires a data structure to hold values, a hashing function to map values to the data structure, and a collision resolution policy.

Mapping—Hash tables use a hashing function to map values from one domain (names, employee IDs) to another domain (indices in an array). A good hashing function maps any input to a random distribution of output values.

Chaining—Using linked lists to hold bucket overflow.

Sorted counting—Sorting the linked lists improves performance in many algorithms.

Opening addressing—Mapping directly to arrays.
Marking items as deleted—Many data structures cannot easily remove items. Instead, you may be able to mark items as deleted and then reuse their spots later.

Clustering—In some algorithms, such as linear and quadratic probing, the probability of an item's landing in different places may not be equal. This can reduce the algorithm's efficiency.

Randomization—By randomizing data, you can sometimes avoid bad consequences.
Double hashing uses a second hash function to avoid clustering.

## Chapter 9: Recursion

Recursive metrics—For recursive algorithms, in addition to studying runtime and memory requirements, you must consider maximum depth of recursion and use of stack space.

Recursive approach—Recursive algorithm calls itself to solve a smaller problem. When the recursive calls reach a point where the problem is small enough, the algorithm solves it without recursion and returns to the calling instance.

Recursive definitions—Some sequences, such as the factorial and Fibonacci numbers, have natural recursive definitions. These lead easily to recursive algorithms, although they are not as efficient as nonrecursive algorithms.

Self-similar fractals are curves that start with an initiator and then recursively replace parts of the curve with a suitably scaled, rotated, and translated generator curve.

Backtracking is a recursive algorithm that considers partial solutions. If it finds a partial solution that cannot be extended to a full solution, the algorithm discards the partial solution, backtracks to the previous feasible solution, and continues searching from there.

A selection is an unordered subset of set of objects. The number of selections without duplicates of k items taken from a total of n items is given by this equation:

$$\binom{n}{k} = \frac{n!}{k!(n-k)!}$$

Tail recursion removal—You can replace tail recursion with a loop that resets parameters before the end of the loop.

Storing intermediate values—If a calculation such as the Fibonacci numbers recalculate the same values many times, you can save time by storing values in a lookup table so you can calculate them only once.

General recursion removal—You can remove recursion more generally by mimicking how a program calls a method recursively. Push variables onto stacks before recursion, and pop them off afterwards.

## Chapter 10: Trees

Many algorithms use trees, it's important to remember at least the most basic tree properties.

Logarithmic growth—If a tree is reasonably balanced

Lots of leaves—If a tree is reasonably balanced, roughly half its nodes are leaves.

Inductive reasoning—Proof by induction is a useful technique for proving tree theorems.

Branches and object references—You can use object references or pointers to link a node to its children. You can use similar references to create threads through trees. You also can use similar references to build networks.

Traversals—Preorder, inorder, postorder, and breadth-first traversals process the nodes in different orders.
Sorted trees—A sorted tree arranges its nodes so that they are processed in order.
Threads—You can use special branches or links to visit the tree or network in unusual orders. A data structure can have as many threads as you find, although maintaining threads requires extra work.
Knowledge trees—The animal game uses a knowledge tree to represent questions and the results that answer them.
Expressions can be represented and evaluated as trees.
Quadtrees and octrees divide two- or three-dimensional space to make locating objects

## Chapter 11: Balanced Trees

Amortized operations—Sometimes you can do little extra work during common operations such as rebalancing a tree when you add or remove a value.
AVL trees use rotations to rebalance the tree, the heights of the subtrees at any node differ by most 1.
2-3 trees—Every internal node has either two or three children. If a node has three children and you add one, it splits into two nodes with children. If a node has two children and you remove one of them, the node rearranges with a sibling node or merges with a value in place.
Btrees—Every node holds between K and 2 K values, where K is the tree's order. A node holding M values has M + 1 children. B-trees are a generalization of 2-3 trees and use similar splitting and merging.
Top-down B—When moving down into the tree to add a value, the algorithm splits any full nodes it encounters so that there is room if needed. This is another example of an amortized operation in which the algorithm does some extra work to make later operations easier.

## Chapter 12: Decision Trees

You can model many problems with decision trees. A branch in a decision tree represents a single decision.
Game trees are a special kind of decision tree. A minimax strategy lets you minimize your opponent's board position. Game tree heuristics include precomputed initial moves and responses, looking for patterns, and numeric board locations (that may change over time).
