# Chapter 6 Algorithms and complexity

+   * AA tree,
* AVL tree,
* B tree (variations: B+ tree, B*-tree),
* Binary tree,
* Fusion tree,
* Heap (variations: 2–3 heap, binary heap, binomial heap ...),
* K-d tree
* Octree,
* Quadtree,
* R-tree,
* Red-black tree (variation: LLRB tree),
* Scapegoat tree,
* Splay tree,
* T-tree,
* Top tree,
* Treap,
* Trie tree (variation: radix tree).

If one province of the landscape of useful data structures is this rich, we can see how tried-and-tested data structures there are to choose from, and how frequently problems occur require new and unique solutions to be developed. If we wish to be the designers of these new solutions, using the most efficient means available, we need to appreciate the synergy that exists between the algorithm and the data structure on which it works.

# Too clever for our own good

With the help of complex data structures, and making sensible assumptions about the input, it is possible to design complex algorithms that can perform well in time and space. However, it could be argued that such solutions might not always be the best.

How an algorithm performs in a computer system is clearly important; however, unless it is perfectly implemented, it will never be changed, somebody, at time, we will probably go back and modify how it works. A rule of thumb here is that the more complex the algorithm, the more fragile its implementation: fragile to unseen bugs and fragile to future changes. Sometimes, even with rigorous commenting the only way to follow a complex algorithm is to watch the flow of control, and keep track of multiple values in memory. Sometimes, the only course of action is to throw away the algorithm and start again from scratch. In such cases, it might be sensible (depending on how important its requirements are) to choose a less complex, less efficient algorithm, if it's more amenable to maintenance.

# 6.6 Implementing algorithms

In committing an algorithm to digital form, a new vista of interesting problems becomes apparent that can have a drastic impact on how well that algorithm performs. Some of these problems are relatively high-level, and can be offset by the type of problem, and solution, we have seen before. Choosing an appropriate programming language—if we are at liberty to do so—can lead to significant benefits in terms of efficiency and