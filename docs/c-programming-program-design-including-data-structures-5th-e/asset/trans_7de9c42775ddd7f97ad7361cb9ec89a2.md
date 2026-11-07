


```cpp
//复制构造函数
template <class elemType>
binaryTreeType<elemType>::binaryTreeType
              (const binaryTreeType<elemType> & otherTree)
{
    if (otherTree.root == NULL)  //otherTree 为空
        root = NULL;
    else
        copyTree(root, otherTree.root);
}
```

析构函数的定义相当简单。当 `binaryTreeType` 类型的对象超出作用域时，析构函数会释放二叉树各节点占用的内存。析构函数通过调用函数 `destroy` 来完成此任务。

```cpp
//析构函数
template <class elemType>
binaryTreeType<elemType>::~binaryTreeType()
{
    destroy(root);
}
```

接下来，我们讨论重载赋值运算符的函数定义。要将一棵二叉树的值赋给另一棵二叉树，我们使用函数 `copyTree`，创建待赋值二叉树的完全相同的副本。重载赋值运算符的函数定义如下：

```cpp
//重载赋值运算符
template <class elemType>
const binaryTreeType<elemType>& binaryTreeType<elemType>::
        operator=(const binaryTreeType<elemType>& otherTree)
{
    if (this != &otherTree)  //避免自我复制
    {
        if (root != NULL)  //如果二叉树非空，
                          //则销毁该二叉树
            destroy(root);

        if (otherTree.root == NULL)  //otherTree 为空
            root = NULL;
        else
            copyTree(root, otherTree.root);
    } //结束 else

    return *this;
}
```

## 二叉搜索树

了解二叉树的基本操作后，本节将介绍一种特殊类型的二叉树，称为二叉搜索树。

考虑图 20-7 所示的二叉树。

![](img/f97f778697507bb6fdd80c5991210cba_1326_0.png)

**图 20-7** 任意二叉树

假设我们要确定 53 是否在这棵二叉树中。为此，可以使用前面介绍的任意一种遍历算法访问每个节点，并将搜索项与节点中存储的数据进行比较。然而，这可能需要遍历二叉树的很大一部分，因此搜索速度会很慢。之所以需要逐个访问二叉树中的节点，直到找到该项或遍历完整棵二叉树，是因为没有任何准则可以引导搜索。这种情况类似于任意链表：我们必须从第一个节点开始搜索，并逐个检查节点，直到找到该项或搜索完整个链表。

另一方面，请考虑图 20-8 所示的二叉树。

![](img/f97f778697507bb6fdd80c5991210cba_1327_0.png)

图 20-8 二叉搜索树

在图 20-8 所示的二叉树中，每个节点中的数据：

- 大于其左子节点中的数据
- 小于其右子节点中的数据

图 20-8 所示的二叉树中的节点具有一定的顺序。假设我们要确定 58 是否在这棵二叉树中。和之前一样，我们必须从根节点开始搜索。将 58 与根节点中的数据进行比较，也就是将 58 与 60 进行比较。由于 58 ≠ 60 且 58 < 60，因此可以确定 58 不会在根节点的右子树中。因此，如果 58 在这棵二叉树中，它必定在根节点的左子树中。沿着根节点的左指针移动到信息为 50 的节点。然后在该节点应用相同的准则。由于 58 > 50，因此必须沿着该节点的右指针移动到信息为 58 的节点。在该节点，我们找到了 58。

这个例子表明，每次向下移动到子节点时，我们都会从搜索范围中排除该节点的一棵子树。如果二叉树构造得当，那么搜索过程就与在数组上执行二分查找非常相似。

图 20-8 所示的二叉树是一种特殊类型的二叉树，称为二叉搜索树。（在下面的定义中，术语“节点的键”指的是能够唯一标识数据项的数据项键。）

**定义：** **二叉搜索树** *T*，满足以下条件之一：为空，或者：

- i. *T* 有一个称为**根**节点的特殊节点；
- ii. *T* 有两组节点，分别称为 *T* 的左子树和右子树，记为 *L*_T 和 *R*_T；

```cpp
void deleteNode(const elemType& deleteItem);
    //从二叉搜索树中删除 deleteItem。
    //后置条件：如果找到与 deleteItem 信息相同的节点，
    //          则将其从二叉搜索树中删除。
    //          如果二叉树为空，或者 deleteItem 不在二叉树中，
    //          则打印相应的消息。

private:
    void deleteFromTree(nodeType<elemType>* &p);
        //从二叉搜索树中删除 p 所指向的节点。
        //后置条件：p 所指向的节点已从二叉搜索树中删除。
};
```

请自行绘制 `bSearchTreeType` 类的 UML 类图及其继承层次结构。参见本章末尾的练习 22。

接下来，我们介绍这些操作。

### 搜索

函数 `search` 在二叉搜索树中搜索给定项。如果在二叉搜索树中找到该项，则返回 `true`；否则返回 `false`。由于指针 `root` 指向二叉搜索树的根节点，因此必须从根节点开始搜索。此外，由于 `root` 必须始终指向根节点，我们需要使用另一个指针（例如 `current`）遍历二叉搜索树。将指针 `current` 初始化为 `root`。

如果二叉搜索树非空，首先将搜索项与根节点中的 `info` 进行比较。如果二者相同，则停止搜索并返回 `true`。否则，如果搜索项小于节点中的 `info`，则沿着 `LLink` 进入左子树；否则沿着 `RLink` 进入右子树。对下一个节点重复此过程。如果搜索项在二叉搜索树中，搜索将在包含该搜索项的节点处结束；否则，搜索将在空子树处结束。因此，通用算法如下：

```text
如果 root 为 NULL
    无法搜索空树，返回 false。
否则
{
    current = root;
    当 current 不为 NULL 且尚未找到时
        如果 current->info 与搜索项相同
            将 found 设为 true；
        否则
            如果 current->info 大于搜索项
                沿着 current 的 LLink 移动
            否则
                沿着 current 的 RLink 移动
}
```

该伪代码算法可转换为以下 C++ 函数：

```cpp
template <class elemType>
bool bSearchTreeType<elemType>::search
                         (const elemType& searchItem) const
{
    nodeType<elemType> *current;
    bool found = false;

    if (root == NULL)
        cout << "Cannot search an empty tree." << endl;
    else
    {
        current = root;

        while (current != NULL && !found)
        {
            if (current->info == searchItem)
                found = true;
            else if (current->info > searchItem)
                current = current->llink;
            else
                current = current->rlink;
        }//end while
    }//end else

    return found;
}//end search
```

### 插入

向二叉搜索树中插入项后，生成的二叉树必须仍然是二叉搜索树。要插入新项，首先搜索二叉搜索树，找到新项应插入的位置。搜索算法与函数 `search` 的算法类似。这里，我们使用两个指针遍历二叉搜索树：一个指针（例如 `current`）用于检查当前节点，另一个指针（例如 `trailCurrent`）指向 `current` 的父节点。由于不允许重复项，搜索必须在空子树处结束。随后可以使用指针 `trailCurrent` 将新项插入适当的位置。要插入的项 `insertItem` 作为参数传递给函数 `insert`。通用算法如下：

- a. 创建一个新节点，并将 `insertItem` 复制到该节点中。同时，将新节点的 `LLink` 和 `RLink` 设为 `NULL`。
- b. 如果 `root` 为 `NULL`，则树为空，因此令 `root` 指向新节点。
  否则
  {
      current = root;
      当 `current` 不为 `NULL` 时    //搜索二叉树


