![](bbox=[0.19, 0.08, 0.8, 0.38])

trie in Figure 12.25 is exactly one less than the number of internal branching nodes in the original trie in Figure 12.25. And of course writing all the suffixes in the leaves could take quadratic space. So if the original used quadratic space, so does the compressed trie. Fortunately, we can get by with linear space as follows:

+   1. In the leaves, we use the index where the suffix begins (as in the suffix array).
+   2. In the internal nodes, we store the number of common characters matched from the root until the internal node; this number represents the letter depth.

Figure 12.26 shows how the compressed trie is stored for the suffixes of banana. The leaves are simply the indices of the starting points for each suffix. The internal node with a letter depth of 1 is representing the common string "a" in all nodes that are below it. The internal

![](bbox=[0.19, 0.69, 0.8, 0.92])