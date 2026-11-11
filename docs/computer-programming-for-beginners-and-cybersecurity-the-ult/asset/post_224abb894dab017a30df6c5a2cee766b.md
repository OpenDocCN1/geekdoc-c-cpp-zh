
an easier way than the linked list. Doing this requires that the memory have more structure than a simple list.

So what does structuring data mean? When we started this journey, we only had arrays, but these never really gave us the ability to use data structures other than sequential lists. Linked lists use pointers to grow sequential lists incrementally but don't use the flexibility of the pointer to build more sophisticated structures.

What are these more sophisticated structures in memory? Structures that hold more than a single next node at any given time are a good example. But why would you want this? Simple. If you have two “next nodes,” one can be used to represent elements that are more than the current element. This is called a binary tree.

These are named because there are always one or two branches from every node. Each of the next nodes is a child, and the node that links to the child is the parent node.

This is what a binary tree might look like:

```
10

6 14

5 8 11 18
```

In the tree, the left child on each of the elements is smaller than the element, and the right child is larger. 10 is the parent node for the whole tree, and the child nodes of 6 and 14 are both parent nodes to their own small trees, called subtrees.

Binary trees have one very important property: each child is an entire tree. Combine this with the rule of the left child being smaller and the right child being larger, and you have an easy way of defining algorithms that locate specific nodes in the tree.

First, look at the current node value. If it equals the search target, it’s done. If it’s more than the search target, go left; otherwise, go right. This works because each node to the left of the tree is less than the current node value, and each on the right is more.

In an ideal world, your binary tree will be balanced with the exact same number of nodes on both sides. In such cases, every child tree is roughly 50 percent of the entire tree and, when you search the tree for a value, the search can eliminate 50 percent of the results each time it gets to a child node. So, if you had a tree of 1000 elements, 500 would be immediately eliminated. Search that tree again (it only has 500 elements now), and you can cut it by about 50 percent again. That way it doesn’t take long to find the value you want.

So, how many times must a tree be subdivided before you get to one element? The answer to that is log2n (n is the number of elements the tree has). This is a small value, even if your tree is large—if your tree had, say, 32 billion elements, the value would be 32; almost 100 million times faster than a search of a linked list of four billion elements, where every single one has to be assessed.

If the tree isn’t balanced, you won’t be able to eliminate roughly half of the elements; worst case, each node only has one child and that makes the tree nothing more than a linked list with a few extra pointers, thus requiring you to search all elements.

So, when a tree is approximately balanced, it’s much faster and easier to search for nodes than the same search on a linked list. This is because you can structure the memory of how you want it.

## Implementing a Binary Tree

To implement a binary tree, begin by declaring the node structure:

```cpp
struct node
{
    int key_value;
    node *p_left;
    node *p_right;
};
```

The node can store values as a simple integer, `key_value`, and has two child trees—`p_left` and `p_right`.

There are some common functions that you want on your binary tree: inserting, searching, removing, and destroying.

```cpp
node* insert (node* p_tree, int key);
node *search (node *p_tree, int key);
void destroyTree (node* p_tree);
node *remove (node *p_tree, int key);
```

### Inserting

We’ll use a recursive algorithm for inserting it into the tree. Recursion is fantastic for trees because there are two small trees for each tree; that makes the entire tree recursive by nature. The function takes a key and a tree that already exists (even an empty one) and returns a new tree that has the inserted value.

```cpp
node* insert (node *p_tree, int key)
{
    // base case--we have got to an empty tree and our new node
    // needs to be inserted here
    if ( p_tree == NULL )
    {
        node* p_new_tree = new node;
        p_new_tree->p_left = NULL;
        p_new_tree->p_right = NULL;
        p_new_tree->key_value = key;
        return p_new_tree;
    }
    // decide—left subtree or right subtree for the insertion
    // depending on what the node value is
    if( key < p_tree->key_value )
    {
        // build a new tree from p_tree->p_left, and add in the key
        // replace existing p_tree->p_left pointer with a pointer
        // to the new tree. Set the p_tree->p_left pointer
        // in case p_tree->p_left is NULL. (If it isn’t NULL,
        // p_tree->p_left won't change but it sets it just
        // to make sure.)
        p_tree->p_left = insert( p_tree->p_left, key );
    }
    else
    {
        // Insertion into the right side is symmetric to the
        // insertion in the left
        p_tree->p_right = insert( p_tree->p_right, key );
    }
    return p_tree;
}
```

The basic logic here is this: if you have an empty tree, you create a new one. If not, the value for insertion goes to the left subtree if it’s less than the current node, and the left subtree is then replaced with the new one. Otherwise, insert it into the right subtree and replace it.

When it comes to seeing it in action, build an empty tree into a tree with a couple of nodes. If the value 10 is inserted in the empty tree (NULL), immediately we will hit base case, and the result will be a tree of:

![](img/ecb1bfa35f80f656f92811abb43b3df7_231_0.png)

And both of the child trees will point to NULL.

Then insert 5 into the tree and make the following call:

```text
insert(a tree with a parent, 5)
```

Because 5 is lower than 10, the call onto the left-subtree is recursive:

```text
insert( NULL, 5 )
insert(a tree with a parent, 5)
```

The call of `insert( NULL, 5 )` creates and returns a new tree:

![](img/ecb1bfa35f80f656f92811abb43b3df7_231_1.png)

When the returned tree is received, `insert(a tree with a parent, 5)` links the trees. In this example, 10’s left child was NULL before. Therefore, the left child of 10 is established as a new tree:

![](img/ecb1bfa35f80f656f92811abb43b3df7_231_2.png)

If we now add 7, we get:

```text
insert( NULL, 7 )
insert(a tree with a parent, 7)
```

So, first off, `insert( NULL, 7 )` will return a new tree:

![](img/ecb1bfa35f80f656f92811abb43b3df7_232_0.png)

And then `insert(a tree with a parent, 7)` will link to the subtree of 7 in this way:

![](img/ecb1bfa35f80f656f92811abb43b3df7_232_1.png)

Lastly, the tree gets returned to `insert(a tree with a parent, 7)`. And this will link it back:

![](img/ecb1bfa35f80f656f92811abb43b3df7_232_2.png)

Because there was already a pointer from 10 to the node with 5, it isn’t really necessary to relink 10’s left child to the tree with 5 as the parent, but it does eliminate one conditional check to see if the subtree is empty.

### Destroying

This should also be a recursive function. Before deleting the current node, the algorithm destroys both of the subtrees that are at the current node.

```cpp
void destroy_tree (node *p_tree)
{
    if ( p_tree != NULL )
    {
        destroy_tree( p_tree->p_left );
        destroy_tree( p_tree->p_right );
        delete p_tree;
    }
}
```

As a way of better understanding this, let’s say that the value of the node was printed before the node was deleted:

```cpp
void destroy_tree (node *p_tree)
{
    if ( p_tree != NULL )
    {
        destroy_tree( p_tree->p_left );
        destroy_tree( p_tree->p_right );
        cout << "Deleting node: " << p_tree->key_value;
        delete p_tree;
    }
}
```

As you can see, the tree is deleted from the bottom up. Nodes 5 and 8 go first, then 6, before moving to the other side and deleting 11 and 18, followed by 14. Lastly, 10 will be deleted. The tree values aren’t important; what matters is where the node is. In the following binary tree, rather than the node values, we use the order of deletion:
