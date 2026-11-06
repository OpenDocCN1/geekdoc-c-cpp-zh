![](bbox=[0.394, 0.095, 0.787, 0.348])

**Figure 6**  Binary Search Tree After Five Insertions

We want to insert a new element Romeo into it.

`tree.add("Romeo");`

Start with the root, Juliet. Romeo comes after Juliet, so you move to the right subtree. You encounter the node Tom. Romeo comes before Tom, so you move to the left subtree. But there is no left subtree. Hence, you insert a new Romeo node as the left child of Tom (see Figure 6).

You should convince yourself that the resulting tree is still a binary search tree. When Romeo is inserted, it must end up as a right descendant of Juliet—that is what the binary search tree condition means for the root node Juliet. The root node doesn't care where in the right subtree the new node ends up. Moving along to Tom, the right child of Juliet, all it cares about is that the new node Romeo ends up somewhere on its left. There is nothing to its left, so Romeo becomes the new left child, and the resulting tree is again a binary search tree.

Here is the code for the insert member function of the `BinarySearchTree` class:

```
```cpp
void BinarySearchTree::insert(string data)
{
    TreeNode* new_node = new TreeNode;
    new_node->data = data;
    new_node->left = NULL;
    new_node->right = NULL;
    if (root == NULL)
    {
        root = new_node;
    }
    else
    {
        root->insert_node(new_node);
    }
}
```
```