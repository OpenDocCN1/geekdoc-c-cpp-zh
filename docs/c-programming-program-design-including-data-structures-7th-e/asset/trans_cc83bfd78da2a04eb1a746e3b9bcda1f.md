
接下来，我们给出`class binaryTreeType`的非抽象成员函数的定义。

如果 root 为 `nullptr`，则二叉树为空。因此，函数`isEmpty`的定义为：

```cpp
template <class elemType>
bool binaryTreeType<elemType>::isEmpty() const
{
    return (root == nullptr);
}
```

默认构造函数将二叉树初始化为空状态；也就是说，它将指针 root 设置为 `nullptr`。因此，默认构造函数的定义为：

```cpp
template <class elemType>
binaryTreeType<elemType>::binaryTreeType()
{
    root = nullptr;
}
```

其他函数的定义如下：

```cpp
template <class elemType>
void binaryTreeType<elemType>::inorderTraversal() const
{
    inorder(root);
}
```

```cpp
template <class elemType>
void binaryTreeType<elemType>::preorderTraversal() const
{
    preorder(root);
}
```

```cpp
template <class elemType>
void binaryTreeType<elemType>::postorderTraversal() const
{
    postorder(root);
}
```

```cpp
template <class elemType>
int binaryTreeType<elemType>::treeHeight() const
{
    return height(root);
}
```

```cpp
template <class elemType>
int binaryTreeType<elemType>::treeNodeCount() const
{
    return nodeCount(root);
}
```

```cpp
template <class elemType>
int binaryTreeType<elemType>::treeLeavesCount() const
{
    return leavesCount(root);
}
```

```cpp
template <class elemType>
void binaryTreeType<elemType>::inorder
                    (nodeType<elemType> *p) const
{
    if (p != nullptr)
    {
        inorder(p->lLink);
        cout << p->info << " ";
        inorder(p->rLink);
    }
}
```

```cpp
template <class elemType>
void binaryTreeType<elemType>::preorder
                    (nodeType<elemType> *p) const
{
    if (p != nullptr)
    {
        cout << p->info << " ";
        preorder(p->lLink);
        preorder(p->rLink);
    }
}
```

```cpp
template <class elemType>
void binaryTreeType<elemType>::postorder
                    (nodeType<elemType> *p) const
{
    if (p != nullptr)
    {
        postorder(p->lLink);
        postorder(p->rLink);
        cout << p->info << " ";
    }
}
```

```cpp
template <class elemType>
int binaryTreeType<elemType>::height
                    (nodeType<elemType> *p) const
{
    if (p == nullptr)
        return 0;
    else
        return 1 + max(height(p->lLink), height(p->rLink));
}
```

```cpp
template <class elemType>
int binaryTreeType<elemType>::max(int x, int y) const
{
    if (x >= y)
        return x;
    else
        return y;
}
```

函数 nodeCount 和 leavesCount 的定义留作练习。参见本章末尾的编程练习1和2。

接下来，我们给出函数 copyTree、destroy、destroyTree、复制构造函数和析构函数的定义。我们还重载赋值运算符。

函数 copyTree 的定义与之前相同；在这里，该函数是类 binaryTreeType 的成员。

```cpp
template <class elemType>
void binaryTreeType<elemType>::copyTree
    (nodeType<elemType>* &copiedTreeRoot,
     nodeType<elemType>* otherTreeRoot)
{
    if (otherTreeRoot == nullptr)
        copiedTreeRoot = nullptr;
    else
    {
        copiedTreeRoot = new nodeType<elemType>;
        copiedTreeRoot->info = otherTreeRoot->info;
        copyTree(copiedTreeRoot->lLink, otherTreeRoot->lLink);
        copyTree(copiedTreeRoot->rLink, otherTreeRoot->rLink);
    }
} //end copyTree
```

要销毁一棵二叉树，对于每个节点，首先销毁其左子树，然后销毁其右子树，最后销毁该节点本身。我们必须使用 delete 运算符来释放该节点占用的内存。函数 destroy 的定义为：

```cpp
template <class elemType>
void binaryTreeType<elemType>::destroy(nodeType<elemType>* &p)
{
    if (p != nullptr)
    {
        destroy(p->lLink);
        destroy(p->rLink);
        delete p;
        p = nullptr;
    }
}
```

为了实现函数 destroyTree，我们使用函数 destroy，并将二叉树的根节点传递给函数 destroy。函数 destroyTree 的定义为：

```cpp
template <class elemType>
void binaryTreeType<elemType>::destroyTree()
{
    destroy(root);
}
```

回想一下，当类对象按值传递时，复制构造函数会将实参的值复制到形参中。由于类 binaryTreeType 具有指针成员变量，并且指针用于创建动态内存，因此我们必须提供复制构造函数的定义，以避免数据的浅拷贝。下面给出的复制构造函数定义使用函数 copyTree 来创建作为参数传递的二叉树的完全相同副本。

```cpp
//copy constructor
template <class elemType>
binaryTreeType<elemType>::binaryTreeType
                         (const binaryTreeType<elemType>& otherTree)
{
    if (otherTree.root == nullptr) //otherTree is empty
        root = nullptr;
    else
        copyTree(root, otherTree.root);
}
```

析构函数的定义非常直接。当 binaryTreeType 类型的对象超出作用域时，析构函数会释放二叉树节点占用的内存。析构函数的定义使用函数 destroy 来完成此任务。

```cpp
//Destructor
template <class elemType>
binaryTreeType<elemType>::~binaryTreeType()
{
    destroy(root);
}
```

接下来，我们讨论重载赋值运算符的函数的定义。为了将一棵二叉树的值赋给另一棵二叉树，我们使用函数 copyTree 创建要赋值的二叉树的完全相同副本。重载赋值运算符的函数的定义为：

```cpp
//Overload the assignment operator
template <class elemType>
const binaryTreeType<elemType>& binaryTreeType<elemType>::
                         operator=(const binaryTreeType<elemType>& otherTree)
{
    if (this != &otherTree) //avoid self-copy
    {
        if (root != nullptr)    //if the binary tree is not empty,
            destroy(root);      //destroy the binary tree

        if (otherTree.root == nullptr) //otherTree is empty
            root = nullptr;
        else
            copyTree(root, otherTree.root);
    } //end else

    return *this;
}
```

## 二叉搜索树

既然你已经了解了二叉树的基本操作，本节将讨论一种特殊类型的二叉树，称为二叉搜索树。

考虑图19–7中的二叉树。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1417_0.png)

**图 19-7** 任意二叉树

假设我们要确定 53 是否在二叉树中。为此，我们可以使用前面任意一种遍历算法访问每个节点，并将搜索项与节点中存储的数据进行比较。然而，这可能要求我们遍历二叉树的大部分，因此搜索会很慢。我们需要访问二叉树中的每个节点，直到找到该项或遍历完整棵二叉树，原因是没有任何准则可以指导我们的搜索。这种情况就像任意链表：我们必须从第一个节点开始搜索，并继续查看每个节点，直到找到该项或搜索完整个链表。

另一方面，考虑图19–8中的二叉树。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1418_0.png)

**图 19-8** 二叉搜索树

在图19–8的二叉树中，每个节点中的数据：

- 大于其左孩子中的数据
- 小于其右孩子中的数据

图19–8中的二叉树对其节点有一定顺序。假设我们要确定 58 是否在这棵二叉树中。和之前一样，我们必须从根节点开始搜索。我们将 58 与根节点中的数据进行比较；也就是说，我们将 58 与 60 进行比较。因为 58 ≠ 60 且 58 < 60，所以可以保证 58 不会在根节点的右子树中。因此，如果 58 在这棵二叉树中，那么它一定在根节点的左子树中。我们沿着根节点的左指针来到 info 为 50 的节点。现在我们在该节点应用相同的准则。因为 58 > 50，所以我们必须沿着该节点的右指针来到 info 为 58 的节点。在这个节点，我们找到了 58。

这个例子表明，每当我们向下移动到一个孩子节点时，就会从搜索中排除该节点的一棵子树。如果二叉树构造得足够好，那么这种搜索就非常类似于对数组的二分搜索。

图19–8中给出的二叉树是一种特殊类型的二叉树，称为二叉搜索树。（在下面的定义中，节点的 key 一词指的是唯一标识该项的数据项的键。）

**定义：** 一棵二叉搜索树 *T* 或者为空，或者：

- i. *T* 有一个称为**根**节点的特殊节点；
- ii. *T* 有两组节点，*L_T* 和 *R_T*，分别称为 *T* 的左子树和右子树；

