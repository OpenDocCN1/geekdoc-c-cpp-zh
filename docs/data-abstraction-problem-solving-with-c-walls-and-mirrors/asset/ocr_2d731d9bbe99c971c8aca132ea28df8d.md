several variations of the basic binary search tree. Such trees absorb insertions and removals without a deterioration of their balance and are easier to maintain a minimum-height binary search tree. In addition, you can search these almost as efficiently as you can search a minimum-height binary search tree. This chapter discusses the better-known search trees to give you a sense of possibilities. We continue to assume that the entries in a tree are unique—that is, there are no duplicates.

# 19.2 2-3 Trees

A **2-3 tree** is a tree in which each internal node (nonleaf) has either two or three children and all leaves are at the same level. For example, Figure 19-2 shows a 2-3 tree of height 3. A node with two children is called a **2-node**—the nodes in the binary tree are all 2-nodes—and a node with three children is called a **3-node**.

FIGURE 19-2 A2-3 tree of height 3

![](bbox=[0.298, 0.355, 0.538, 0.473])

A 2-3 tree is not a binary tree, because a node can have three children; nevertheless, a 2-3 tree resembles a full binary tree. If a particular 2-3 tree contains only 2-nodes—a possibility, according to the definition—it is like a full binary tree, because all of its internal nodes have two children and all of its leaves are at the same level. If, on the other hand, some of the internal nodes of a 2-3 tree do have children, the tree will contain more nodes than a full binary tree of the same height. Therefore, a 2-3 tree of height $h$ always has at least as many nodes as a full binary tree of height $h$; that is, it has at least $2^{h-1}$ nodes. To prove this way, a 2-3 tree with $n$ nodes has height greater than $[\log_2(n+1)]$, the minimum height of a binary tree with $n$ nodes.

Given these observations, a 2-3 tree might be useful as an implementation of the AD dictionary. Indeed, if this is the case the 2-3 tree orders its nodes to make it useful as a search tree. Just as we distinguish between a binary tree and a search tree, we could distinguish between a “2-3 tree” and a “2-3 search tree.” The previous description would define a 2-3 tree, and the recursive definition next would define a 2-3 search tree. Most people, however, not make such a distinction and use the term “2-3” to mean “2-3 search tree”; we will do so as well. The following recursive definition of a 2-3 tree specifies the order of its nodes, making it a search tree:

> Note: 2-3 trees
T is a 2-3 tree of height $h$ if one of the following is:
* T is empty, in which case $h$ is 0.
* T is of the form