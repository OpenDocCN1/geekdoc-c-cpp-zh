
![](img/45784b9f0334626143002ec0d63692fd_425_0.png)

(a) Delete 14

![](img/45784b9f0334626143002ec0d63692fd_425_1.png)

(b) Delete 27

Figure 13.4 Deletion of 14, 27 and 30 individually from 4-way search tree shown in Figure 13.2

![](img/45784b9f0334626143002ec0d63692fd_426_0.png)

(c) Delete 30

Figure 13.4 Continued

## 13.3.4 DRAWBACKS OF M-WAY SEARCH TREES

The search, insert and delete operations on an m-way search tree of height h (without external nodes) have the complexity as O(h). An m-way search tree of height h will have a minimum of h and a maximum of m^h -1 number of elements. Minimum of h is as one element per node at every level and maximum as at every level, each node has m child nodes and m -1 elements. This says that the maximum number of nodes at level i is given by m^(i-1). As in an m-way search tree of height h, the total number of nodes is

$$\sum_{i=1}^{h} m^{i-1} = \frac{(m^h - 1)}{(m - 1)}$$

and each of these nodes will have m-1 elements, the maximum number of elements is

$$\frac{(m^h - 1)}{(m - 1)}(m - 1) = (m^h - 1)$$

Because the number of elements in an m-way search tree with a height h will be from h to m^h -1, when a tree with n elements is considered its height will be a minimum of log (n+1) and a maximum of n. In the worst case the height of an m-way search tree with n elements may be O(n) which yields a poor performance. So, it is required to maintain the balanced heights in m-way search trees.

## 13.4 B TREES

A data structure which is a height balanced version of m-way search tree is known as a B tree of order m. When the growth of an m-way search tree is left uncontrolled then in the worst case it yields a complexity of O(n). This shows deterioration in performance. So, there is a need to have balanced m-way search trees which guarantees a complexity of O(log n) for search, insert and delete operations.

**Definition:** A B tree of order m is an m-way search tree and it may be empty. If not empty then the following properties to be satisfied by the extended trees:

- (i) The root node should have a minimum of two children and a maximum of m children.
- (ii) All the internal nodes except the root should be with a minimum [m/2] non-empty children and a maximum of m non-empty children.
- (iii) All the external nodes are at the same level.
- (iv) A leaf node must have minimum [m/2 - 1] and maximum m-1 elements.

The 4-way search tree shown in Figure 13.2 is not a B tree because all the external nodes are not at the same level. All the internal nodes except the root should be with a minimum [4/2] = 2 children. But, the node [12, 27] is a non-root internal node with only one child.

![](img/45784b9f0334626143002ec0d63692fd_427_0.png)

Figure 13.5 B Tree of order 3 (2-3 trees)

B trees with order 3 are also referred to as 2-3 trees as their internal nodes can have only two or three children. Figure 13.5 shows a B tree of order 3. B trees of order 4 are also referred to as 2-3-4 or 2-4 trees.

A B tree of order 5 is shown in Figure 13.6. In this tree the root [40, 82] has minimum two children. All the internal nodes except the root have minimum [m/2] = [5/2] = 3 children and hence two elements in corresponding order 5. All the external nodes are at the same level. As all the properties are satisfied, it is a B tree of order 5.

![](img/45784b9f0334626143002ec0d63692fd_428_0.png)

## 13.5 OPERATIONS ON B TREES

B tree grows in a bottom up manner. Various operations can be performed on B trees of order m but the most frequently used are search, insert and delete operations.

### 13.5.1 SEARCHING

The search operation on a B tree of order m is exactly the same as that performed on m-way search trees. If h is the height of the B tree of order m then the search operation yields a complexity of O(h).

### 13.5.2 INSERTION

Inserting an element into a B tree of order m is followed by the search operation for the same element. The place where search falls off, the element is inserted by following either of the cases. Case 1: In a B tree of order m, if node X in which the element is to be inserted can accommodate the element then it is inserted in the same node and the number of child pointer fields are adjusted accordingly. Case 2: In a B tree of order m if a node x in which the element is to be inserted is full, then first insert the element into its list of elements. This list is split into two at the median. The elements that are less than the median becomes the left node and that greater than the median becomes the right node. The median element is shifted up into the parent node of X. Accommodating the median element into the parent node may once again invoke either of the insertion cases. Insertion of element 64 into the B tree of order 5 shown in Figure 13.6 initiates search operation for 64. This falls at node [58, 74]. As it is not full the node is able to accommodate 64 and the node now appears as [58, 64, 74]. This is illustrated in Figure 13.7(a). To insert element 99 into the B tree the search operation for 99 falls off at node [86, 89, 93, 97]. This node is full and cannot accommodate 99. So, insert 99 into the list of elements, the list appears as 86, 89, 93, 97, 99. Here the median element is 93. So, split the node at the median into two as [86, 89] and [97, 99]. Now the median element 93 is shifted up into the parent, i.e. root. Again Case 1 is invoked to insert 93 into the root. This is illustrated in Figure 13.7(b).

![](img/45784b9f0334626143002ec0d63692fd_429_0.png)

![](img/45784b9f0334626143002ec0d63692fd_429_1.png)

Figure 13.7 Inserting 64 and 99 individually into the B tree of order 5 shown in Figure 13.6

### 13.5.3 DELETION

Deleting an element from a B Tree of an order m may be performed according to one of the four cases.

Case 1: This deletion is the simplest of all the cases. An element belongs to a leaf node and deleting it does not make the node with the number of elements less than its minimum number of elements. In this case the element is deleted from the leaf node and the child pointers are adjusted accordingly.

Case 2: When an element x from a non-leaf node is to be deleted, replace x with the largest element from its left subtree or the smallest element from its right subtree. The replaced element must be deleted from the node and as it happens to be from a leaf node; Case 1 is followed to delete it.

The B tree of order 5 shown in Figure 13.6 is considered. To delete 89 from the tree as it is a leaf node element, Case 1 can be followed. Delete 89 and adjust its child pointer fields. To delete 40, a non-leaf node element, Case 2 can be followed. Replace 40 with 38 the largest element from its left subtree. Deleting 38 again follows Case 1. This is illustrated in Figure 13.8

![](img/45784b9f0334626143002ec0d63692fd_430_0.png)

(a) After deleting 89

![](img/45784b9f0334626143002ec0d63692fd_430_1.png)

(b) Delete 40

**Figure 13.8** Deletion of 89 and 40 individually from B tree of order 5 shown in Figure 13.6

If the deletion of an element leaves less than the minimum number of elements in the corresponding nodes, then deletion becomes complicated. Cases 3 and 4 deal with such cases. Case 3: If deleting an element k from a node leaves it with less than its minimum number of elements, then elements can be borrowed from either of its sibling nodes. When the left subtree node is capable to spare the element then its largest element is shifted into the parent node. If the right subtree node is capable to do so, its smallest element is shifted into the parent node. From the parent node the intervening element is shifted down to fill the vacancy created by the deleted element.

Case 4: In a situation where the deletion of an element is making the elements of the node to be less than its minimum number and if either or both of its sibling nodes have no chance of sparing an element, then this node is merged with either the sibling nodes including the intervening element from the parent node. This once again invokes one of the cases to delete the intervening element from the parent node.

Consider the B tree of order 5 shown in Figure 13.6. Deleting 58 leaves the node with one element, i.e. less than the minimum number of elements. From its left sibling node 38 can be borrowed. So, 38 replaces the intervening parent node 40 and is pushed down to fill the vacancy created by deleting 58. Figure 13.9(a) depicts this situation. In this turn calls Case 1 to delete 38 from the leaf node. This is an illustration of Case 3.

To illustrate Case 4 consider the B tree of order 5 from Figure 13.9(a), the resulting tree after deleting 58. Deletion of 25 makes the nodes with elements less than the minimum number of elements. Its sibling right subtree is unable to spare the element. Now, merge 11 with [40, 74] along with the intervening element from the parent node, i.e. 38. So, the new node is [11, 38, 40, 74]. This is depicted in Figure 13.9(b).

![](img/45784b9f0334626143002ec0d63692fd_431_0.png)

(a) After deleting 58

![](img/45784b9f0334626143002ec0d63692fd_431_1.png)

(b) After deleting 25
