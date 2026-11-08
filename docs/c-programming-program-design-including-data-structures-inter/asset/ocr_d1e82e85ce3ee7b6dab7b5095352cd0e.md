Next, we give the definitions of the nonabstract member functions of the class `binaryTreeType`.

The binary tree is empty if root is NULL. So the definition of the function `isEmpty` is:

```
```cpp
template <class elemType>
bool binaryTreeType<elemType>::isEmpty() const
{
    return (root == NULL);
}
```
```

The default constructor initializes the binary tree to an empty state; that is, it sets the pointer root to NULL. Therefore, the definition of the default constructor is:

```
```cpp
template <class elemType>
binaryTreeType<elemType>::binaryTreeType()
{
    root = NULL;
}
```
```

The definitions of the other functions are:

```
```cpp
template <class elemType>
void binaryTreeType<elemType>::inorderTraversal() const
{
    inorder(root);
}
```
```

```
```cpp
template <class elemType>
void binaryTreeType<elemType>::preorderTraversal() const
{
    preorder(root);
}
```
```

```
```cpp
template <class elemType>
void binaryTreeType<elemType>::postorderTraversal() const
{
    postorder(root);
}
```
```

```
```cpp
template <class elemType>
int binaryTreeType<elemType>::treeHeight() const
{
    return treeHeight(root);
}
```
```

```
```cpp
template <class elemType>
int binaryTreeType<elemType>::treeNodeCount() const
{
    return nodeCount(root);
}
```
```