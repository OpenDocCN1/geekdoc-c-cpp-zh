Depth of a tree. The depth of a tree is the maximum depth of any of its leaves. In Figure 10.2(b), the leaf containing 13 has depth three, and there is no deeper leaf. So the depth of the example tree is three. If a tree has only one node, the root, then its depth is zero (since the depth of the root is zero). The empty tree doesn't have any leaves, so we use –1 for its depth. Just to confuse things, you won't often see the term height of a tree used instead of depth, but they mean the same thing.

Full binary trees. In a full binary tree, every leaf has the same depth, and every nonleaf has two children. Figure 10.1 on page 475 is not a full tree because it has leaves at different depths—some with depth two and some with depth three. Also, some of the nonleaves have only one child. In Figure 10.2, part (a) is full, but parts (b) and (c) are not full.

Complete binary trees. Suppose you take a full binary tree and start adding new leaves at a new depth from left to right. All the new leaves have the same depth—one more than where we started—and we always add leftmost nodes first. For example, if you add three nodes to Figure 10.2(a), then another possible result is Figure 10.2(b). The tree is no longer a full tree because some leaves are a bit deeper than others. Instead, we call this a complete binary tree. In order to be a complete tree, every level except the deepest must contain as many nodes as possible; and at the deepest level, all the nodes are as far left as possible.

# Binary Taxonomy Trees

binary taxonomy trees store knowledge

Binary trees are useful in many situations. We'll look at one example, binary taxonomy trees, which can be used to store certain kinds of knowledge. The particular example we have in mind stores information about a collection of animals. Each leaf in a binary taxonomy tree contains the name of an animal, and each nonleaf node contains a question about animals.

For example, suppose that we want a taxonomy tree for four animals: a kangaroo, a mouse, a trout, and a robin. The tree might look like Figure 10.3. To use a binary taxonomy tree, you start at the root and ask the question that is written there. If the answer is "yes," you move to the left child, and if the answer is "no,"

# FIGURE 10.3 A Small Binary Taxonomy Tree

![](bbox=[0.17, 0.71, 0.73, 0.85])