
the node referenced by the root will need to change. We use the usual technique of implementing private recursive methods to do the merging. The class skeleton is also shown in Figure 6.25.

The two merge routines (Fig. 6.26) are drivers designed to remove special cases and ensure that H1 has the smaller root. The actual merging is performed in merge1 (Fig. 6.27). The public merge method merges rhs into the controlling heap. rhs becomes empty. The alias test in the public method disallows h.merge(h).

The time to perform the merge is proportional to the sum of the length of the right paths, because constant work is performed at each node visited during the recursive calls. Thus we obtain a O(log N) time bound to merge two leftist heaps. We can also perform this operation nonrecursively by essentially performing two passes. In the first pass, we create a new tree by merging the right paths of both heaps. To do this, we arrange the nodes on the right paths of H1 and H2 in sorted order, keeping their respective left children. In our example, the new right path is 3, 6, 7, 8, 18 and the resulting tree is shown in Figure 6.28.

```
/**
 * Merge rhs into the priority queue.
 * rhs becomes empty. rhs must be different from this.
 */
void merge( LeftistHeap& rhs )
{
    if( this == &rhs ) // Avoid aliasing problems
        return;

    root = merge( root, rhs.root );
    rhs.root = nullPtr;
}

/**
 * Internal method to merge two roots.
 * Deals with deviant cases and calls recursive merge1.
 */
LeftistNode * merge( LeftistNode *h1, LeftistNode *h2 )
{
    if( h1 == nullPtr )
        return h2;
    if( h2 == nullPtr )
        return h1;
    if( h1->element < h2->element )
        return merge1( h1, h2 );
    else
        return merge1( h2, h1 );
}
```

Figure 6.26 Driving routines for merging leftist heaps

```
/*
 * Internal method to merge two roots.
 * Assumes trees are not empty, and h1's root contains smallest item.
 */
LeftistNode * merge1( LeftistNode * h1, LeftistNode * h2 )
{
    if ( h1->left == nullPtr ) // Single node
        h1->left = h2; // Other fields in h1 already accurate
    else
    {
        h1->right = merge( h1->right, h2 );
        if ( h1->left->npl < h1->right->npl )
            swapChildren( h1 );
        h1->npl = h1->right->npl + 1;
    }
    return h1;
}
```

Figure 6.27 Actual routine to merge leftist heaps

A second pass is made up the heap, and child swaps are performed at nodes that violate the leftist heap property. In Figure 6.28, there is a swap at nodes 7 and 3, and the same tree as before is obtained. The nonrecursive version is simpler to visualize but harder to code. We leave it to the reader to show that the recursive and nonrecursive procedures do the same thing.

![](img/e449061a0cac9cafaefd979fab665b33_285_0.png)

Figure 6.28 Result of merging right paths of H1 and H2

```
/**
 * Inserts x; duplicates allowed.
 */
void insert( const Comparable & x )
{
    root = merge( new LeftistNode{ x }, root );
}
```

Figure 6.29 Insertion routine for leftist heaps

As mentioned above, we can carry out insertions by making the item to be inserted a one-node heap and performing a merge. To perform a deleteMin, we merely destroy the root, creating two heaps, which can then be merged. Thus, the time to perform a deleteMin is O(log N). These two routines are coded in Figure 6.29 and Figure 6.30.

Finally, we can build a leftist heap in O(N) time by building a binary heap (obviously using a linked implementation). Although a binary heap is clearly leftist, this is not necessarily the best solution, because the heap we obtain is the worst possible leftist heap. Furthermore, traversing the tree in reverse-level order is not as easy with links. The buildHeap effect can be obtained by recursively building the left and right subtrees and then percolating the root down. The exercises contain an alternative solution.

```
/**
 * Remove the minimum item.
 * Throws UnderflowException if empty.
 */
void deleteMin( )
{
    if( isEmpty( ) )
        throw UnderflowException{ };

    LeftistNode *oldRoot = root;
    root = merge( root->left, root->right );
    delete oldRoot;
}

/**
 * Remove the minimum item and place it in minItem.
 * Throws UnderflowException if empty.
 */
void deleteMin( Comparable & minItem )
{
    minItem = findMin( );
    deleteMin( );
}
```

Figure 6.30 deleteMin routine for leftist heaps

## 6.7 Skew Heaps

A skew heap is a self-adjusting version of a leftist heap that is incredibly simple to implement. The relationship of skew heaps to leftist heaps is analogous to the relation between splay trees and AVL trees. Skew heaps are binary trees with heap order, but there is no structural constraint on these trees. Unlike leftist heaps, no information is maintained about the null path length of any node. The right path of a skew heap can be arbitrarily long at any time, so the worst-case running time of all operations is O(N). However, as with splay trees, it can be shown (see Chapter 11) that for any M consecutive operations, the total worst-case running time is O(M log N). Thus, skew heaps have O(log N) amortized cost per operation.

As with leftist heaps, the fundamental operation on skew heaps is merging. The merge routine is once again recursive, and we perform the exact same operations as before, with one exception. The difference is that for leftist heaps, we check to see whether the left and right children satisfy the leftist heap structure property and swap them if they do not. For skew heaps, the swap is unconditional; we always do it, with the one exception that the largest of all the nodes on the right paths does not have its children swapped. This one exception is what happens in the natural recursive implementation, so it is not really a special case at all. Furthermore, it is not necessary to prove the bounds, but since this node is guaranteed not to have a right child, it would be silly to perform the swap and give it one. (In our example, there are no children of this node, so we do not worry about it.) Again, suppose our input is the same two heaps as before. Figure 6.31.

If we recursively merge $H_2$ with the subheap of $H_1$ rooted at 8, we will get the heap in Figure 6.32.

Again, this is done recursively, so by the third rule of recursion (Section 1.3) we need not worry about how it was obtained. This heap happens to be leftist, but there is no guarantee that this is always the case. We make this heap the new left child of $H_1$, and the old left child of $H_1$ becomes the new right child (see Fig. 6.33).

The entire tree is leftist, but it is easy to see that that is not always true: Inserting 15 into this new heap would destroy the leftist property.

We can perform all operations nonrecursively, as with leftist heaps, by merging the right paths and swapping left and right children for every node on the right path, with the exception of the last. After a few examples, it becomes clear that since all but the last node on the right path have their children swapped, the net effect is that this becomes the new left path (see the preceding example to convince yourself). This makes it very easy to merge two skew heaps visually.

![](img/e449061a0cac9cafaefd979fab665b33_287_0.png)

Figure 6.31 Two skew heaps $H_1$ and $H_2$

![](img/e449061a0cac9cafaefd979fab665b33_288_0.png)

![](img/e449061a0cac9cafaefd979fab665b33_288_1.png)

4 This is not exactly the same as the recursive implementation (but yields the same time bounds). If we only swap children for nodes on the right path that are above the point where the merging of right paths terminated due to exhaustion of one heap's right path, we get the same result as the recursive version.

The implementation of skew heaps is left as a (trivial) exercise. Note that because a right path could be long, a recursive implementation could fail because of lack of stack space, even though performance would otherwise be acceptable. Skew heaps have the advantage that no extra space is required to maintain path lengths and no tests are required to determine when to swap children. It is an open problem to determine precisely the expected right path length of both leftist and skew heaps (the latter is undoubtedly more difficult). Such a comparison would make it easier to determine whether the slight loss of balance information is compensated by the lack of testing.

## 6.8 Binomial Queues

Although both leftist and skew heaps support merging, insertion, and `deleteMin` all effectively in O(log N) time per operation, there is room for improvement because we know that binary heaps support insertion in _constant average_ time per operation. Binomial queues support all three operations in O(log N) worst-case time per operation, but insertions take constant time on average.

### 6.8.1 Binomial Queue Structure

**Binomial queues** differ from all the priority queue implementations that we have seen in that a binomial queue is not a heap-ordered tree but rather a _collection_ of heap-ordered trees, known as a **forest**. Each of the heap-ordered trees is of a constrained form known as a **binomial tree** (the reason for the name will be obvious later). There is at most one binomial tree of every height. A binomial tree of height 0 is a one-node tree; a binomial tree, B<sub>k</sub>, of height k is formed by attaching a binomial tree, B<sub>k-1</sub>, to the root of another binomial tree, B<sub>k-1</sub>. Figure 6.34 shows binomial trees B<sub>0</sub>, B<sub>1</sub>, B<sub>2</sub>, B<sub>3</sub>, and B<sub>4</sub>.

From the diagram we see that a binomial tree, B<sub>k</sub>, consists of a root with children B<sub>0</sub>, B<sub>1</sub>, ..., B<sub>k-1</sub>. Binomial trees of height k have exactly 2<sup>k</sup> nodes, and the number of nodes at depth d is the binomial coefficient \(\binom{k}{d}\). If we impose heap order on the binomial trees and allow at most one binomial tree of any height, we can represent a priority queue of any size by a collection of binomial trees. For instance, a priority queue of size 113 could be represented by a forest B<sub>3</sub>, B<sub>2</sub>, B<sub>0</sub>. We might write this representation as 1101, which not only represents 13 in binary but also represents the fact that B<sub>3</sub>, B<sub>2</sub>, and B<sub>0</sub> are present in the representation and B<sub>1</sub> is not.

As an example, a priority queue of six elements could be represented as in Figure 6.35.

### 6.8.2 Binomial Queue Operations

The minimum element can then be found by scanning the roots of all the trees. Since there are at most log N different trees, the minimum can be found in O(log N) time. Alternatively, we can maintain knowledge of the minimum and perform the operation in O(1) time if we remember to update the minimum when it changes during other operations.

Merging two binomial queues is a conceptually easy operation, which we will describe by example. Consider the two binomial queues, H<sub>1</sub> and H<sub>2</sub>, with six and seven elements, respectively, pictured in Figure 6.36.
