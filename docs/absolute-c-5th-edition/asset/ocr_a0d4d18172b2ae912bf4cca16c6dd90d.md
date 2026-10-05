# Answers to Self-Test Exercises

Note that the following return statement does not work, since it can cause a dereferencing of NULL, which is illegal. The error would be a run-time error, not a compiler error.

```
return (*i == target);
```

25. The template SearchTree needs function declarations added. These are just the definitions.

```
template<class T>//uses iostream:
void SearchTree<T>:::preorderShow( ) const
{
    preorderShow(root);
}
```

```
template<class T>//uses iostream:
void SearchTree<T>:::preorderShow(
    TreeNode<T>* subtreeRoot) const
    if (subtreeRoot != NULL)
    {
        cout << subtreeRoot->data << " ";
        preorderShow(subtreeRoot->leftLink);
        preorderShow(subtreeRoot->rightLink);
    }
```

```
template<class T>//uses iostream:
void SearchTree<T>:::postorderShow( ) const
{
    postorderShow(root);
}
```

```
template<class T>//uses iostream:
void SearchTree<T>:::postorderShow(
    TreeNode<T>* subtreeRoot) const
    {
    if (subtreeRoot != NULL)
    {
        postorderShow(subtreeRoot->leftLink);
        postorderShow(subtreeRoot->rightLink);
        cout << subtreeRoot->data << " ";
    }
```