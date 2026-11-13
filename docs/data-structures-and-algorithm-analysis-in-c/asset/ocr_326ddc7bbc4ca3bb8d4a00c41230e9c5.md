```
1 /*
2  * Internal method to merge two roots.
3  * Assumes trees are not empty, and h1's root contains smallest item.
4  */
5 LeftistNode * merge1( LeftistNode * h1, LeftistNode * h2 )
6 {
7 if ( h1->left == nullPtr ) // Single node
8 h1->left = h2; // Other fields in h1 already accurate
9 else
10 {
11 h1->right = merge( h1->right, h2 );
12 if ( h1->left->npl < h1->right->npl )
13 swapChildren( h1 );
14 h1->npl = h1->right->npl + 1;
15 }
16 return h1;
17 }
```

# Figure 6.27 Actual routine to merge leftist heaps

A second pass is made up the heap, and child swaps are performed at nodes that violate the leftist heap property. In Figure 6.28, there is a swap at nodes 7 and 3, and the same tree as before is obtained. The nonrecursive version is simpler to visualize but harder to code. We leave it to the reader to show that the recursive and nonrecursive procedures do the same thing.

![](bbox=[0.05, 0.59, 0.8, 0.88])

# Figure 6.28 Result of merging right paths of H1 and H2