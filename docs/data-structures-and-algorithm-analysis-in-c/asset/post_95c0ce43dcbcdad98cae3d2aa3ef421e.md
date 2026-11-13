
of red-black trees is the relatively low overhead required to perform insertion, and the fact that, in practice, rotations occur relatively infrequently.

An actual implementation is complicated not only by the host of possible rotations but also by the possibility that some subtrees (such as 1's right subtree) might be empty, and the special case of dealing with the root (which among other things, has no parent). Thus, we use two sentinel nodes: one for the root, and nullNode, which indicates a nullPtr pointer as it did for splay trees. The root sentinel will store the key -infinity and a right link to the real root. Because of this, the searching and printing procedures need to be adjusted. The recursive routines are trickiest. Figure 12.13 shows how the inorder traversal is rewritten. The printTree routines are straightforward. The test t!=null could be written as t!=nullNode. However, there is a trap in a similar routine that performs the deep copy. This is also shown in Figure 12.13. The copy constructor calls clone after other initialization is complete. But in clone, the test t==nullNode does not work, because nullNode is the target's null node, not the sources (that is not nullNode). Thus we use a trickier test.

Figure 12.14 shows the RedBlackTree skeleton, along with the constructor.

Next, Figure 12.15 (page 574) shows the routine to perform a single rotation. Because the resultant tree must be attached to a parent, rotate takes the parent node as a parameter. Rather than keeping track of the type of rotation as we descend the tree, we pass it as a parameter. Since we expect very few rotations during the insertion procedure, it turns out that it is not only simpler, but actually faster, to do it this way. rotate simply returns the result performing an appropriate single rotation.

Finally, we provide the insertion procedure in Figure 12.16 (on page 574). The routine handleReorient is called when we encounter a node with two red children, and also when we insert a leaf. The trickiest part is the observation that a double rotation is really two single rotations, and is done only when branching to X (represented in the insert method by current) takes opposite directions. As we mentioned in the earlier discussion, insert must keep track of the parent, grandparent, and great-grandparent as the tree is descended. Since these are shared with handleReorient, we make these class members. Note that after a rotation, the values stored in the grandparent and great-grandparent are no longer correct. However, we are assured that they will be restored by the time they are next needed.

## 12.2.3 Top-Down Deletion

Deletion in red-black trees can also be performed top-down. Everything boils down to being able to delete a leaf. This is because to delete a node that has two children, we replace it with the smallest node in the right subtree; that node, which must have at most one child, is then deleted. Nodes with only a right child can be deleted in the same manner, while nodes with only a left child can be deleted by replacement with the largest node in the left subtree, and subsequent deletion of that node. Note that for red-black trees, we don't want to use the strategy of bypassing for the case of a node with one child because that may connect two red nodes in the middle of the tree, making enforcement of the red-black condition difficult.

```cpp
void printTree( ) const
{
    if( header->right == nullNode )
        cout << "Empty tree" << endl;
    else
        printTree( header->right );
}

void printTree( RedBlackNode *t ) const
{
    if( t != t->left )
    {
        printTree( t->left );
        cout << t->element << endl;
        printTree( t->right );
    }
}

RedBlackTree( const RedBlackTree & rhs )
{
    nullNode = new RedBlackNode;
    nullNode->left = nullNode->right = nullNode;

    header = new RedBlackNode( rhs.header->element );
    header->left = nullNode;
    header->right = clone( rhs.header->right );
}

RedBlackNode *clone( RedBlackNode * t ) const
{
    if( t == t->left ) // Cannot test against nullNode!!!
        return nullNode;
    else
        return new RedBlackNode{ t->element, clone( t->left ),
                                 clone( t->right ), t->color };
}
```

Figure 12.13 Tree traversals with two sentinels: printTree and copy constructor

Deletion of a red leaf is, of course, trivial. If a leaf is black, however, the deletion is more complicated because removal of a black node will violate condition 4. The solution is to ensure during the top-down pass that the leaf is red.

Throughout this discussion, let X be the current node, T be its sibling, and P be their parent. We begin by coloring the root sentinel red. As we traverse down the tree, we attempt to ensure that X is red. When we arrive at a new node, we are certain

```cpp
template <typename Comparable>
class RedBlackTree
{
public:
    explicit RedBlackTree( const Comparable & negInf );
    RedBlackTree( const RedBlackTree & rhs );
    RedBlackTree & operator=( const RedBlackTree & rhs );
    ~RedBlackTree( );

    const Comparable & findMin( ) const;
    const Comparable & findMax( ) const;
    bool contains( const Comparable & x ) const;
    bool isEmpty( ) const;
    void printTree( ) const;

    void makeEmpty( );
    void insert( const Comparable & x );
    void remove( const Comparable & x );

    enum { RED, BLACK };

    RedBlackTree & operator=( const RedBlackTree & rhs );
    RedBlackTree & operator=( RedBlackTree && rhs );

private:
    struct RedBlackNode
    {
        Comparable element;
        RedBlackNode *left;
        RedBlackNode *right;
        int color;

        RedBlackNode( const Comparable & theElement = Comparable{ },
                      RedBlackNode *lt = nullptr, RedBlackNode *rt = nullptr,
                      int c = BLACK )
            : element{ theElement }, left{ lt }, right{ rt }, color{ c } { }

        RedBlackNode( Comparable && theElement, RedBlackNode *lt = nullptr,
                      RedBlackNode *rt = nullptr, int c = BLACK )
            : element{ std::move( theElement ) }, left{ lt }, right{ rt }, color{ c } { }
    };

    RedBlackNode *header;    // The tree header (contains negInf)
    RedBlackNode *nullNode;

    // Used in insert routine and its helpers (logically static)
    RedBlackNode *current;
}
```

Figure 12.14 Class interface and constructor

```cpp
RedBlackNode *parent;
RedBlackNode *grand;
RedBlackNode *great;
// usual recursive stuff
void reclaimMemory( RedBlackNode *t );
void printTree( RedBlackNode *t ) const;
RedBlackNode * clone( RedBlackNode * t ) const;
// Red-black tree manipulations
void handleReorient( const Comparable & item );
RedBlackNode * rotate( const Comparable & item, RedBlackNode *theParent );
void rotateWithLeftChild( RedBlackNode * & k2 );
void rotateWithRightChild( RedBlackNode * & k1 );
};
/**
 * Construct the tree.
 * negInf is a value less than or equal to all others.
 */
explicit RedBlackTree( const Comparable & negInf )
{
    nullNode = new RedBlackNode;
    nullNode->left = nullNode->right = nullNode;
    header = new RedBlackNode( negInf );
    header->left = header->right = nullNode;
}
```

Figure 12.14 (continued)

that P is red (inductively, by the invariant we are trying to maintain), and that X and T are black (because we can't have two consecutive red nodes). There are two main cases.

First, suppose X has two black children. Then there are three subcases, which are shown in Figure 12.17. If T also has two black children, we can flip the colors of X, T, and P to maintain the invariant. Otherwise, one of T's children is red. Depending on which one it is, we can apply the rotation shown in the second and third cases of Figure 12.17. Note carefully that this case will apply for the leaf, because nullNode is considered to be black.

If both children are red, we can apply either rotation. As usual, there are symmetric rotations for the case when X is a right child that are not shown.
