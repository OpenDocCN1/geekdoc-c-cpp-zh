

### Table 10.7 (Continued)

| Data inserted | AVL tree after insertion of BF | Rotation performed | Rebalanced AVL tree |
|---|---|---|---|
| 22 | Tree diagram: Root 31 (BF 2), Left child 23 (BF 1) with left child 22. Right child 32. Node 30 (BF 2) inside dashed box. | LL | Tree diagram: Root 31 (BF 1). Left child 23 (BF 0) with children 22 and 30. Right child 32 (BF 0). |
| 28 | Tree diagram: Root 31 (BF 2). Left child 23 (BF -1) with left child 22 and right child 30 (BF 1) containing 28. Right child 32. | LR | Tree diagram: Root 30 (BF 0). Left child 23 (BF 0) with children 22 and 28. Right child 31 (BF -1) with right child 32. |
| 24 | Tree diagram: Root 31 (-1). Left child 23 (-1) with children 22 and 28 (containing 24). Right child 31 (-1) with child 32. | No balancing required | |
| 29 | Tree diagram: Root 31 (1). Left child 23 (-1) with children 22 and 28 (containing 24, 29). Right child 31 (-1) with child 32. | No balancing required | |
| 26 | [Tree Diagram] | RL | [Tree Diagram] |
| 27 | [Tree Diagram] | LR | [Tree Diagram] |
| 34 | [Tree Diagram] | RR | [Tree Diagram] |
| 36 | [Tree Diagram] | RR | [Tree Diagram] |

## EXAMPLE 10.6 Construct an AVL tree for the following data:
STA, ADD, LDA, MOV, JMP, TRIM, XCHG, MVI, DIV, NOP, IN, JNZ

Solution Figure 10.24 demonstrates the steps involved to construct the AVL tree for the given sequence.

### 1. Insert STA

![](img/a99ec79093c067f0bed8f1086197950e_532_0.png)

### 2. Insert ADD

![](img/a99ec79093c067f0bed8f1086197950e_532_1.png)

### 3. Insert LDA

![](img/a99ec79093c067f0bed8f1086197950e_532_2.png)

### 4. Insert MOV

![](img/a99ec79093c067f0bed8f1086197950e_532_3.png)

### 5. Insert JMP

![](img/a99ec79093c067f0bed8f1086197950e_532_4.png)

### 6. Insert TRIM

![](img/a99ec79093c067f0bed8f1086197950e_532_5.png)

### 7. Insert XCHG

![](img/a99ec79093c067f0bed8f1086197950e_533_0.png)

### 8. Insert MVI

![](img/a99ec79093c067f0bed8f1086197950e_533_1.png)

### 9. Insert DIV

![](img/a99ec79093c067f0bed8f1086197950e_533_2.png)

### 10. Insert NOP

![](img/a99ec79093c067f0bed8f1086197950e_533_3.png)

### 11. Insert IN

![](img/a99ec79093c067f0bed8f1086197950e_534_0.png)

### 12. Insert JNZ

![](img/a99ec79093c067f0bed8f1086197950e_534_1.png)

Fig.10.24 (Continued) (k) Key = IN (l) Key = JNZ

## EXAMPLE 10.7 Construct an AVL tree for the set of keys = {50, 55, 60, 15, 10, 40, 20, 45, 30, 70, 80}.

Solution Figure 10.25 demonstrates the construction of an AVL tree for the given set of keys.

### 1. After insertion of (50, 55, and 60):

![](img/a99ec79093c067f0bed8f1086197950e_534_2.png)

### 2. After insertion of (15, 10, 40, 20, 45, and 30):

![](img/a99ec79093c067f0bed8f1086197950e_535_0.png)

RL

![](img/a99ec79093c067f0bed8f1086197950e_535_1.png)

RR

### 3. After insertion of 70 and 80:

![](img/a99ec79093c067f0bed8f1086197950e_535_2.png)

Fig.10.25 Construction of AVL tree for Example 10.7

## RECAPITULATION

- Search trees are of great importance in an algorithm design.
- It is always desirable to keep the search time of each node in a tree minimal.
- OBST maintains the optimal average search time of all the nodes.
- In an AVL tree, after insertion of each node, it is checked whether the tree is balanced or not. If unbalanced, it is rebalanced immediately.
- Rebalancing of AVL tree is performed using one of the four rotations: LL, RR, LR, RL.
- AVL trees work by ensuring that all nodes of the left and right subtrees differ in height by utmost 1, which ensures that a tree cannot get too deep.
- Compilers use hash tables to keep track of the declared variables in a source code called as a symbol table.
- Unbalancing of an AVL tree due to insertion is removed in a single rotation. However, unbalancing due to the deletion may require multiple steps for balancing.

## KEY TERMS

AVL tree An AVL tree is a BST where the heights of the left and right subtrees of the root differ by utmost 1. In addition, the left and right subtrees of the root are again AVL trees.

Keyed table Keyed tables are a very useful data structure. They store <key, information> pairs with no additional logical structure.

OBST Optimal binary search tree is a binary search tree having an average search time of all keys as the optimal value.

Symbol table While compilers and assemblers scan a program, each identifier must be examined to determine if it is a keyword. This information concerning the keywords and identifier in a programming language is stored in a table called symbol table.

## EXERCISES

### Multiple choice questions

- 1. Which of the following is true?
- (a) The cost of searching an AVL tree is O(logn) but that of a BST is O(n).
- (b) The cost of searching an AVL tree is O(logn) but that of a complete binary tree is O(logn).
- (c) The cost of searching a BST is O(logn) but that of an AVL tree is O(n).
- (d) The cost of searching an AVL tree is O(logn) but that of a BST is O(n)

- 2. In the following AVL tree, the structure has to be balanced, so we have to rotate it
- (a) clockwise
- (b) counter clockwise
- (c) in both the directions
- (d) none of the above

![](img/a99ec79093c067f0bed8f1086197950e_536_0.png)

- 3. What is the maximum height of an AVL tree with seven nodes?
- Note: Assume that the height of a tree with a single node is 0.

- (a) 2
- (b) 3
- (c) 4
- (d) 5

- 4. The worst case height of an AVL tree with n nodes is
- (a) 1.44log(n + 2)
- (b) 2.44log(n + 2)
- (c) 3.44log(n + 2)
- (d) 1.44log(n + 2)

- 5. What will be the time complexity for inserting a node into an AVL tree?
- (a) O(n)
- (b) O(logn)
- (c) n
- (d) n²

- 6. Which of the following properties of OBST is true?
- (a) The left subtree of a node contains only the nodes with keys less than the node's key.
- (b) The right subtree of a node contains only the nodes with keys greater than the node's key.
- (c) Both the left and right subtrees must also be BSTs.
- (d) All of the above

- 7. To find the cost of the given OBST,

![](img/a99ec79093c067f0bed8f1086197950e_537_0.png)

- (c) 16/7
- (d) 12/7

### Review questions

1. A size-balanced binary tree in which for every node, the difference between the number of nodes in the left and right subtree is utmost 1. The distance of a node from the root is the length of path from the root to the node. The height of a binary tree is the maximum distance of a leaf node from the root.
(a) Prove by using induction on h that a size-balanced binary tree of height h contains at least 2^h nodes.
(b) In a fixed-balanced binary tree of height h <= 1, how many nodes are at distance h - 1 from the root?

- we have to consider
- (a) successful search of internal nodes.
- (b) unsuccessful search of internal nodes.
- (c) successful search of internal nodes and unsuccessful search of external nodes.
- (d) unsuccessful search of external nodes.

2. (a) In a binary tree, a full node is defined to be a node with two children. Use induction on the height of the binary tree to prove that the number of full nodes plus one is equal to the number of leaves.
(b) Draw the min-heap that results from the insertion of the following elements in order into an initially empty min-heap: 7, 6, 5, 4, 2, 3, 1. Show the result after the deletion of the root of the heap.

- 8. What is the time complexity of an OBST?
- (a) O(n!)
- (b) O(nlogn)
- (c) O(logn)
- (d) O(n^2)

- 9. The OBST is an example of
- (a) static symbol table
- (b) dynamic symbol table
- (c) all of the above
- (d) none of the above

3. Consider the following array and draw the heap that this array represents.

![](img/a99ec79093c067f0bed8f1086197950e_537_1.png)

10. Compute the total cost of the given OBST, if the probability of successful search is (p1, p2, p3) = (1/7, 1/7, 1/7) and the probability of unsuccessful search is (q0, q1, q2, q3) = (1/7, 1/7, 1/7, 1/7)

4. What is OBST? Derive the various equations to calculate the cost and weight of each node in OBST. Write the pseudo-C++ code for the OBST algorithm.

![](img/a99ec79093c067f0bed8f1086197950e_537_2.png)

5. Insert the following numbers in an AVL tree and show at each stage the required transformations: 50, 60, 108, 8, 0, 48, 32, 40 Show the BF of each node throughout the process.

- (a) 2
- (b) 15/7

6. Compare OBST with AVL tree.

7. Give one example for each of the four types of rotations possible in an AVL tree.

