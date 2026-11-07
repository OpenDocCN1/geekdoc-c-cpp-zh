

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

该伪代码算法对应以下 C++ 函数：

```cpp
template <class elemType>
void SearchTree<elemType>::insert
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
                cout << "in the tree -- duplicates are not "
                     << "allowed." << endl;
                return;
            }
            else if (current->info > insertItem)
                current = current->lLink;
            else
                current = current->rLink;
        }//end while
```

**情况 1：** 假设我们要从图 20–9 的二叉搜索树中删除 45。我们搜索二叉树并到达包含 45 的节点。由于该节点是叶节点，并且是其父节点的左孩子，我们可以简单地将父节点的 lLink 设置为 NULL，并释放该节点占用的内存。删除该节点后，图 20–10(a) 显示了所得的二叉搜索树。

**情况 2：** 假设我们要从图 20–9 的二叉搜索树中删除 30。在这种情况下，要删除的节点没有左子树。由于 30 是其父节点的左孩子，我们让父节点的 lLink 指向 30 的右孩子，然后释放 30 占用的内存。图 20–10(b) 显示了所得的二叉树。

**情况 3：** 假设我们要从图 20–9 的二叉搜索树中删除 80。包含 80 的节点没有右孩子，并且是其父节点的右孩子。因此，我们让 80 的父节点（即 70）的 rLink 指向 80 的左孩子。图 20–10(c) 显示了所得的二叉树。

**情况 4：** 假设我们要从图 20–9 的二叉搜索树中删除 50。info 为 50 的节点具有非空左子树和非空右子树。这里，我们首先按如下方式将此情况归约为情况 2 或情况 3。具体来说，假设我们将其归约为情况 3——即要删除的节点没有右子树。对于这种情况，我们在此二叉树中找到 50 的直接前驱，即 48。具体做法是先转到 50 的左孩子，然后定位 50 的左子树中最右的节点。为此，我们沿着节点的 rLink 前进。由于二叉搜索树是有限的，我们最终会到达一个没有右子树的节点。接下来，我们将要删除节点中的 info 与其直接前驱的 info 交换。在这种情况下，我们交换 48 与 50。这就归约为要删除的节点没有右子树的情况。现在我们应用情况 3 来删除该节点。（注意，由于我们将从二叉树中删除直接前驱，因此实际上我们只是将直接前驱的 info 复制到要删除的节点中。）从图 20–9 的二叉搜索树中删除 50 后，所得的二叉树如图 20–10(d) 所示。

在每种情况下，我们都能清楚地看到，所得的二叉树仍然是一棵二叉搜索树。由上述讨论可知，要从二叉搜索树中删除一个项，我们必须执行以下操作：

- 1. 找到包含要删除项（如果存在）的节点。
- 2. 删除该节点。

我们通过一个单独的函数来完成第二步，我们将其称为 deleteFromTree。给定指向要删除节点的指针，该函数会考虑前面的四种情况来删除该节点。

从上述示例可以清楚地看出，每当我们从二叉树中删除一个节点时，我们都会调整父节点的某个指针。由于调整必须在父节点中进行，我们必须使用父节点的适当指针来调用函数 deleteFromTree。例如，假设要删除的节点是 35，它是其父节点的右孩子。假设 trailCurrent 指向包含 30 的节点，即 35 的父节点。对函数 deleteFromTree 的调用为：

```cpp
deleteFromTree(trailCurrent->rLink);
```

当然，如果要删除的节点是根节点，那么对函数 `deleteFromTree` 的调用为：

`deleteFromTree(root);`

现在我们定义 C++ 函数 `deleteFromTree`。

```cpp
template <class elemType>
void SearchTree<elemType>::deleteFromTree
                                      (nodeType<elemType>* &p)
{
    nodeType<elemType>* current;   //pointer to traverse the tree
    nodeType<elemType>* trailCurrent;  //pointer behind current
    nodeType<elemType>* temp;       //pointer to delete the node

    if (p == NULL)
    {
        cout << "Error: The node to be deleted is NULL."
             << endl;
    }
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
        }//end while

        p->info = current->info;

        if (trailCurrent == NULL) //current did not move;
                                  //current == p->lLink; adjust p
            p->lLink = current->lLink;
        else
            trailCurrent->rLink = current->lLink;

        delete current;
    }//end else
} //end deleteFromTree
```

接下来，我们描述函数 `deleteNode`。函数 `deleteNode` 首先搜索二叉搜索树，以找到包含要删除项的节点。要删除的项 `deleteItem` 作为参数传递给该函数。如果在二叉搜索树中找到包含 `deleteItem` 的节点，则函数 `deleteNode` 调用函数 `deleteFromTree` 来删除该节点。函数 `deleteNode` 的定义如下。

```cpp
template <class elemType>
void bSearchTreeType<elemType>::deleteNode
                         (const elemType& deleteItem)
{
    nodeType<elemType> *current; //pointer to traverse the tree
    nodeType<elemType> *trailCurrent; //pointer behind current
    bool found = false;

    if (root == NULL)
        cout << "Cannot delete from an empty tree."
             << endl;
    else
    {
        current = root;
        trailCurrent = root;

        while (current != NULL && !found)
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
        }//end while

        if (current == NULL)
            cout << "The item to be deleted is not in the tree."
                 << endl;
        else if (found)
        {
            if (current == root)
                deleteFromTree(root);
```

