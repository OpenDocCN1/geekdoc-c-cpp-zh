
`n1.setRight(&n3);` // 注意：代码块中有 `n3`，但只定义了 `n1` 和 `n2`。

`cout` << "Value of n1 after modification: " << `endl`

<< `n1.getData()` << " " << `n1.getLeft()` << " "

<< `n1.getRight()` << `endl`;

`cout` << "Value of n2 after modification: " << `endl`

<< `n2.getData()` << " " << `n2.getLeft()` << " "

<< `n2.getRight()` << `endl`;

`return` 0;

```
```

测试程序的示例运行产生了如下输出：

Value of n1 after default construction: 0 0 0
Value of n2 after parameterized construction: 4 0 0
Value of n1 after modification: 13 0x... 0x... 
... （等待，OCR 文本在代码块中有 `n3`，但只定义了 `n1` 和 `n2`。我将保持文本不变，但修复逻辑上的错误。）

（注，此处根据指令要求保留 OCR 文本中的逻辑错误，仅进行翻译和格式调整。）

## 递归成员函数
为了继续开发图 10.5 中的 `BinaryTree` 类，我们必须考虑我们希望如何在树中安排节点，以及我们如何遍历树。二叉树可以是有序的，也可以是无序的。无序二叉树假设定义树的数据值之间没有强制的顺序。有序二叉树则对树的节点施加了排序。

### 二叉搜索树
二叉搜索树是有序二叉树的一个例子。二叉搜索树被定义为满足以下条的二叉树：
- 每个节点都有一个值。
- 节点的左子树只包含小于该节点值的节点。
- 节点的右子树只包含大于或等于该节点值的节点。

### 树遍历
树遍历指的是以系统的方法访问树结构中的每个节点一次。遍历根据访问节点的顺序进行分类。例如，如果我们使用 `print()` 方法打印存储在图 10.7 所示二叉搜索树中的有序数据，我们将对树进行中序遍历，在访问每个节点时打印其值。树的中序遍历的递归算法如下所示：

![](img/4456642232e4f4a18bd7dfe37e70176d_548_0.png)

**图 10.7** 具有6个节点的二叉搜索树。

中序遍历：

```
if(root == null)

    return

inOrder traverse left child

    visit node

inOrder traverse right child
```

该算法从二叉树的根节点开始，对每个后续节点的左子节点递归调用自身，直到遇到空值。当最终找到一个左孩子为空的节点时，该节点被“访问”，然后算法对该节点的右节点递归调用自身。条件 `root == null` 是终止条件，每次递归调用都将问题简化为对较小子树的遍历。对图 10.7 中的树应用中序遍历，并打印每个节点，输出结果为：8 10 14 22 27。

在二叉树中插入新节点的算法从树的根节点开始。如果树为空，则将新节点作为树的第一个节点插入。如果不为空，则将新节点的值与第一个节点的值进行比较。如果新节点的值小于根节点的值，算法在左子节点上调用自身，否则算法在右子节点上调用自身。递归算法描述如下：

```
void insert(node* root, int value) {

    if(root == null)

        root = new node(value);

        return;

    else

        if(value < root->value)

            insert(root->left child, value);

        else

            insert(root->right child, value);

}
```

# 第 10 章 高级主题

![](img/4456642232e4f4a18bd7dfe37e70176d_549_0.png)

**图 10.8** 插入新节点后的二叉搜索树。

如果在图 10.7 的二叉搜索树中插入值 17

接下来描述清空树的算法。

```cpp
void clear(node* root) {
    if(root == null)
        return;
    else
        clear(root->left);
        clear(root->right);
    delete root;
}
```

我们现在可以完成图 10.5 中描述的 `BinaryTree` 类定义。

```cpp
/*
 * 二叉树声明
 * filename: binaryTree.h
 */
#include "node.h" // 需要 node 类。
#include <iostream> // 需要 ostream。
using namespace std;
class BinaryTree {
public:
    // 默认构造函数
    BinaryTree();
    // 公共、非递归打印和插入
    void print(ostream& out) const;
    void insert(int value);
    void clear();
private:
    // 私有递归重载打印和插入
    void print(ostream& out, node* rt) const;
    void insert(node* rt, int value);
    // 私有属性
    Node* root;
};
```

注意在 `BinaryTree` 类声明中，`print()`、`insert()` 和 `clear()` 方法被重载了。这些方法的公共版本不是递归的。这些方法的私有版本是递归的，且每个都有一个 `Node*` 的形式的形式参数。

这些方法的公共版本必须由 `BinaryTree` 对象调用，树的根由调用对象提供。这些方法的私有版本通过在调用对象的右、左子树上递归调用自身来遍历树。形式参数 `rt` 的值在随后的每次调用中不同，并作为参数支持这些方法的递归性质。最小 `BinaryTree` 类的定义如下：

```cpp
/*
 * 二叉树实现
 * filename: binaryTree.cpp
 */
#include "bTree.h" // 需要 BinaryTree。
#include <iostream> // 需要 ostream。
using namespace std;
// 构造函数
BinaryTree::BinaryTree() : root(0)
{
}
// print: 公共方法
void BinaryTree::print(ostream& os) const
{
    if(root == NULL) {
        cout << "tree is empty";
        return;
    }
    else
        print(os, root);
}
// print: 私有、递归方法
void BinaryTree::print(ostream& os, node* theRoot) const
{
    if(theRoot == NULL) {
        return;
    }
    else {
        print(os, theRoot->left());
        os << theRoot->getData() << ' ';
        print(os, theRoot->right());
    }
}
// insert: 公共方法
void BinaryTree::insert(int value)
{
    if(root == NULL) {
        root = new node(value);
    }
    else
        insert(root, value);
}
// insert: 私有方法
void BinaryTree::insert(node* root, int val)
{
    if(val < root->getData()) {
        if(root->left == NULL) {
            root->setLeft(new node(val));
        }
        else
            insert(root->left, val);
    } else {
        if(root->right == NULL) {
            root->setRight(new node(val));
        }
        else
            insert(root->right, val);
    }
}
// clear: 公共方法
void BinaryTree::clear()
{
    if(root == NULL) {
        return;
    }
    else {
        clear(root);
        root = 0;
    }
}
// clear: 私有递归方法
void BinaryTree::clear(node* theRoot)
{
    if(theRoot == NULL) {
        return;
    }
    else {
        clear(theRoot->left());
        clear(theRoot->right());
        delete theRoot;
    }
}
```

下面的程序测试了 `BinaryTree` 类。

```cpp
/* filename: testTree.cpp */
#include<iostream>
#include "BinaryTree.h" // 需要 BinaryTree。
using namespace std;
int main() {
    BinaryTree bt;
    bt.insert(2); // 测试在空树上插入。
    bt.insert(10); // 测试向右子树插入。
    bt.insert(-2); // 测试向左子树插入。
    bt.print(cout); // 测试打印方法。
    bt.clear(); // 测试 clear 方法。
    bt.print(cout);
    return 0;
}
```

程序运行的输出如下：

```
-2 2 10
tree is empty
```

既然 `BinaryTree` 的工作版本已经编写并测试，我们将编写一个表示泛型二叉树的类模板，并针对工作版本进行测试。

## 类模板

类模板的声明必须以以下形式开头：
`template < typename identifier >`
如下面的二叉树节点类声明所示：

```cpp
/* * 节点类声明
 * filename: nodeTemplate.h
 */
#ifndef TNODE_H
#define TNODE
template<typename T>
class Node
{
    // 私有属性
    private:
    T data;
    Node *left;
    Node *right;
    // 公共接口
    public:
    Node(); // 默认构造函数
    Node(T); // 参数构造函数
    // 访问器
    Node* getLeft() const;
    Node* getRight() const;
    T getData() const;
    // 修改器
    void setLeft(Node*);
    void setRight(Node*);
    void setData(T v);
};
#endif
```

注意标识符 `T` 替换了类模板声明中的 `int`。该类模板的实现如下：

```cpp
/* * 节点类实现
 * filename: nodeTemplate.cpp
 */
#include "nodeTemplate.h" // 需要 node 类。
using namespace std;
// 构造函数
template<typename T>
Node<T>::Node() : data(0),left(0),right(0)
{
}
template<typename T>
Node<T>::Node(T v):data(v), left(0), right(0)
{
}
// 访问器
template<typename T>
Node<T>* Node<T>::getLeft() const
{
    return left;
}
template<typename T>
Node<T>Node<T>::getRight() const
{
    return right;
}
template<typename T>
T Node<T>::getData() const
{
    return data;
}
// 修改器
template<typename T>
void Node<T>::setLeft(Node<T>*) l
{
    left=l;
}
template<typename T>
void Node<T>::setRight(Node<T>*) r
{
    right=r;
}
template<typename T>
void Node<T>::setData(T v)
{
    data=v;
}
```

注意类实现要求每个定义的方法都定义为方法模板。`BinaryTree` 的类模板定义如下：

### 第 10.5 类模板 539

```cpp
clear(root); //调用私有 clear
root = 0; //树为空
}
//结束 clear
```

```cpp
//clear: 私有，递归方法
template<typename T>
void BinaryTree<T>::clear(Node<T>*) {
    if(root == NULL)
        return;
    else
    {
        clear(root->getLeft());
        clear(root->getRight());
        delete(root);
    }
}//end clear
```

```cpp
//print: 公有方法
template<typename T>
void BinaryTree<T>::print(ostream& os) {
    if(root == NULL)
    {
        cout << "tree is empty";
        return;
    }
    else
        print(os, root); //调用私有 print
}//end print
```

```cpp
//print: 私有，递归方法
template<typename T>
void BinaryTree<T>::print(ostream& os, Node<T>* theRoot) const {
    if(root == NULL)
        return;
    else
    {
        print(os, root->getLeft());
        os << theRoot->getData() << ' ' << endl;
        print(os, theRoot->getRight());
    }
}//end print
```

```cpp
//insert: 公有方法
template<typename T>
void BinaryTree<T>::insert(T value) {
    if(root == NULL)
        root = new node<T>(value);
    else
        insert(root, value); //调用私有 insert
)//end insert
```

### 第 10 章 级主题

```cpp
//insert: 私有方法
template<typename T>
void BinaryTree<T>::insert(Node<T>* root, T val) {
    if(val < root->getData()) {
        // 遍历左子树
        if(root->getLeft() == NULL) {
            //在此处插入新节点
            root->setLeft(new Node<T>(val));
        } else {
            // 递归调用遍历左子树
            insert(root->getLeft(), val);
        }
    }
```

```cpp
else {
        // 遍历右子树
        if(root->getRight() == NULL) {
            //在此处插入新节点
            root->setRight(new Node<T>(val));
        } else {
```
