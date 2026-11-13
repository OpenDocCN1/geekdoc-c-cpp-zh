
case running time for its operations and is efficient to use as searching, insertion, and deletion can all be done in O(n log n) time, where n is the number of nodes in the tree. Practically, a red-black tree is a binary search tree which inserts and removes intelligently, to keep the tree reasonably balanced. A special point to note about the red-black tree is that in this tree, no data is stored in the leaf nodes.

## 10.5.1 Properties of Red-Black Trees

A red-black tree is a binary search tree in which every node has a colour which is either red or black. Apart from the other restrictions of a binary search tree, the red-black tree has the following additional requirements:

- The colour of a node is either red or black.
- The colour of the root node is always black.
- All leaf nodes are black.
- Every red node has both the children coloured in black.
- Every simple path from a given node to any of its leaf nodes has an equal number of black nodes.

Look at Fig. 10.55 which shows a red-black tree.

![](img/be6359df08208122bec6fad1103de211_341_0.png)

These constraints enforce a critical property of red-black trees. The longest path from the root node to any leaf node is no more than twice as long as the shortest path from the root to any other leaf in that tree.

This results in a roughly balanced tree. Since operations such as insertion, deletion, and searching require worst-case times proportional to the height of the tree, this theoretical upper bound on the height allows red-black trees to be efficient in the worst case, unlike ordinary binary search trees.

To understand the importance of these properties, it suffices to note that according to property 4, no path can have two red nodes in a row. The shortest possible path will have all black nodes, and the longest possible path would alternately have a red and a black node. Since all maximal paths have the same number of black nodes (property 5), no path is more than twice as long as any other path.

Figure 10.56 shows some binary search trees that are not red-black trees.

![](img/be6359df08208122bec6fad1103de211_342_0.png)

> (Root is red in colour)

![](img/be6359df08208122bec6fad1103de211_342_1.png)

> (Non-black leaf node)

(First, every red node does not have both the children coloured in black. Second, every simple path from a given node to any of its leaf nodes does not have equal number of black nodes.)

![](img/be6359df08208122bec6fad1103de211_342_2.png)

## 10.5.2 Operations on Red-Black Trees

Performing a read-only operation (like traversing the nodes in a tree) on a red-black tree requires no modification from those used for binary search trees. Remember that every red-black tree is a special case of a binary search tree. However, insertion and deletion operations may violate the properties of a red-black tree. Therefore, these operations may create a need to restore the red-black properties that may require a small number of O(log n) or amortized O(1) colour changes.

### Inserting a Node in a Red-Black Tree

The insertion operation starts in the same way as we add a new node in the binary search tree. However, in a binary search tree, we always add the new node as a leaf, while in a red-black tree, leaf nodes contain no data. So instead of adding the new node as a leaf node, we add a red internal node that has two black leaf nodes. Note that the colour of the new node is red and its leaf nodes are coloured in black.

Once a new node is added, it may violate some properties of the red-black tree. So in order to restore their property, we check for certain cases and restore the property depending on the case that turns up after insertion. But before learning these cases in detail, first let us discuss certain important terms that will be used.

Grandparent node (g) of a node (n) refers to the parent of N's parent (P), as in human family trees. The C code to find a node's grandparent can be given as follows:

```c
struct node * grand_parent(struct node *n)
{
    // No parent means no grandparent
    if ((n != NULL) && (n->parent != NULL))
        return n->parent->parent;
    else
        return NULL;
}
```

Uncle node (u) of a node (n) refers to the sibling of N's parent (P), as in human family trees. The C code to find a node's uncle can be given as follows:

```c
struct node * uncle(struct node *n)
{
    struct node *g;
    g = grand_parent(n);
    //With no grandparent, there cannot be any uncle
    if (g == NULL)
        return NULL;
    if (n->parent == g->left)
        return g->right;
    else
        return g->left;
}
```

When we insert a new node in a red-black tree, note the following:

- All leaf nodes are always black. So property 3 always holds true.
- Property 4 (both children of every red node are black) is threatened only by adding a red node, repainting a black node red, or a rotation.
- Property 5 (all paths from any given node to its leaf nodes has equal number of black nodes) is threatened only by adding a black node, repainting a red node black, or a rotation.

### Case 1: The New Node N is Added as the Root of the Tree

In this case, n is repainted black, as the root of the tree is always black. Since n adds one black node to every path at once, Property 5 is not violated. The C code for case 1 can be given as follows:

```c
void case1(struct node *n)
{
    if (n->parent == NULL) // Root node
        n->colour = BLACK;
    else
        case2(n);
}
```

### Case 2: The New Node's Parent P is Black

In this case, both children of every red node are black, so Property 4 is not invalidated. Property 5 is also not threatened. This is because the new node n has two black leaf children, but because n is red, the paths through each of its children have the same number of black nodes. The C code to check for case 2 can be given as follows:

```c
void case2(struct node *n)
{
    if (n->parent->colour == BLACK)
        return; /* Red black tree property is not violated*/
    else
        case3(n);
}
```

In the following cases, it is assumed that n has a grandparent node g, because its parent p is red, and if it were the root, it would be black. Thus, n also has an uncle node u (irrespective of whether u is a leaf node or an internal node).

### Case 3: If Both the Parent (P) and the Uncle (U) are Red

In this case, Property 5 which says all paths from any given node to its leaf nodes have an equal number of black nodes is violated. Insertion in the third case is illustrated in Fig. 10.57.

In order to restore Property 5, both nodes (p and u) are repainted black and the grandparent g is repainted red. Now, the new red node n has a black parent and the grandparent g is repainted red.

![](img/be6359df08208122bec6fad1103de211_344_0.png)

uncle must pass through the grandparent, the number of black nodes on these paths has not changed.

However, the grandparent g may now violate Property 2 which says that the root node is always black or Property 4 which states that both children of every red node are black. Property 4 will be violated when g has a red parent. In order to fix this problem, this entire procedure is recursively performed on g from Case 1.

The C code to deal with Case 3 insertion is as follows:

```c
void case3(struct node *n)
{
    struct node *u, *g;
    u = uncle(n);
    g = grand_parent(n);
    if ((u != NULL) && (u->colour == RED)) {
        n->parent->colour = BLACK;
        u->colour = BLACK;
        g->colour = RED;
        case3(g);
    }
    else {
        insert_case4(n);
    }
}
```

> Note: In the remaining cases, we assume that the parent node P is the left child of its parent. If it is the right child, then interchange left and right in cases 4 and 5.

### Case 4: The Parent P is Red but the Uncle U is Black and N is the Right Child of P and P is the Left Child of G

In order to fix this problem, a left rotation is done to switch the roles of the new node N and its parent P. After the rotation, note that in the C code, we have re-labelled N and P and then, case 5 is called to deal with the new node's parent. This is done because Property 4 which says both children of every red node should be black is still violated. Figure 10.58 illustrates Case 4 insertion.

![](img/be6359df08208122bec6fad1103de211_345_0.png)

Figure 10.58 Insertion in Case 4

Note that in case N is the left child of P and P is the right child of g, we have to perform a right rotation. In the C code that handles Case 4, we check for P and N and then, perform either a left or a right rotation.

```c
void case4(struct node *n)
{
    struct node *g = grand_parent(n);
    if ((n == n->parent->right) && (n->parent == g->left)) {
        rotate_left(n->parent);
        n = n->left;
    }
    else if ((n == n->parent->left) && (n->parent == g->right)) {
        rotate_right(n->parent);
        n = n->right;
    }
    case5(n);
}
```

### Case 5: The Parent P is Red but the Uncle U is Black and the New Node N is the Left Child of P, and P is the Left Child of its Parent G.

In order to fix this problem, a right rotation on G (the grandparent of N) is performed. After this rotation, the former parent P is now the parent of both the new node N and the former grandparent G. We know that the colour of G is black (because otherwise its former parent P could not have been red), so now switch the colours of P and G so that the resulting tree satisfies Property 4 which states that both children of a red node are black. Case 5 insertion is illustrated in Fig. 10.59.
