Next, we give the definitions of the nonabstract member functions of the `class binaryTreeType`.

The binary tree is empty if root is `nullptr`. So the definition of the function `isEmpty` is:

```
template <class elemType>
bool binaryTreeType<elemType>::isEmpty() const
{
    return (root == nullptr);
}
```

The default constructor initializes the binary tree to an empty state; that is, it sets the pointer root to `nullptr`. Therefore, the definition of the default constructor is:

```
template <class elemType>
binaryTreeType<elemType>::binaryTreeType()
{
    root = nullptr;
}
```

The definitions of the other functions are:

```
template <class elemType>
void binaryTreeType<elemType>::inorderTraversal() const
{
    inorder(root);
}
```

```
template <class elemType>
void binaryTreeType<elemType>::preorderTraversal() const
{
    preorder(root);
}
```

```
template <class elemType>
void binaryTreeType<elemType>::postorderTraversal() const
{
    postorder(root);
}
```

```
template <class elemType>
int binaryTreeType<elemType>::treeHeight() const
{
    return height(root);
}
```

```
template <class elemType>
int binaryTreeType<elemType>::treeNodeCount() const
{
    return nodeCount(root);
}
```