
> 注意
>
> 除了中序、前序和后序遍历之外，二叉树还可以**逐层**遍历，也称为**广度优先遍历**。在第20章中，我们讨论图。二叉树也是一种图。我们讨论如何为图实现广度优先遍历算法。你可以修改该算法，以对二叉树进行广度优先遍历。

## 实现二叉树

前面几节描述了可以对二叉树执行的各种操作，以及实现这些操作的函数。本节将二叉树描述为抽象数据类型（ADT）。在设计将二叉树实现为 ADT 的类之前，让我们列出通常对二叉树执行的各种操作。

- 1. 判断二叉树是否为空。
- 2. 在二叉树中搜索特定项。
- 3. 在二叉树中插入一项。
- 4. 从二叉树中删除一项。
- 5. 求二叉树的高度。
- 6. 求二叉树中的节点数。
- 7. 求二叉树中的叶子数。
- 8. 遍历二叉树。
- 9. 复制二叉树。

项搜索、插入和删除操作都需要遍历二叉树。然而，由于二叉树的节点没有特定顺序，这些算法在任意二叉树上效率不高。也就是说，不存在指导在这些二叉树上进行搜索的标准，正如我们将在下一节中看到的。因此，我们将在讨论特殊二叉树时讨论这些算法。

下面的类将二叉树定义为 ADT。节点的定义与前面相同。然而，为了完整性和便于参考，我们先给出节点的定义，然后给出类的定义：

```cpp
//Definition of the Node
template <class elemType>
struct nodeType
{
    elemType info;
    nodeType<elemType> *lLink;
    nodeType<elemType> *rLink;
};
```

```cpp
//Definition of the class
template <class elemType>
class binaryTreeType
{
public:
    const binaryTreeType<elemType>& operator=
                 (const binaryTreeType<elemType>&);
       //Overload the assignment operator.

    bool isEmpty() const;
       //Function to determine whether the binary tree is empty.
       //Postcondition: Returns true if the binary tree is empty;
       //               otherwise, returns false.

    void inorderTraversal() const;
       //Function to do an inorder traversal of the binary tree.
       //Postcondition: Nodes are printed in inorder sequence.

    void preorderTraversal() const;
       //Function to do a preorder traversal of the binary tree.
       //Postcondition: Nodes are printed in preorder sequence.

    void postorderTraversal() const;
       //Function to do a postorder traversal of the binary tree.
       //Postcondition: Nodes are printed in postorder sequence.

    int treeHeight() const;
       //Function to determine the height of a binary tree.
       //Postcondition: Returns the height of the binary tree.

    int treeNodeCount() const;
       //Function to determine the number of nodes in a
       //binary tree.
       //Postcondition: Returns the number of nodes in the
       //               binary tree.

    int treeLeavesCount() const;
       //Function to determine the number of leaves in a
       //binary tree.
       //Postcondition: Returns the number of leaves in the
       //               binary tree.

    void destroyTree();
       //Function to destroy the binary tree.
       //Postcondition: Memory space occupied by each node
       //               is deallocated.
       //               root = nullptr;

    virtual bool search(const elemType& searchItem) const = 0;
       //Function to determine if searchItem is in the binary
       //tree.
       //Postcondition: Returns true if searchItem is found in
       //               the binary tree; otherwise, returns
       //               false.

    virtual void insert(const elemType& insertItem) = 0;
    //Function to insert insertItem in the binary tree.
    //Postcondition: If there is no node in the binary tree
    //              that has the same info as insertItem, a
    //              node with the info insertItem is created
    //              and inserted in the binary search tree.

    virtual void deleteNode(const elemType& deleteItem) = 0;
    //Function to delete deleteItem from the binary tree.
    //Postcondition: If a node with the same info as
    //              deleteItem is found, it is deleted from
    //              the binary tree.
    //              If the binary tree is empty or
    //              deleteItem is not in the binary tree,
    //              an appropriate message is printed.

    binaryTreeType(const binaryTreeType<elemType>& otherTree);
    //Copy constructor

    binaryTreeType();
    //Default constructor

    ~binaryTreeType();
    //Destructor

protected:
    nodeType<elemType> *root;

private:
    void copyTree(nodeType<elemType>* copiedTreeRoot,
                  nodeType<elemType>*& otherTreeRoot);
    //Makes a copy of the binary tree to which
    //otherTreeRoot points.
    //Postcondition: The pointer copiedTreeRoot points to
    //              the root of the copied binary tree.

    void destroy(nodeType<elemType>*& p);
    //Function to destroy the binary tree to which p points.
    //Postcondition: Memory space occupied by each node, in
    //              the binary tree to which p points, is
    //              deallocated.
    //              p = nullptr;

    void inorder(nodeType<elemType> *p) const;
    //Function to do an inorder traversal of the binary
    //tree to which p points.
    //Postcondition: Nodes of the binary tree, to which p
    //              points, are printed in inorder sequence.

    void preorder(nodeType<elemType> *p) const;
    //Function to do a preorder traversal of the binary
    //tree to which p points.
    //Postcondition: Nodes of the binary tree, to which p
    //              points, are printed in preorder
    //              sequence.

    void postorder(nodeType<elemType> *p) const;
    //Function to do a postorder traversal of the binary
    //tree to which p points.
    //Postcondition: Nodes of the binary tree, to which p
    //              points, are printed in postorder
    //              sequence.

    int height(nodeType<elemType> *p) const;
    //Function to determine the height of the binary tree
    //to which p points.
    //Postcondition: Height of the binary tree to which
    //              p points is returned.

    int max(int x, int y) const;
    //Function to determine the larger of x and y.
    //Postcondition: Returns the larger of x and y.

    int nodeCount(nodeType<elemType> *p) const;
    //Function to determine the number of nodes in
    //the binary tree to which p points.
    //Postcondition: The number of nodes in the binary
    //              tree to which p points is returned.
    int leavesCount(nodeType<elemType> *p) const;
    //Function to determine the number of leaves in
    //the binary tree to which p points.
    //Postcondition: The number of leaves in the binary
    //              tree to which p points is returned.
};
```

我们将类 `binaryTreeType` 的 UML 类图留作练习。参见本章末尾的练习33。

函数 search、insert 和 deleteNode 在类 `binaryTreeType` 的定义中被声明为抽象函数。这是因为在本节中，我们讨论的是任意二叉树。对于任意二叉树，实现这些操作效率不高，甚至可能无法实现，正如我们将在“二叉搜索树”一节中讨论的那样。由于类 `binaryTreeType` 包含抽象函数，因此该类是抽象类。所以，你不能创建该类的对象。在“二叉搜索树”一节中，我们将从类 `binaryTreeType` 派生一个类，并提供这些函数的定义。

注意，类 `binaryTreeType` 的定义包含重载赋值运算符、复制构造函数和析构函数的语句。这是因为类 `binaryTreeType` 包含指针成员变量。回想一下，对于带指针成员变量的类，我们必须显式重载赋值运算符、包含复制构造函数并包含析构函数。

类 `binaryTreeType` 的定义包含若干作为该类私有成员的成员函数。这些函数用于实现该类的公有成员函数。例如，为了进行中序遍历，函数 inorderTraversal 调用函数 inorder，并将指针 root 作为参数传递给该函数。此外，指针 root 被声明为保护成员，以便我们以后可以派生特殊的二叉树。
