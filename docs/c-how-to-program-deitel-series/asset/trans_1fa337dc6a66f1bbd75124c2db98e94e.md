

```text
先序遍历
39.2 16.5 3.3 1.1 4.4 82.7 65.2 90.8 89.5 92.5
中序遍历
1.1 3.3 4.4 16.5 39.2 65.2 82.7 89.5 90.8 92.5
后序遍历
1.1 4.4 3.3 16.5 65.2 89.5 92.5 90.8 82.7 39.2
```

**图 19.20** | 创建并遍历一棵二叉树。（第 3 部分，共 3 部分。）

## 类模板 TreeNode

`TreeNode` 类模板定义（图 19.21）将 `Tree<NODETYPE>` 声明为其友元（第 13 行）。这使得类模板 `Tree`（图 19.22）的某个特化版的所有成员函数成为类模板 `TreeNode` 对应特化版的友元，从而它们能够访问该类型 TreeNode 对象的私有成员。由于在友元声明中 `TreeNode` 的模板参数 NODETYPE 被用作 `Tree` 的模板实参，因此以特定类型特化出的 `TreeNode` 只能由以相同类型特化出的 `Tree` 来处理（例如，一个存储 int 值的 `Tree` 管理存储 int 值的 TreeNode 对象）。

第 30–32 行声明了 TreeNode 的私有数据——节点的数据值，以及指向节点*左子树*的指针 `leftPtr` 和指向节点*右子树*的指针 `rightPtr`。构造函数（第 16–22 行）将 data 设置为作为构造函数实参提供的值，并将指针 `leftPtr` 和 `rightPtr` 设置为 `nullptr`（从而将该节点初始化为一个*叶节点*）。成员函数 `getData`（第 25–28 行）返回数据值。

```cpp
// Fig. 19.21: TreeNode.h
// TreeNode class-template definition.
#ifndef TREENODE_H
#define TREENODE_H

// forward declaration of class Tree
template< typename NODETYPE > class Tree;

// TreeNode class-template definition
template< typename NODETYPE >
class TreeNode
{
    friend class Tree< NODETYPE >;
public:
    // constructor
    TreeNode( const NODETYPE &d )
        : leftPtr( nullptr ), // pointer to left subtree
          data( d ), // tree node data
          rightPtr( nullptr ) // pointer to right subtree
    {
        // empty body
    } // end TreeNode constructor
```

**图 19.21** | TreeNode 类模板定义。（第 1 部分，共 2 部分。）

```cpp
    // return copy of node's data
    NODETYPE getData() const
    {
        return data;
    } // end getData function

private:
    TreeNode< NODETYPE > *leftPtr; // pointer to left subtree
    NODETYPE data;
    TreeNode< NODETYPE > *rightPtr; // pointer to right subtree
}; // end class TreeNode

#endif
```

**图 19.21** | TreeNode 类模板定义。（第 2 部分，共 2 部分。）

## 类模板 Tree

类模板 `Tree`（图 19.22）的私有数据是 rootPtr（第 42 行），它是一个指向树根节点的指针。`Tree` 构造函数（第 14–15 行）将 rootPtr 初始化为 nullptr，以表示树最初为空。该类的公有成员函数有：`insertNode`（第 18–21 行），用于在树中插入一个新节点；`preOrderTraversal`（第 24–27 行）、`inOrderTraversal`（第 30–33 行）和 `postOrderTraversal`（第 36–39 行），它们分别以指定的方式遍历树。这些成员函数中的每一个都调用自己的递归工具函数来对树的内部表示执行相应操作，因此程序无需访问底层的私有数据即可执行这些函数。请记住，递归要求我们传入一个指针，该指针表示下一个要处理的子树。

```cpp
// Fig. 19.22: Tree.h
// Tree class-template definition.
#ifndef TREE_H
#define TREE_H

#include <iostream>
#include "TreeNode.h"

// Tree class-template definition
template< typename NODETYPE > class Tree
{
public:
    // constructor
    Tree()
        : rootPtr( nullptr ) { /* empty body */ }

    // insert node in Tree
    void insertNode( const NODETYPE &value )
    {
        insertNodeHelper( &rootPtr, value );
    } // end function insertNode
```

**图 19.22** | Tree 类模板定义。（第 1 部分，共 3 部分。）

```cpp
    // begin preorder traversal of Tree
    void preOrderTraversal() const
    {
        preOrderHelper( rootPtr );
    } // end function preOrderTraversal

    // begin inorder traversal of Tree
    void inOrderTraversal() const
    {
        inOrderHelper( rootPtr );
    } // end function inOrderTraversal

    // begin postorder traversal of Tree
    void postOrderTraversal() const
    {
        postOrderHelper( rootPtr );
    } // end function postOrderTraversal

private:
    TreeNode< NODETYPE > *rootPtr;

    // utility function called by insertNode; receives a pointer
    // to a pointer so that the function can modify pointer's value
    void insertNodeHelper(
        TreeNode< NODETYPE > **ptr, const NODETYPE &value )
    {
        // subtree is empty; create new TreeNode containing value
        if ( *ptr == nullptr )
            *ptr = new TreeNode< NODETYPE >( value );
        else // subtree is not empty
        {
            // data to insert is less than data in current node
            if ( value < ( *ptr )->data )
                insertNodeHelper( &( *ptr )->leftPtr, value );
            else
            {
                // data to insert is greater than data in current node
                if ( value > ( *ptr )->data )
                    insertNodeHelper( &( *ptr )->rightPtr, value );
                else // duplicate data value ignored
                    cout << value << " dup" << endl;
            } // end else
        } // end else
    } // end function insertNodeHelper

    // utility function to perform preorder traversal of Tree
    void preOrderHelper( TreeNode< NODETYPE > *ptr ) const
    {
        if ( ptr != nullptr )
        {
            cout << ptr->data << " "; // process node
            preOrderHelper( ptr->leftPtr ); // traverse left subtree
```

**图 19.22** | Tree 类模板定义。（第 2 部分，共 3 部分。）

![](img/b42ba5cd262b1358d16610173f975e4d_845_0.png)

**图 19.23**  一棵二叉搜索树。

## 中序遍历算法

函数 `inOrderTraversal` 调用工具函数 `inOrderHelper`（第 80–88 行）来对二叉树执行中序遍历。中序遍历的步骤如下：

1. 用中序遍历遍历*左*子树。（这由第 84 行对 `inOrderHelper` 的调用来完成。）
2. 处理节点中的值——即打印节点值（第 85 行）。
3. 用中序遍历遍历*右*子树。（这由第 86 行对 `inOrderHelper` 的调用来完成。）

节点中的值在其*左*子树中的值被处理之后才被处理，因为每次调用 `inOrderHelper` 都会立即用指向*左*子树的指针再次调用 `inOrderHelper`。图 19.23 中树的中序遍历为

```text
6  13  17  27  33  42  48
```

对二叉搜索树进行中序遍历会按*升序*打印节点值。创建二叉搜索树的过程实际上对数据进行了*排序*——因此，这一过程被称为[二叉树排序](#)。

## 先序遍历算法

函数 `preOrderTraversal` 调用工具函数 `preOrderHelper`（第 69–77 行）来对二叉树执行先序遍历。先序遍历的步骤如下：

1. 处理节点中的值（第 73 行）。
2. 用先序遍历遍历*左*子树。（这由第 74 行对 `preOrderHelper` 的调用来完成。）
3. 用先序遍历遍历*右*子树。（这由第 75 行对 `preOrderHelper` 的调用来完成。）

每个节点中的值在访问该节点时被处理。处理完给定节点中的值后，再处理*左*子树中的值。然后处理*右*子树中的值。图 19.23 中树的先序遍历为

```text
27  13  6  17  42  33  48
```

## 后序遍历算法

函数 `postOrderTraversal` 调用工具函数 `postOrderHelper`（第 91–99 行）来对二叉树执行后序遍历。后序遍历的步骤如下：

1. 用后序遍历遍历*左*子树。（这由第 95 行对 `postOrderHelper` 的调用来完成。）

## 小结

### 第 19.1 节 引言

- 动态数据结构（第 778 页）在执行期间会增长和收缩。
- 链表（第 778 页）是数据项“排成一行”的集合——可以在链表中的任何位置进行插入和删除。
- 栈（第 778 页）在编译器和操作系统中很重要：插入和删除只能在栈的一端——栈顶（第 778 页）进行。
- 队列（第 778 页）表示等待线；插入在队列的后面（也称为尾部；第 778 页）进行，删除在队列的前面（也称为头部；第 778 页）进行。
- 二叉树（第 778 页）有助于高速数据排序和查找、高效的重复数据消除、文件系统目录的表示以及将表达式编译为机器码。

### 第 19.2 节 自引用类

- 自引用类（第 779 页）包含一个指向相同类类型对象的指针。
- 自引用类对象可以链接在一起，形成有用的数据结构，如列表、队列、栈和树。

### 第 19.3 节 链表

- 链表是自引用类对象（称为节点）的线性集合，通过指针链接（第 780 页）连接起来——因此称为“链”表。
- 通过指向列表第一个节点的指针来访问链表。每个后续节点通过前一个节点中存储的链接指针成员访问，最后一个节点包含一个空指针。
- 链表、栈和队列是线性数据结构（第 780 页）。树是非线性数据结构（第 780 页）。
- 当要表示的数据元素数量不可预测时，链表是合适的。
- 链表是动态的，因此列表的长度可以根据需要增加或减少。
- 单向链表以指向第一个节点的指针开始，每个节点包含一个指向“序列中”下一个节点的指针。
- 循环单向链表（第 793 页）以指向第一个节点的指针开始，每个节点包含一个指向下一个节点的指针。“最后一个节点”不包含空指针；相反，最后一个节点中的指针指回第一个节点，从而闭合“环”。
- 双向链表（第 793 页）允许向前和向后遍历。
- 双向链表通常用两个“起始指针”实现——一个指向第一个元素，允许从前往后遍历列表；另一个指向最后一个元素，允许从后往前遍历。每个节点都有指向下一个节点和前一个节点的指针。
- 在循环双向链表（第 794 页）中，最后一个节点的向前指针指向第一个节点，第一个节点的向后指针指向最后一个节点，从而闭合“环”。

### 第 19.4 节 栈

- 栈数据结构只允许在栈顶添加和删除节点。
- 栈被称为后进先出（LIFO）数据结构。
- 函数 push 在栈顶插入一个新节点。函数 pop 从栈顶删除一个节点。

