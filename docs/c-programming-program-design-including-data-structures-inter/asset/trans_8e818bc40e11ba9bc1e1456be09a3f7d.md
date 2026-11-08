

```text
{
    trailCurrent = current;
    if (current->info is the same as the insertItem)
        Error: Cannot insert duplicate
        exit
    else
        if (current->info > insertItem)
            Follow lLink of current
        else
            Follow rLink of current
}

//insert the new node in the binary tree

if (trailCurrent->info > insertItem)
    make the new node the left child of trailCurrent
else
    make the new node the right child of trailCurrent
}
```

这段伪代码算法转换为以下 C++ 函数：

```cpp
template <class elemType>
void SearchTreeType<elemType>::insert
                    (const elemType& insertItem)
{
    nodeType<elemType> *current; //pointer to traverse the tree
    nodeType<elemType> *trailCurrent; //pointer behind current
    nodeType<elemType> *newNode; //pointer to create the node

    newNode = new nodeType<elemType>;
    newNode->info = insertItem;
    newNode->lLink = NULL;
    newNode->rLink = NULL;

    if (root == NULL)
        root = newNode;
    else
    {
        current = root;

        while (current != NULL)
        {
            trailCurrent = current;

            if (current->info == insertItem)
            {
                cout << "The item to be inserted is already ";
                cout << "in the tree and duplicates are not "
                     << "allowed." << endl;
                return;
            }
            else if (current->info > insertItem)
                current = current->lLink;
            else
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

和之前一样，首先在二叉搜索树中搜索要删除的节点。为了帮助你更好地理解删除操作，在描述从二叉搜索树中删除一项的函数之前，让我们先考虑图 19-9 中的二叉搜索树。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1374_0.png)

**图 19-9**  删除节点之前的二叉搜索树

删除所需项（如果它存在于二叉搜索树中）后，结果树必须仍是一棵二叉搜索树。删除操作有四种情况，如下：

**情况 1：** 要删除的节点没有左子树和右子树；也就是说，要删除的节点是叶节点。例如，信息为 45 的节点是叶节点。

**情况 2：** 要删除的节点没有左子树；也就是说，左子树为空，但它有一个非空右子树。例如，信息为 40 的节点的左子树为空，而其右子树非空。

**情况 3：** 要删除的节点没有右子树；也就是说，右子树为空，但它有一个非空左子树。例如，信息为 80 的节点的右子树为空，而其左子树非空。

**情况 4：** 要删除的节点具有非空左子树和右子树。例如，信息为 50 的节点的左子树和右子树均非空。

图 19-10 说明了这四种情况。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1375_0.png)

**图 19-10**  删除各种项后的图 19-9 的二叉树

**情况 1：** 假设我们要从图 19-9 的二叉搜索树中删除 45。我们搜索二叉树并到达包含 45 的节点。由于该节点是叶节点且是其父节点的左孩子，我们可以简单地将父节点的 lLink 设置为 NULL，并释放该节点占用的内存。删除该节点后，图 19-10(a) 显示了结果二叉搜索树。

**情况 2：** 假设我们要从图 19-9 的二叉搜索树中删除 30。在这种情况下，要删除的节点没有左子树。由于 30 是其父节点的左孩子，我们使父节点的 lLink 指向 30 的右孩子，然后释放 30 占用的内存。图 19-10(b) 显示了结果二叉树。

**情况 3：** 假设我们要从图 19-9 的二叉搜索树中删除 80。包含 80 的节点没有右孩子，并且是其父节点的右孩子。因此，我们使 80 的父节点——即 70——的 rLink 指向 80 的左孩子。图 19-10(c) 显示了结果二叉树。

**情况 4：** 假设我们要从图 19-9 的二叉搜索树中删除 50。信息为 50 的节点具有非空左子树和非空右子树。这里，我们首先按如下方式将此情况归约为情况 2 或情况 3。具体来说，假设我们将其归约为情况 3——即要删除的节点没有右子树。对于这种情况，我们在此二叉树中找到 50 的直接前驱，即 48。做法是先转到 50 的左孩子，然后定位 50 的左子树中最右侧的节点。为此，我们沿着节点的 rLink 前进。由于二叉搜索树是有限的，我们最终会到达一个没有右子树的节点。接下来，我们将待删除节点中的信息与其直接前驱的信息交换。在此情况下，我们交换 48 与 50。这便归约为待删除节点没有右子树的情况。现在我们应用情况 3 来删除该节点。（注意：由于我们能够从二叉搜索树中找到直接前驱，实际上我们只将直接前驱的信息复制到待删除节点中。）从图 19-9 的二叉搜索树中删除 50 后，结果二叉树如图 19-10(d) 所示。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1376_0.png)

在每种情况下，我们都能清楚地看到，结果二叉树仍然是一棵二叉搜索树。由上述讨论可知，要从二叉搜索树中删除一项，我们必须执行以下操作：

- 1. 找到包含待删除项（如果存在）的节点。
- 2. 删除该节点。

我们通过一个单独的函数来完成第二步，我们将该函数称为 deleteFromTree。给定指向待删除节点的指针，该函数会考虑前面四种情况来删除该节点。

从前面的示例可以清楚地看出，每当我们从二叉树中删除一个节点时，我们都会调整父节点的一个指针。由于调整必须在父节点中进行，我们必须使用父节点的适当指针来调用函数 deleteFromTree。例如，假设要删除的节点是 35，它是其父节点的右孩子。假设 trailCurrent 指向包含 30 的节点，即 35 的父节点。对函数 deleteFromTree 的调用为：

```cpp
deleteFromTree(trailCurrent->rLink);
```

当然，如果要删除的节点是根节点，那么对函数 `deleteFromTree` 的调用为：

`deleteFromTree(root);`

现在定义 C++ 函数 `deleteFromTree`。

```cpp
template <class elemType>
void SearchTreeType<elemType>::deleteFromTree
                                      (nodeType<elemType>* &p)
{
    nodeType<elemType> *current;    //pointer to traverse the tree
    nodeType<elemType> *trailCurrent;   //pointer behind current
    nodeType<elemType> *temp;       //pointer to delete the node

    if (p == NULL)
        cout << "Error: The node to be deleted is NULL."
             << endl;
    else if (p->lLink == NULL && p->rLink == NULL)
    {
        temp = p;
        p = NULL;
        delete temp;
    }
    else if (p->lLink == NULL)
    {
        temp = p;
        p = temp->rLink;
        delete temp;
    }
    else if (p->rLink == NULL)
    {
        temp = p;
        p = temp->lLink;
        delete temp;
    }
    else
    {
        current = p->lLink;
        trailCurrent = NULL;

        while (current->rLink != NULL)
        {
            trailCurrent = current;
            current = current->rLink;
        } //end while

        p->info = current->info;

        if (trailCurrent == NULL) //current did not move;
            //current == p->lLink; adjust p
            p->lLink = current->lLink;
```

