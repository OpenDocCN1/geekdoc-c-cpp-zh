
```cpp
        current = current->rLink;
    }//end while

    if (trailCurrent->info > insertItem)
        trailCurrent->lLink = newNode;
    else
        trailCurrent->rLink = newNode;
}
}//end insert
```

## 删除

和之前一样，首先在二叉搜索树中搜索要删除的节点。为了帮助你更好地理解删除操作，在描述从二叉搜索树中删除项的函​​数之前，让我们先考虑图 19-9 中的二叉搜索树。

![](img/b217c421655b51e7494cf3b89bb5432d_1436_0.png)

**图 19-9**  删除节点前的二叉搜索树

删除所需项（如果它存在于二叉搜索树中）后，得到的树必须仍然是二叉搜索树。删除操作有以下四种情况：

- **情况 1：** 要删除的节点没有左子树和右子树；也就是说，要删除的节点是叶节点。例如，信息为 45 的节点是叶节点。
- **情况 2：** 要删除的节点没有左子树；也就是说，左子树为空，但它有一个非空的右子树。例如，信息为 40 的节点的左子树为空，而其右子树非空。
- **情况 3：** 要删除的节点没有右子树；也就是说，右子树为空，但它有一个非空的左子树。例如，信息为 80 的节点的右子树为空，而其左子树非空。
- **情况 4：** 要删除的节点具有非空的左子树和右子树。例如，信息为 50 的节点的左子树和右子树都非空。

图 19-10 展示了这四种情况。

![](img/b217c421655b51e7494cf3b89bb5432d_1437_0.png)

**图 19-10**  删除不同项后图 19-9 的二叉树

**情况 1：** 假设我们要从图 19-9 的二叉搜索树中删除 45。我们搜索二叉树并到达包含 45 的节点。由于该节点是叶节点，并且是其父节点的左子节点，我们可以简单地将父节点的 `lLink` 设置为 `nullptr`，并释放该节点占用的内存。删除该节点后，图 19-10(a) 显示了得到的二叉搜索树。

**情况 2：** 假设我们要从图 19-9 的二叉搜索树中删除 30。在这种情况下，要删除的节点没有左子树。由于 30 是其父节点的左子节点，我们将父节点的 `lLink` 指向 30 的右子节点，然后释放 30 占用的内存。图 19-10(b) 显示了得到的二叉树。

**情况 3：** 假设我们要从图 19-9 的二叉搜索树中删除 80。包含 80 的节点没有右子节点，并且是其父节点的右子节点。因此，我们将 80 的父节点——即 70——的 `rLink` 指向 80 的左子节点。图 19-10(c) 显示了得到的二叉搜索树。

**情况 4：** 假设我们要从图 19-9 的二叉搜索树中删除 50。信息为 50 的节点有一个非空左子树和一个非空右子树。这里，我们首先按如下方式将此情况归约为情况 2 或情况 3。更准确地说，假设我们将其归约为情况 3——即要删除的节点没有右子树。对于这种情况，我们在此二叉树中找到 50 的直接前驱，即 48。具体做法是先转到 50 的左子节点，然后定位 50 的左子树中最右侧的节点。为此，我们沿着节点的 `rLink` 前进。由于二叉搜索树是有限的，我们最终会到达一个没有右子树的节点。接下来，我们将要删除节点中的信息与其直接前驱的信息交换。在这种情况下，我们交换 48 与 50。这归约为要删除的节点没有右子树的情况。现在我们应用情况 3 删除该节点。（注意：由于我们将从二叉树中删除直接前驱，实际上我们只将直接前驱的信息复制到要删除的节点中。）从图 19-9 的二叉搜索树中删除 50 后，得到的二叉树如图 19-10(d) 所示。

在每种情况下，我们都能清楚地看到，得到的二叉树仍然是二叉搜索树。由以上讨论可知，要从二叉搜索树中删除一项，必须执行以下操作：

1. 找到包含要删除项（如果存在）的节点。
2. 删除该节点。

我们通过一个单独的函数完成第二步，该函数称为 `deleteFromTree`。给定指向要删除节点的指针，该函数会考虑前面四种情况来删除节点。

从前面的示例可以清楚地看出，每当我们从二叉树中删除一个节点时，都要调整父节点的一个指针。由于调整必须在父节点中进行，我们必须使用父节点的适当指针调用函数 `deleteFromTree`。例如，假设要删除的节点是 35，它是其父节点的右子节点。假设 `trailCurrent` 指向包含 30 的节点，即 35 的父节点。对函数 `deleteFromTree` 的调用为

`deleteFromTree(trailCurrent->rLink);`

当然，如果要删除的节点是根节点，那么对函数 `deleteFromTree` 的调用为

`deleteFromTree(root);`

现在，我们如下定义 C++ 函数 `deleteFromTree`：

```cpp
template <class elemType>
void binarySearchTree<elemType>::deleteFromTree
                              (nodeType<elemType>* &p)
{
    nodeType<elemType> *current;   //pointer to traverse the tree
    nodeType<elemType> *trailCurrent;   //pointer behind current
    nodeType<elemType> *temp;      //pointer to delete the node

    if (p == nullptr)
        cout << "Error: The node to be deleted does not exist."
             << endl;
    else if (p->lLink == nullptr && p->rLink == nullptr)
    {
        temp = p;
        p = nullptr;
        delete temp;
    }
    else if (p->lLink == nullptr)
    {
        temp = p;
        p = temp->rLink;
        delete temp;
    }
    else if (p->rLink == nullptr)
    {
        temp = p;
        p = temp->lLink;
        delete temp;
    }
    else
    {
        current = p->lLink;
        trailCurrent = nullptr;

        while (current->rLink != nullptr)
        {
            trailCurrent = current;
            current = current->rLink;
        }//end while

        p->info = current->info;

        if (trailCurrent == nullptr) //current did not move;
                                     //current == p->lLink; adjust p
            p->lLink = current->lLink;
        else
            trailCurrent->rLink = current->rLink;

        delete current;
    } //end else
} //end deleteFromTree
```

接下来，我们描述函数 `deleteNode`。函数 `deleteNode` 首先搜索二叉搜索树，以找到包含要删除项的节点。要删除的项 `deleteItem` 作为参数传递给该函数。如果在二叉搜索树中找到包含 `deleteItem` 的节点，函数 `deleteNode` 会调用函数 `deleteFromTree` 来删除该节点。函数 `deleteNode` 的定义如下。

```cpp
template <class elemType>
void binarySearchTree<elemType>::deleteNode
                                      (const elemType deleteItem)
{
    nodeType<elemType> *current; //pointer to traverse the tree
    nodeType<elemType> *trailCurrent; // pointer behind current
    bool found = false;

    if (root == nullptr)
        cout << "Cannot delete from an empty tree."
             << endl;
    else
    {
        current = root;
        trailCurrent = root;

        while (current != nullptr && !found)
        {
            if (current->info == deleteItem)
                found = true;
            else
            {
                trailCurrent = current;
                if (current->info > deleteItem)
                    current = current->lLink;
                else
                    current = current->rLink;
            }
        } //end while

        if (current == nullptr)
            cout << "The item to be deleted is not in the tree."
                 << endl;
```
