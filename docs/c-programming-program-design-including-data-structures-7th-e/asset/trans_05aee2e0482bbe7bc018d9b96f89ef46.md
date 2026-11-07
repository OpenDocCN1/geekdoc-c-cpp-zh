
- iii. 根节点中的键大于左子树中的每个键，并且小于右子树中的每个键；并且
- iv. $L_T$ 和 $R_T$ 是二叉搜索树。

通常对二叉搜索树执行以下操作。

- 1. 判断二叉搜索树是否为空。
- 2. 在二叉搜索树中查找特定项。
- 3. 在二叉搜索树中插入一项。
- 4. 从二叉搜索树中删除一项。
- 5. 求二叉搜索树的高度。
- 6. 求二叉搜索树中的节点数。
- 7. 求二叉搜索树中的叶子数。
- 8. 遍历二叉搜索树。
- 9. 复制二叉搜索树。

显然，每棵二叉搜索树都是一棵二叉树。二叉搜索树的高度的确定方式与二叉树的高度相同。类似地，求节点数、求叶子数，以及对二叉搜索树进行中序、前序和后序遍历的操作，都与二叉树的相应操作相同。因此，我们可以从二叉树继承所有这些操作。也就是说，我们可以利用继承原理扩展二叉树的定义，从而定义二叉搜索树。

下面的类通过扩展二叉树的定义，将二叉搜索树定义为一种 ADT：

```cpp
template <class elemType>
class binarySearchTreeType: public binaryTreeType<elemType>
{
public:
    bool search(const elemType& searchItem) const;
    //Function to determine if searchItem is in the binary
    //              search tree.
    //Postcondition: Returns true if searchItem is found in
    //              the binary search tree; otherwise,
    //              returns false.
    //
    void insert(const elemType& insertItem);
    //Function to insert insertItem in the binary search tree.
    //Postcondition: If there is no node in the binary search
    //              tree that has the same info as
    //              insertItem, a node with the info
    //              insertItem is created and inserted in the
    //              binary search tree.

    void deleteNode(const elemType& deleteItem);
    //Function to delete deleteItem from the binary search tree.
    //Postcondition: If a node with the same info as deleteItem
    //              is found, it is deleted from the binary
    //              search tree.
    //              If the binary tree is empty or deleteItem
    //              is not in the binary tree, an appropriate
    //              message is printed.

private:
    void deleteFromTree(nodeType<elemType>* &p);
        //Function to delete the node to which p points is
        //deleted from the binary search tree.
        //Postcondition: The node to which p points is deleted
        //              from the binary search tree.
};
```

我们将其留作练习：画出类 bSearchTreeType 的 UML 类图以及继承层次结构。参见本章末尾的练习 34。

接下来，我们描述这些操作中的每一个。

## 查找

函数 search 在二叉搜索树中查找给定项。如果在二叉搜索树中找到该项，则返回 true；否则返回 false。由于指针 root 指向二叉搜索树的根节点，我们必须从根节点开始查找。此外，由于 root 必须始终指向根节点，我们需要一个指针——比如 current——来遍历二叉搜索树。指针 current 初始化为 root。

如果二叉搜索树非空，我们首先将查找项与根节点中的 info 进行比较。如果它们相同，则停止查找并返回 true。否则，如果查找项小于该节点中的 info，则沿 lLink 进入左子树；否则，沿 rLink 进入右子树。我们对下一个节点重复此过程。如果查找项在二叉搜索树中，则查找结束于包含该查找项的节点；否则，查找结束于空子树。因此，一般算法为：

```text
if root is nullptr
    Cannot search an empty tree, returns false.
else
{
    current = root;
    while (current is not nullptr and not found)
        if (current->info is the same as the search item)
            set found to true
        else
            if (current->info is greater than the search item)
                follow the lLink of current
            else
                follow the rLink of current
}
```

```text
{
        trailCurrent = current;
        if (current->info is the same as the insertItem)
                Error: Cannot insert duplicate
                exit
        else
                if (current->info > insertItem)
                        Follow LLink of current
                else
                        Follow RLink of current
}

//insert the new node in the binary tree

if (trailCurrent->info > insertItem)
        make the new node the left child of trailCurrent
else
        make the new node the right child of trailCurrent
}
```

该伪代码算法转换为以下 C++ 函数：

```cpp
template <class elemType>
void bSearchTree<elemType>::insert
                         (const elemType& insertItem)
{
        nodeType<elemType> *current;    //pointer to traverse the tree
        nodeType<elemType> *trailCurrent; // pointer behind current
        nodeType<elemType> *newNode;     //pointer to create the node

        newNode = new nodeType<elemType>;
        newNode->info = insertItem;
        newNode->lLink = nullptr;
        newNode->rLink = nullptr;

        if (root == nullptr)
                root = newNode;
        else
        {
                current = root;

                while (current != nullptr)
                {
                        trailCurrent = current;

                        if (current->info == insertItem)
                        {
                                cout << "The item to be inserted is already ";
                                cout << "in the tree -- duplicates are not ";
                                cout << "allowed." << endl;
                                return;
                        }
                        else if (current->info > insertItem)
                                current = current->lLink;
                        else
                                current = current->rLink;
                } //end while

                if (trailCurrent->info > insertItem)
                    trailCurrent->lLink = newNode;
                else
                    trailCurrent->rLink = newNode;
        }
}//end insert
```

## 删除

和之前一样，首先在二叉搜索树中查找要删除的节点。为了帮助你更好地理解删除操作，在描述从二叉搜索树中删除项的函数之前，让我们考虑图 19–9 中的二叉搜索树。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1423_0.png)

**图 19-9**  删除节点之前的二叉搜索树

删除所需项（如果它存在于二叉搜索树中）之后，结果树必须是一棵二叉搜索树。删除操作有以下四种情况：

- **情况 1：** 要删除的节点没有左子树和右子树；也就是说，要删除的节点是叶子。例如，info 为 45 的节点是叶子。

- **情况 2：** 要删除的节点没有左子树；也就是说，左子树为空，但它有一个非空右子树。例如，info 为 40 的节点的左子树为空，其右子树非空。

- **情况 3：** 要删除的节点没有右子树；也就是说，右子树为空，但它有一个非空左子树。例如，info 为 80 的节点的右子树为空，其左子树非空。

- **情况 4：** 要删除的节点具有非空左子树和右子树。例如，info 为 50 的节点的左子树和右子树都非空。

图 19-10 说明了这四种情况。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1424_0.png)

**图 19-10**  删除各种项之后的图 19-9 中的二叉树

