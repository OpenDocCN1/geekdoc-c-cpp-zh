Note that the following return statement does not work, since it can cause a dereferencing of nullptr, which is illegal. The error would be a run-time error, not a compiler error.

```
return (*i == target);
```

25. The template class SearchTree needs function declarations added. These are just the definitions.

```
template<class T>//uses iostream:
void SearchTree<T>::preorderShow() const
{
    preorderShow(root);
}
```

```
template<class T>//uses iostream:
void SearchTree<T>::preorderShow(
    TreeNode<T>* subTreeRoot) const
{
    if (subTreeRoot != nullptr)
    {
        cout << subTreeRoot->data << " ";
        preorderShow(subTreeRoot->leftLink);
        preorderShow(subTreeRoot->rightLink);
    }
}
```

```
template<class T>//uses iostream:
void SearchTree<T>::postorderShow() const
{
    postorderShow(root);
}
```

```
template<class T>//uses iostream:
void SearchTree<T>::postorderShow(
    TreeNode<T>* subTreeRoot) const
{
    if (subTreeRoot != nullptr)
    {
        postorderShow(subTreeRoot->leftLink);
        postorderShow(subTreeRoot->rightLink);
        cout << subTreeRoot->data << " ";
    }
}
```