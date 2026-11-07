

- ii. $T$ 有两组节点 $L_T$ 和 $R_T$，分别称为 $T$ 的左子树和右子树；
- iii. 根节点中的键大于左子树中的每个键，并且小于右子树中的每个键；以及
- iv. $L_T$ 和 $R_T$ 都是二叉搜索树。

通常会对二叉搜索树执行以下操作：

- 1. 确定二叉搜索树是否为空。
- 2. 在二叉搜索树中搜索特定项。
- 3. 在二叉搜索树中插入一个项。
- 4. 从二叉搜索树中删除一个项。
- 5. 查找二叉搜索树的高度。
- 6. 查找二叉搜索树中的节点数。
- 7. 查找二叉搜索树中的叶节点数。
- 8. 遍历二叉搜索树。
- 9. 复制二叉搜索树。

显然，每棵二叉搜索树都是一棵二叉树。二叉搜索树的高度与二叉树的高度采用相同的确定方法。同样，查找节点数、查找叶节点数，以及对二叉搜索树进行中序、前序和后序遍历的操作，也都与二叉树的相应操作相同。因此，我们可以从二叉树继承所有这些操作。也就是说，我们可以利用继承原则扩展二叉树的定义，从而定义二叉搜索树。

下面的类通过扩展二叉树的定义，将二叉搜索树定义为一种 ADT：

```cpp
template <class elemType>
class BinarySearchTreeType: public binaryTreeType<elemType>
{
public:
    bool search(const elemType& searchItem) const;
        //Function to determine if searchItem is in the binary
        //search tree.
        //Postcondition: Returns true if searchItem is found in
        //               the binary search tree; otherwise,
        //               returns false.

    void insert(const elemType& insertItem);
        //Function to insert insertItem in the binary search tree.
        //Postcondition: If there is no node in the binary search
        //               tree that has the same info as
        //               insertItem, a node with the info
        //               insertItem is created and inserted in the
        //               binary search tree.

    void deleteNode(const elemType& deleteItem);
        //Function to delete deleteItem from the binary search tree
        //Postcondition: If a node with the same info as
        //               deleteItem is found, it is deleted from
        //               the binary search tree.
        //               If the binary tree is empty or deleteItem
        //               is not in the binary tree, an appropriate
        //               message is printed.

    private:
        void deleteFromTree(nodeType<elemType>*& p);
            //Function to delete the node to which p points is
            //deleted from the binary search tree.
            //Postcondition: The node to which p points is
            //               deleted from the binary search tree.
};
```

我们将类 BinarySearchTreeType 的 UML 类图以及继承层次结构留作练习，具体参见本章末尾的练习 34。接下来，我们将介绍这些操作中的每一个。

### 搜索

函数 search 在二叉搜索树中搜索给定项。如果在二叉搜索树中找到该项，则返回 true；否则返回 false。由于指针 root 指向二叉搜索树的根节点，因此我们必须从根节点开始搜索。此外，由于 root 必须始终指向根节点，所以需要使用一个指针（例如 current）来遍历二叉搜索树。指针 current 被初始化为 root。

如果二叉搜索树非空，我们首先将搜索项与根节点中的信息进行比较。如果二者相同，则停止搜索并返回 true。否则，如果搜索项小于该节点中的信息，则沿着 lLink 进入左子树；否则，沿着 rLink 进入右子树。对于下一个节点，我们重复这一过程。如果搜索项位于二叉搜索树中，搜索将在包含该搜索项的节点处结束；否则，搜索将在一棵空子树处结束。因此，通用算法如下：

```
if root is nullptr
    Cannot search an empty tree, returns false.
else
{
    current = root;
    while (current is not nullptr and not found)
        if (current->info is the same as the search item)
            set found to true;
        else
            if (current->info is greater than the search item)
                follow the lLink of current
            else
                follow the rLink of current
}
```

该伪代码算法转换为以下 C++ 函数：

```cpp
template <class elemType>
bool BinarySearchTreeType<elemType>::search
                      (const elemType& searchItem) const
{
    nodeType<elemType> *current;
    bool found = false;

    if (root == nullptr)
        cout << "Cannot search an empty tree." << endl;
    else
    {
        current = root;

        while (current != nullptr && !found)
        {
            if (current->info == searchItem)
                found = true;
            else if (current->info > searchItem)
                current = current->lLink;
            else
                current = current->rLink;
        }//end while
    }//end else

    return found;
}//end search
```

### 插入

在二叉搜索树中插入一个项后，生成的二叉树必须仍然是一棵二叉搜索树。要插入一个新项，首先要搜索二叉搜索树，找到应插入新项的位置。搜索算法与函数 search 的搜索算法相似。在这里，我们使用两个指针遍历二叉搜索树：一个指针（例如 current）用于检查当前节点，另一个指针（例如 trailCurrent）指向 current 的父节点。由于不允许重复项，因此搜索必须在一棵空子树处结束。然后，我们可以使用指针 trailCurrent 在适当的位置插入新项。要插入的项 insertItem 作为参数传递给函数 insert。通用算法如下：

- a. 创建一个新节点，并将 `insertItem` 复制到新节点中。同时，将新节点的 `lLink` 和 `rLink` 设置为 `nullptr`。
- b. 如果 root 为 `nullptr`，则树为空，因此让 root 指向新节点。

```cpp
else
{
    current = root;
    while (current is not nullptr) //search the binary tree
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

该伪代码算法转换为以下 C++ 函数：

```cpp
template <class elemType>
void BinarySearchTreeType<elemType>::insert
                (const elemType& insertItem)
{
    nodeType<elemType> *current; //pointer to traverse the tree
    nodeType<elemType> *trailCurrent = nullptr; //pointer behind current
    nodeType<elemType> *newNode; //pointer to create the node

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
```

