**Zig-zag step** The zig-zag operation is performed when p is not the root. In addition to this, n is the right child of p and p is the left child of g or vice versa. In zig-zag step, the tree is first rotated on the edge between n and p, and then rotated on the edge between n and g. Refer Fig.10.67.

![](bbox=[0.2, 0.16, 0.8, 0.34])

Figure 10.67 Zig-zag step

# Inserting a Node in a Splay Tree

Although the process of inserting a new node n into a splay tree begins in the same way as we insert a node in a binary search tree, but after the insertion, n is made the new root of the splay tree. The steps performed to insert a new node n in a splay tree can be given as follows:

+   Step 1 Search n in the splay tree. If the search is successful, splay at the node n.
+   Step 2 If the search is unsuccessful, add the new node n in such a way that it replaces the null pointer reached during the search by a pointer to a new node n. Splay the tree at n.

# Example 10.11

Consider the splay tree given on the left. Observe the change in its structure when 81 is added to it.

# Solution

![](bbox=[0.15, 0.61, 0.85, 0.82])

**Note** To get the final splay tree, first apply zig-zag step on 81. Then apply zig-zag step to make 81 the root node.