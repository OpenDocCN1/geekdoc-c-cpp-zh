
## 程序 18.15 二叉搜索树的实现文件（续）

```cpp
// Insert member function
template <class T>
void BinarySearchTree<T>::insert(const T& value)
{
    insert(value, root);
    count++;
}

// Search member function
template <class T>
bool BinarySearchTree<T>::search(const T& value) const
{
    return search(value, root);
}

// Preorder traversal function
template <class T>
void BinarySearchTree<T>::preorder() const
{
    preorder(root);
}

// Inorder traversal function
template <class T>
void BinarySearchTree<T>::inorder() const
{
    inorder(root);
}

// Postorder traversal function
template <class T>
void BinarySearchTree<T>::postorder() const
{
    postorder(root);
}

// Size member function
template <class T>
int BinarySearchTree<T>::size() const
{
    return count;
}

// Empty member function
template <class T>
bool BinarySearchTree<T>::empty() const
{
    return (count == 0);
}

// Recursive helper member function called by the destructor
template <class T>
void BinarySearchTree<T>::destroy(Node<T>* ptr)
{
    if (!ptr)
    {
        return;
    }
    destroy(ptr->left);
    destroy(ptr->right);
    delete ptr;
}

// Recursive helper member function called by insert member function
template <class T>
void BinarySearchTree<T>::insert(const T& value, Node<T>*& ptr)
{
    if (!ptr)
    {
        ptr = makeNode(value);
        return;
    }
    else if (value < ptr->data)
    {
        insert(value, ptr->left);
    }
    else
    {
        insert(value, ptr->right);
    }
}

// Recursive helper member function called by preorder function
template <typename T>
void BinarySearchTree<T>::preorder(Node<T>* ptr) const
{
    if (!ptr)
    {
        return;
    }
    cout << ptr->data << endl;
    preorder(ptr->left);
    preorder(ptr->right);
}

// Recursive helper member function called by the inorder function
template <class T>
void BinarySearchTree<T>::inorder(Node<T>* ptr) const
{
    if (!ptr)
    {
        return;
    }
    inorder(ptr->left);
    cout << ptr->data << endl;
    inorder(ptr->right);
}

// Recursive helper member function called by the postorder function
template <class T>
void BinarySearchTree<T>::postorder(Node<T>* ptr) const
{
    if (!ptr)
    {
        return;
    }
    postorder(ptr->right);
    postorder(ptr->left);
    cout << ptr->data << endl;
}

// Recursive helper member function called by the search function
template <typename T>
bool BinarySearchTree<T>::search(const T& value, Node<T>* ptr) const
{
    if (!ptr)
    {
        return false;
    }
    else if (ptr->data == value)
    {
        return true;
    }
    else if (value < ptr->data)
    {
        return search(value, ptr->left);
    }
    else
    {
        return search(value, ptr->right);
    }
}

// Recursive helper member function called by the makeNode function
template <typename T>
Node<T>* BinarySearchTree<T>::makeNode(const T& value)
{
    Node<T>* temp = new Node<T>;
    temp->data = value;
    temp->left = 0;
    temp->right = 0;
    return temp;
}
#endif
```

**应用文件** 程序 18.16 展示了如何使用实现文件创建二叉搜索树，然后按前序、中序和后序序列打印数据项。注意，只有中序遍历能给出数据值的有序列表（从最小到最大）。另外两种遍历给出树的结构（哪个元素是根，哪些元素在左子树中，哪些元素在右子树中）。

## 程序 18.16 用于测试二叉搜索树的应用文件

```cpp
/****************************************************************
 * The application file that tests the binary search tree class  *
 ****************************************************************/
#include "binarySearchTree.cpp"

int main()
{
    // Instantiation of a binary search tree object
    BinarySearchTree<string> bct;

    // Inserting six nodes in the tree
    bct.insert("Michael");
    bct.insert("Jane");
    bct.insert("Sophie");
    bct.insert("Thomas");
    bct.insert("Rose");
    bct.insert("Richard");

    // Printing values using preorder traversal
    cout << "Using preorder traversal" << endl;
    bct.preorder();
    cout << endl << endl;

    // Printing values using inorder traversal
    cout << "Using inorder traversal" << endl;
    bct.inorder();
    cout << endl << endl;

    // Printing values using postorder traversal
    cout << "Using postorder traversal" << endl;
    bct.postorder();
    cout << endl << endl;
```

## 小结

在计算机科学中，对象通常呈现在集合中：线性和非线性。要实现一个集合，我们通常有两种选择：使用数组或使用链表。

要将容器实现为单链表，我们使用两种不同的对象类型：*列表* 和 *节点*。列表对象在栈内存中实现；节点在堆内存中实现。列表的两种常见适配是栈和队列。*栈* 是一种线性表，其中所有添加和删除都限制在一端，称为 *栈顶*。*队列* 是一种线性表，其中数据只能在一端插入，称为 *队尾*，并从另一端删除，称为 *队头*。

作为非线性集合的一个例子，我们介绍了二叉搜索树，其中左子树中的所有元素的值都小于根，右子树中的所有元素的值都大于根。要使用二叉搜索树，我们需要三种遍历。前序遍历用于创建二叉搜索树。中序遍历用于获取有序列表中节点的值，后序遍历用于在销毁树时删除树中的节点。

## 习题

- **1. PR-1.** 假设我们决定使用如下所示的双向链表（为简单起见只显示三个节点）。给出向空列表添加节点所需的分步操作。

- **2. PR-2.** 对在列表开头插入节点的情况重复 PR-1。

- **3. PR-3.** 对在列表末尾插入节点的情况重复 PR-1。

- **4. PR-4.** 对在中间（第二个和第三个节点之间）添加节点的情况重复 PR-1。

- **5. PR-5.** 使用 PR-1 中的双向链表，说明我们如何删除第一个节点。

- **6. PR-6.** 使用 PR-1 中的双向链表，说明我们如何删除最后一个节点。下面显示了删除链表最后一个节点时的操作及其效果。

![](img/d68f6199646ca63591a6d8419e0ed4ba_868_0.png)

![](img/d68f6199646ca63591a6d8419e0ed4ba_868_1.png)

- **7. PR-7.** 使用 PR-1 中的双向链表，说明我们如何删除中间节点。

- **8. PR-8.** 假设我们有一个包含五个元素的栈。我们需要删除从栈顶数第三个元素。使用另一个栈作为辅助容器展示这些操作。

- **9. PR-9.** 假设我们有一个包含五个元素的队列。我们需要删除第三个元素。我们能否使用另一个队列保存队列前面的两个元素，删除第三个元素，然后再把前面的元素放回？

- **10. PR-10.** 你认为从队列中间删除元素并保持元素原始顺序的解决方案是什么？

- **11. PR-11.** 以下二叉搜索树的前序、中序和后序遍历的输出是什么？

![](img/d68f6199646ca63591a6d8419e0ed4ba_869_0.png)

- **12. PR-12.** 从以下列表创建二叉搜索树。

```text
32 45 47 23 24 41 39 15 26 47
```

## 编程题

- **PRG-1.** 向 *List* 类添加一个 void 尾递归函数和非递归函数，以便我们可以按逆序打印链表的内容。递归函数从第一个节点开始并移动到链表末尾。当它返回时，它打印每个节点的数据值，如下所示。

![](img/d68f6199646ca63591a6d8419e0ed4ba_869_1.png)

- **PRG-2.** 假设我们决定将图 18.4 中的单链表改为如下所示的双向链表。重写并测试接口文件、实现文件和应用程序文件（程序 18.1、18.2 和 18.3），以使用这个新设计。还要说明如何使用这个设计按逆序打印链表。

![](img/d68f6199646ca63591a6d8419e0ed4ba_869_2.png)

- **PRG-3.** 修改程序 18.7，使程序能将任意十进制数转换为等价的二进制数。

- **PRG-4.** 更改程序 18.7 中的代码，使程序能将任意十进制数转换为等价的八进制数。

- **PRG-5.** 使用在堆中创建的数组，重写 *Stack* 类的接口文件、实现文件和应用程序文件。一种方法是使用一个更大的数组和一个索引作为栈顶指示器。

- **PRG-6.** 使用在堆中创建的数组，重写 *Queue* 类的接口文件、实现文件和应用程序文件。一种方法是使用两个索引分别作为队列的队头和队尾。

