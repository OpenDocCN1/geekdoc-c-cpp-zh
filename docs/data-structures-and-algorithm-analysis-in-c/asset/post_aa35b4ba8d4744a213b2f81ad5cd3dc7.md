

```cpp
/**
 * Internal routine that performs a single or double rotation.
 * Because the result is attached to the parent, there are four cases.
 * Called by handleReorient.
 * item is the item in handleReorient.
 * theParent is the parent of the root of the rotated subtree.
 * Return the root of the rotated subtree.
 */
RedBlackNode * rotate( const Comparable & item, RedBlackNode *theParent )
{
    if( item < theParent->element )
    {
        item < theParent->left->element ?
            rotateWithLeftChild( theParent->left ) : // LL
            rotateWithRightChild( theParent->left ) ; // LR
        return theParent->left;
    }
    else
    {
        item < theParent->right->element ?
            rotateWithLeftChild( theParent->right ) : // RL
            rotateWithRightChild( theParent->right ); // RR
        return theParent->right;
    }
}
```

Figure 12.15 rotate method

```cpp
/**
 * Internal routine that is called during an insertion if a node has two red
 * children. Performs flip and rotations. item is the item being inserted.
 */
void handleReorient( const Comparable & item )
{
    // Do the color flip
    current->color = RED;
    current->left->color = BLACK;
    current->right->color = BLACK;
    if( parent->color == RED ) // Have to rotate
```

Figure 12.16 Insertion procedure

```cpp
{
    grand->color = RED;
    if ( item < grand->element || item < parent->element )
        parent = rotate( item, grand ); // Start dbl rotate
    current = rotate( item, great );
    current->color = BLACK;
}
header->right->color = BLACK; // Make root black
}
void insert( const Comparable & x )
{
    current = parent = grand = header;
    nullNode->element = x;

    while( current->element != x )
    {
        great = grand; grand = parent; parent = current;
        current = x < current->element ? current->left : current->right;

        // Check if two red children; fix if so
        if ( current->left->color == RED && current->right->color == RED )
            handleReorient( x );
    }
    // Insertion fails if already present
    if( current != nullNode )
        return;
    current = new RedBlackNode( x, nullNode, nullNode );

    // Attach to parent
    if( x < parent->element )
        parent->left = current;
    else
        parent->right = current;
    handleReorient( x );
}
```

Figure 12.16 (continued)

Otherwise one of X's children is red. In this case, we fall through to the next level, obtaining new X, T, and P. If we're lucky, X will land on the red child, and we can continue onward. If not, we know that T will be red, and X and P will be black. We can rotate T and P, making X's new parent red; X and its grandparent will, of course, be black. At this point, we can go back to the first main case.

![](img/e449061a0cac9cafaefd979fab665b33_594_0.png)

Figure 12.17 Three cases when X is a left child and has two black children

## 12.3 Treaps

Our last type of binary search tree, known as the **treap**, is probably the simplest of all. Like the skip list, it uses random numbers and gives O(log N) expected time behavior for any input. Searching time is identical to an unbalanced binary search tree (and thus slower than balanced search trees), while insertion time is only slightly slower than a recursive unbalanced binary search tree implementation. Although deletion is much slower, it is still O(log N) expected time.

The treap is so simple that we can describe it without a picture. Each node in the tree stores an item, a left and right pointer, and a priority that is randomly assigned when the node is created. A treap is a binary search tree with the property that the node priorities satisfy heap order: Any node's priority must be at least as large as its parents.

A collection of distinct items each of which has a distinct priority can only be represented by one treap. This is easily deduced by induction, since the node with the lowest priority must be the root. Consequently, the tree is formed on the basis of the N! possible arrangements of priority instead of the N! item orderings. The node declarations are straightforward, requiring only the addition of the priority member. The sentinel nullNode will have priority of \(\infty\), as shown in Figure 12.18.

```cpp
template <typename Comparable>
class Treap
{
  public:
    Treap( )
    {
        nullNode = new TreapNode;
        nullNode->left = nullNode->right = nullNode;
        nullNode->priority = INT_MAX;
        root = nullNode;
    }

    Treap( const Treap & rhs );
    Treap( Treap && rhs );
    ~Treap( );

    Treap & operator=( const Treap & rhs );
    Treap & operator=( Treap && rhs );

    // Additional public member functions (not shown)

  private:
    struct TreapNode
    {
        Comparable element;
        TreapNode *left;
        TreapNode *right;
        int priority;

        TreapNode( ) : left{ nullNode }, right{ nullNode }, priority{ INT_MAX }
        { }

        TreapNode( const Comparable & e, TreapNode *lt, TreapNode *rt, int pr )
            : element{ e }, left{ lt }, right{ rt }, priority{ pr }
        { }

        TreapNode( Comparable && e, TreapNode *lt, TreapNode *rt, int pr )
            : element{ std::move( e ) }, left{ lt }, right{ rt }, priority{ pr }
        { }
    };

    TreapNode *root;
    TreapNode *nullNode;
    UniformRandom randomNums;

    // Additional private member functions (not shown)
};
```

Insertion into the treap is simple: After an item is added as a leaf, we rotate it up the treap until its priority satisfies heap order. It can be shown that the expected number of rotations is less than 2. After the item to be deleted has been found, it can be deleted by increasing its priority to ∞ and rotating it down through the path of low-priority children. Once it is a leaf, it can be removed. The routines in Figure 12.19 and Figure 12.20 implement these strategies using recursion. A nonrecursive implementation is left for the reader (Exercise 12.14). For deletion, note that when the node is logically a leaf, it still has `nullNode` as both its left and right children. Consequently, it is rotated with the right child. After the rotation, `t` is `nullNode`, and the left child, which now stores the item to be deleted, can be freed. Note also that our implementation assumes that there are no duplicates; if this is not true, then the `remove` could fail (why?).

The treap implementation never has to worry about adjusting the priority data member. One of the difficulties of the balanced tree approaches is that it is difficult to track down errors that result from failing to update balance information in the course of an operation. In terms of total lines for a reasonable insertion and deletion package, the treap, especially a nonrecursive implementation, seems like the hands-down winner.

```
1 /**
2 * Internal method to insert into a subtree.
3 * x is the item to insert.
4 * t is the node that roots the tree.
5 * Set the new root of the subtree.
6 * (randomNums is a UniformRandom object that is a data member of Treap.)
7 */
8 void insert( const Comparable & x, TreapNode * & t )
9 {
10 if( t == nullNode )
11 t = new TreapNode( x, nullNode, nullNode, randomNums.nextInt( ) );
12 else if( x < t->element )
13 {
14 insert( x, t->left );
15 if( t->left->priority < t->priority )
16 rotateWithLeftChild( t );
17 }
18 else if( t->element < x )
19 {
20 insert( x, t->right );
21 if( t->right->priority < t->priority )
22 rotateWithRightChild( t );
23 }
24 // else duplicate; do nothing
25 }
```

Figure 12.19 Treaps: insertion routine

```cpp
/**
 * Internal method to remove from a subtree.
 * x is the item to remove.
 * t is the node that roots the tree.
 * Set the new root of the subtree.
 */
void remove( const Comparable & x, TreapNode * & t )
{
    if( t != nullNode )
    {
        if( x < t->element )
            remove( x, t->left );
        else if( t->element < x )
            remove( x, t->right );
        else
        {
            // Match found
            if( t->left->priority < t->right->priority )
                rotateWithLeftChild( t );
            else
                rotateWithRightChild( t );

            if( t != nullNode ) // Continue on down
                remove( x, t );
            else
            {
                delete t->left;
                t->left = nullNode; // At a leaf
            }
        }
    }
}
```

Figure 12.20 Treaps: deletion procedure

## 12.4 Suffix Arrays and Suffix Trees

One of the most fundamental problems in data processing is to find the location of a pattern, P, in a text, T. For instance, we may be interested in answering questions such as

- Is there a substring of T matching P?
- How many times does P appear in T?
- Where are all occurrences of P in T?

