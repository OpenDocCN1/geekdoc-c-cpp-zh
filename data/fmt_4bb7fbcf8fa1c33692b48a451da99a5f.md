
# 第 21 章 二叉树

## 21.2 二叉搜索树

### `IntBinaryTree` 类成员函数实现

#### `insertNode(int num)`

```cpp
void IntBinaryTree::insertNode(int num)
{
    TreeNode *newNode = nullptr; // 指向新节点的指针。
    // 创建新节点并将 num 存储其中。
    newNode = new TreeNode;
    newNode->value = num;
    newNode->left = newNode->right = nullptr;

    // 插入节点。
    insert(root, newNode);
}
```

#### `destroySubTree(TreeNode *nodePtr)`

```cpp
void IntBinaryTree::destroySubTree(TreeNode *nodePtr)
{
    if (nodePtr)
    {
        if (nodePtr->left)
            destroySubTree(nodePtr->left);
        if (nodePtr->right)
            destroySubTree(nodePtr->right);
        delete nodePtr;
    }
}
```

#### `searchNode(int num)`

```cpp
bool IntBinaryTree::searchNode(int num)
{
    TreeNode *nodePtr = root;

    while (nodePtr)
    {
        if (nodePtr->value == num)
            return true;
        else if (num < nodePtr->value)
            nodePtr = nodePtr->left;
        else
            nodePtr = nodePtr->right;
    }
    return false;
}
```

#### `remove(int num)`

```cpp
void IntBinaryTree::remove(int num)
{
    deleteNode(num, root);
}
```

#### `deleteNode(int num, TreeNode *nodePtr)`

```cpp
void IntBinaryTree::deleteNode(int num, TreeNode *nodePtr)
{
    if (num < nodePtr->value)
        deleteNode(num, nodePtr->left);
    else if (num > nodePtr->value)
        deleteNode(num, nodePtr->right);
    else
        makeDeletion(nodePtr);
}
```

#### `makeDeletion(TreeNode *&nodePtr)`

```cpp
void IntBinaryTree::makeDeletion(TreeNode *&nodePtr)
{
    // 定义一个临时指针用于重新连接左子树。
    TreeNode *tempPtr = nullptr;

    if (nodePtr == nullptr)
        cout << "Cannot delete node.\n";
    else if (nodePtr->right == nullptr)
    {
        tempPtr = nodePtr;
        nodePtr = nodePtr->left; // 重新连接左节点。
        delete tempPtr;
    }
    else if (nodePtr->left == nullptr)
    {
        tempPtr = nodePtr;
        nodePtr = nodePtr->right; // 重新连接右节点。
        delete tempPtr;
    }
    else
    // 两个子节点。
    {
        // 向右侧移动。
        tempPtr = nodePtr->right;
        // 直到末尾。
        while (tempPtr->left)
            tempPtr = tempPtr->left;
        // 重新连接左子树。
        tempPtr->left = nodePtr->left;
        // 重新连接右节点。
        tempPtr->right = nodePtr->right;
        delete nodePtr;
        nodePtr = tempPtr;
    }
}
```

#### `displayInOrder(TreeNode *nodePtr)`

```cpp
void IntBinaryTree::displayInOrder(TreeNode *nodePtr)
{
    if (nodePtr)
    {
        displayInOrder(nodePtr->left);
        cout << nodePtr->value;
        displayInOrder(nodePtr->right);
    }
}
```

### 模板类 `BinaryTree<T>` 成员函数实现

#### `insert(TreeNode *&nodePtr, TreeNode *&newNode)`

```cpp
template <class T>
void BinaryTree<T>::insert(TreeNode *&nodePtr, TreeNode *&newNode)
{
    if (nodePtr == nullptr)
        nodePtr = newNode; // 插入节点
    else if (newNode->value < nodePtr->value)
        insert(nodePtr->left, newNode); // 搜索左分支
    else
        insert(nodePtr->right, newNode); // 搜索右分支
}
```

#### `insertNode(T item)`

```cpp
template <class T>
void BinaryTree<T>::insertNode(T item)
{
    TreeNode *newNode = nullptr; // 指向新节点的指针
    // 创建新节点并将名称存储其中。
    newNode = new TreeNode;
    newNode->value = item;
    newNode->left = newNode->right = nullptr;

    // 插入节点。
    insert(root, newNode);
}
```

#### `destroySubTree(TreeNode *nodePtr)`

```cpp
template <class T>
void BinaryTree<T>::destroySubTree(TreeNode *nodePtr)
{
    if (nodePtr)
    {
        if (nodePtr->left)
            destroySubTree(nodePtr->left);
        if (nodePtr->right)
            destroySubTree(nodePtr->right);
        delete nodePtr;
    }
}
```

#### `searchNode(T item)`

```cpp
template <class T>
bool BinaryTree<T>::searchNode(T item)
{
    TreeNode* nodePtr = root;

    while (nodePtr)
    {
        if (nodePtr->value == item)
            return true;
        else if (item < nodePtr->value)
            nodePtr = nodePtr->left;
        else
            nodePtr = nodePtr->right;

    }
    return false;
}
```
