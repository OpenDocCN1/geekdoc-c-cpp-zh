

- 3. The tree could be non-empty, with the root entry less than the target. Again, make a recursive call, using the pointer to the right subtree.

- 4. The tree could be non-empty, with the target equal to the root entry. We have found a copy of the target and must somehow remove it from the tree. But be careful! We can't simply delete this node, because it may have children and we don't want those children to be disconnected from the rest of the tree. To avoid orphaning those children, we'll deal with Case 4 in two separate cases:
- Case 4a: The root node has no left child.
- Case 4b: The root node does have a left child.
- The pseudocode for these two cases is described below.

### Case 4a.

In this case of the bst_remove function, the root data is equal to the target, and the root node has no left child. For example, we might be deleting Pittsburgh from this subtree:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_554_0.png)

In this case, we can delete the root entry and make the right child (Seattle) the new root node. To actually implement this root shift requires three steps:

```
oldroot_ptr = root_ptr;
root_ptr = root_ptr->right();
delete oldroot_ptr;
```

The variable oldroot_ptr is a local variable that we make point to the old root (the variable that we are about to get rid of). We then move the actual root pointer down to its right child. And finally we execute delete oldroot_ptr, which returns the old root node to the heap.

Does this scheme work correctly even if there is no right child? Yes, it does. With no right child, the statement root_ptr = root_ptr->right() will set the root pointer to NULL, indicating that there are no nodes left in this particular tree.

### Case 4b.

In this case, the root node does have a left child, so we can't simply move the root pointer to the right (as we did in Case 4a). We could check whether there is a right child, and if not, we could certainly move the root pointer left—but we have a more general plan in mind. The plan is to find some entry in the non-empty left subtree, and move this entry up to the root. But which entry? Here's an example to help you figure out which entry should be taken from the left subtree to replace the root entry. In this example, we are deleting Pittsburgh from this subtree:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_555_0.png)

The plan is to replace the root with one of the three entries from the left subtree. Which of these entries can safely be moved to the root? Not Atlanta, because the remaining entries in the left subtree (Chicago and Denver) would be larger than the new root (Atlanta). Not Chicago, because that would leave the larger string Denver in the left subtree. What about Denver? Yes, that will do, since none of the entries that remain in the left subtree are larger than Denver. Here is the resulting subtree after removing Denver from the left subtree and placing it at the root:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_555_1.png)

The string Denver is the correct choice because it is the largest entry in the left subtree. Any other choice from the left subtree will violate the binary search tree storage rules. So, how do we delete the largest item from the left subtree, and place this same item at the root? We can use our own bst_remove_max function with the call:

```
bst_remove_max(root_ptr->left(), root_ptr->data());
```

Now you know why we proposed the bst_remove_max function. Used in this way, it removes the largest item from the tree with root_ptr->left() as its root pointer, and it places this largest item in the root's data field.

### The bst_remove_max function.

The bst_remove_max function remains to be implemented. We'll leave that as an exercise in recursive thinking, with just two cases: (1) The base case occurs if there is no right child. In this case, the largest item is at the root, so you can set removed equal to the data from the root, move the root pointer down to the left, and delete the root node. (2) On the other hand, if there is a right child, then there are larger items in the right subtree. In this case, make a recursive call to delete the largest item from the right subtree.

## The Union Operators for Binary Search Trees

The last two operations for the bag are the += and + operators.

## The operator +=

The operator += has this prototype:

```
template <class Item>
void operator +=(const bag<Item>& addend);
```

This is another example of a function that will benefit from an auxiliary function. The auxiliary function that we propose is actually another bag member function, with this specification:

```
template <class Item>
void bag::insert_all
(const binary_tree_node<Item>* addroot_ptr);
// Precondition: addroot_ptr is the root pointer of a binary search tree that
// is separate from the binary search tree of the bag that activated this
// method.
// Postcondition: All the items from the addroot_ptr's binary search tree
// have been added to the binary search tree of the bag that activated this
// method.
```

Our intention is that this method is a new private member function of the bag. Since the function is private, the specification can use private information, such as the fact that the bag is implemented with a binary search tree. As a private method, the prototype for insert_all must be placed with other private members in the bag's definition, as shown here:

```
template <class Item>
class bag
{
public:
...
private:
binary_tree_node<Item>* root_ptr; // Root pointer
void insert_all
(const binary_tree_node<Item>* addroot_ptr);
};
```

A private member function is sometimes called a helper function because it will help the other member functions do their work. In the case of the bag, the operator += can be implemented by using insert_all, as shown next:

```
template <class Item>
void bag<Item>::operator +=(const bag& addend)
{
    binary_tree_node<Item> *addroot_ptr;

    if (this == &addend)
    {
        addroot_ptr = tree_copy(addend.root_ptr);
        insert_all(addroot_ptr);
        tree_clear(addroot_ptr);
    }
    else
        insert_all(addend.root_ptr);
}
```

Notice that we do have a bit of complication when the addend is the same bag as the bag that activated the operator += (as in the statement b += b). In this case we must make a second copy of the addend's tree and call insert_all, using the second copy rather than using the addend's tree directly. The reason for this complication is the restriction of insert_all's precondition, which requires that the tree that's being added "is separate from the binary search tree of the bag that activated this method."

Now we can look at the implementation of the private member function insert_all. The approach is to traverse the tree that we are adding, inserting a copy of each traversed item into the bag that activated the operator. For example, if we use a pre-order traversal, then the pseudocode for insert_all is:

```
if (addroot_ptr != NULL)
{
    insert(addroot_ptr->data( ));
    Make a recursive call to insert all of addroot_ptr's left subtree.
    Make a recursive call to insert all of addroot_ptr's right subtree.
}
```

Our pseudocode explicitly uses a pre-order traversal of the nodes. If you wish, you may use a post-order traversal instead. But avoid an in-order traversal. The problem with an in-order traversal is that the nodes of the addend tree will be processed in order from smallest to largest. Therefore, these nodes will be inserted into the other bag from smallest to largest. This is a bad way to build a binary search tree. The resulting tree ends up with a single long, narrow path, with only right children. Sometimes such long, narrow trees are hard to avoid. But do avoid such trees when you can, because searching and other algorithms are inefficient when the trees lose their branching structure. In the next chapter we will examine some specific ways to ensure that long, narrow trees are not created.

