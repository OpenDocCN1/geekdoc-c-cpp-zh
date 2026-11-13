```
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