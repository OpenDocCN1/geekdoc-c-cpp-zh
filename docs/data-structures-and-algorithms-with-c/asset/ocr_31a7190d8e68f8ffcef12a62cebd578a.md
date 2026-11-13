+   - Every non-terminal node except root node has at least [m/2] non null pointers. The root node has at least 2 non-null pointers.
+   - All leaf nodes are at the same level and the tree is balanced.
+   - If a node has (m+1) children it must contain m key-pointers pairs.
+   - For each node key- value pair is less than next key-value pair.
+   - Each and every key- value pair of non-terminal node should be present at leaf level.
+   - All the leaf nodes must be linked with each other and form a linked structure at leaf level.

# Insertion in a B+ Tree

Insertion operation into a B+ tree of order m is performed by searching the appropriate leaf node where we insert the key. There are three cases for insert a key into B+ tree.

**Case 1:** When the leaf node is not at full capacity (i.e. it has fewer than m – 1 keys), then simply insert it into proper position so that after insertion the keys remain seated. Therefore, it requires to movement keys within leaf node for the newly inserted key. Since m is assumed a constant, so the constant time overhead may be ignored.

**Case 2:** When the node is full (i.e. it has exactly m – 1 keys), then one key is moved to immediate upper level. The key at [m/2]th position is moved upward. If m is even, then key at ([m/2]+1)th position can be moved upward. The rule of insertion should be same for inserting key elements at any level. When a key is moved then a copy of that key is stored at the leaf level. Intermediate nodes do not contain any duplicate values. Each leaf node makes link with succeeding leaf node to reduce searching time.

# Example:

Insert the following keys in a B+ tree of order 4 1, 4, 7, 10, 17, 21, 31, 25, 19, 20, 28, 42

Since the order of the B + tree is 4, the node of this tree can hold maximum 4 children, which implies the key pointers for each node is 4 whereas the key value is 3.

![](bbox=[0.105, 0.572, 0.655, 0.642])

![](bbox=[0.105, 0.682, 0.735, 0.862])