
## 19.6.3 测试 `Tree` 类模板

我们从*驱动程序*（**图 19.20**）开始讨论，然后继续介绍类 `TreeNode`（**图 19.21**）和 `Tree`（**图 19.22**）的实现。函数 `main`（**图 19.20**）首先实例化 `Tree<int>` 类型的整数树 `intTree`（第 9 行）。程序提示输入 10 个整数，每个整数都通过调用 `insertNode` 插入二叉树（第 17 行）。然后，程序对 `intTree` 执行*前序*、*中序*和*后序*遍历（稍后将解释这些遍历）（分别在第 21、24 和 27 行）。接下来，我们实例化 `Tree<double>` 类型的浮点数树 `doubleTree`（第 29 行），然后提示输入 10 个 `double` 值，每个值都通过调用 `insertNode` 插入二叉树（第 38 行）。最后，我们对 `doubleTree` 执行前序、中序和后序遍历（分别在第 42、45 和 48 行）。

```cpp
// Fig. 19.20: fig19_20.cpp
// Creating and traversing a binary tree.
#include <iostream>
#include <iomanip>
#include "Tree.h" // Tree class definition
using namespace std;

int main() {
   Tree<int> intTree; // create Tree of int values

   cout << "Enter 10 integer values:\n";

   // insert 10 integers to intTree
   for (int i{0}; i < 10; ++i) {
      int intValue = 0;
      cin >> intValue;
      intTree.insertNode(intValue);
   }

   cout << "\nPreorder traversal\n";
   intTree.preOrderTraversal();

   cout << "\nInorder traversal\n";
   intTree.inOrderTraversal();

   cout << "\nPostorder traversal\n";
   intTree.postOrderTraversal();

   Tree<double> doubleTree; // create Tree of double values

   cout << fixed << setprecision(1)
      << "\nEnter 10 double values:\n";

   // insert 10 doubles to doubleTree
   for (int j{0}; j < 10; ++j) {
      double doubleValue = 0.0;
      cin >> doubleValue;
      doubleTree.insertNode(doubleValue);
   }

   cout << "\nPreorder traversal\n";
   doubleTree.preOrderTraversal();

   cout << "\nInorder traversal\n";
   doubleTree.inOrderTraversal();

   cout << "\nPostorder traversal\n";
   doubleTree.postOrderTraversal();
   cout << endl;
}
```

```text
Enter 10 integer values:
50 25 75 12 33 67 88 6 13 68

Preorder traversal
50 25 12 6 13 33 75 67 68 88
Inorder traversal
6 12 13 25 33 50 67 68 75 88
Postorder traversal
6 13 12 33 25 68 67 88 75 50

Enter 10 double values:
39.2 16.5 82.7 3.3 65.2 90.8 1.1 4.4 89.5 92.5

Preorder traversal
39.2 16.5 3.3 1.1 4.4 82.7 65.2 90.8 89.5 92.5
Inorder traversal
1.1 3.3 4.4 16.5 39.2 65.2 82.7 89.5 90.8 92.5
Postorder traversal
1.1 4.4 3.3 16.5 65.2 89.5 92.5 90.8 82.7 39.2
```

图 19.20 创建并遍历二叉树。

## 19.6.4 `TreeNode` 类模板

`TreeNode` 类模板（图 19.21）的定义将 `Tree<NODETYPE>` 声明为其 `friend`（第 12 行）。这使得类模板 `Tree`（图 19.22）的给定特化的所有成员函数成为类模板 `TreeNode` 对应特化的友元，因此它们可以访问该类型 `TreeNode` 对象的 `private` 成员。由于 `TreeNode` 的模板参数 `NODETYPE` 在 `friend` 声明中用作 `Tree` 的模板实参，因此用特定类型特化的 `TreeNode` 对象只能由用相同类型特化的 `Tree` 处理（例如，`int` 值的 `Tree` 管理存储 `int` 值的 `TreeNode` 对象）。

第 20–22 行声明了 `TreeNode` 的 `private` 数据——节点的 `data` 值，以及指针 `leftPtr`（指向节点的*左*子树）和 `rightPtr`（指向节点的*右*子树）。两个指针都初始化为 `nullptr`——从而将该节点初始化为*叶节点*。构造函数（第 15 行）将 `data` 设置为作为构造函数实参提供的值。成员函数 `getData`（第 18 行）返回 `data` 值。

```cpp
// Fig. 19.21: TreeNode.h
// TreeNode class-template definition.
#ifndef TREENODE_H
#define TREENODE_H

// forward declaration of class Tree
template<typename NODETYPE> class Tree;

// TreeNode class-template definition
template<typename NODETYPE>
class TreeNode {
    friend class Tree<NODETYPE>;
public:
    // constructor
    TreeNode(const NODETYPE& d) : data{d} { }

    // return copy of node's data
    NODETYPE getData() const {return data;}
private:
    TreeNode<NODETYPE>* leftPtr{nullptr}; // pointer to left subtree
    NODETYPE data{};
    TreeNode<NODETYPE>* rightPtr{nullptr}; // pointer to right subtree
};

#endif
```

图 19.21 *TreeNode* 类模板定义。

## 19.6.5 `Tree` 类模板

类模板 `Tree`（图 19.22）的 `private` 数据为 `rootPtr`（第 33 行），它是指向树根节点的指针，初始化为 `nullptr` 以表示空树。该类的 `public` 成员函数包括：在树中插入新节点的 `insertNode`（第 13–15 行），以及 `preOrderTraversal`（第 18–20 行）、`inOrderTraversal`（第 23–25 行）和 `postOrderTraversal`（第 28–30 行），它们各自按指定方式遍历树。这些成员函数中的每一个都会调用自己的递归工具函数，以对树的内部表示执行相应操作，因此程序*不*需要访问底层的 `private` 数据来执行这些函数。请记住，递归要求我们传入一个表示下一个要处理的子树的指针。

```cpp
// Fig. 19.22: Tree.h
// Tree class-template definition.
#ifndef TREE_H
#define TREE_H

#include <iostream>
#include "TreeNode.h"

// Tree class-template definition
template<typename NODETYPE> class Tree {
public:
    // insert node in Tree
    void insertNode(const NODETYPE& value) {
        insertNodeHelper(&rootPtr, value);
    }

    // begin preorder traversal of Tree
    void preOrderTraversal() const {
        preOrderHelper(rootPtr);
    }

    // begin inorder traversal of Tree
    void inOrderTraversal() const {
        inOrderHelper(rootPtr);
    }

    // begin postorder traversal of Tree
    void postOrderTraversal() const {
        postOrderHelper(rootPtr);
    }

private:
    TreeNode<NODETYPE>* rootPtr{nullptr};

    // utility function called by insertNode; receives a pointer
    // to a pointer so that the function can modify pointer's value
    void insertNodeHelper(
        TreeNode<NODETYPE>** ptr, const NODETYPE& value) {
        // subtree is empty; create new TreeNode containing value
        if (*ptr == nullptr) {
            *ptr = new TreeNode<NODETYPE>(value);
        }
        else { // subtree is not empty
            // data to insert is less than data in current node
            if (value < (*ptr)->data) {
                insertNodeHelper(&((*ptr)->leftPtr), value);
            }
            else {
                // if data to insert is greater than data in current node
                if (value > (*ptr)->data) {
                    insertNodeHelper(&((*ptr)->rightPtr), value);
                }
                else { // duplicate data value ignored
                    cout << value << " dup" << endl;
                }
            }
        }
    }

    // utility function to perform preorder traversal of Tree
    void preOrderHelper(TreeNode<NODETYPE>* ptr) const {
        if (ptr != nullptr) {
            cout << ptr->data << ' '; // process node
            preOrderHelper(ptr->leftPtr); // traverse left subtree
            preOrderHelper(ptr->rightPtr); // traverse right subtree
        }
    }

    // utility function to perform inorder traversal of Tree
    void inOrderHelper(TreeNode<NODETYPE>* ptr) const {
        if (ptr != nullptr) {
            inOrderHelper(ptr->leftPtr); // traverse left subtree
            cout << ptr->data << ' '; // process node
            inOrderHelper(ptr->rightPtr); // traverse right subtree
        }
    }

    // utility function to perform postorder traversal of Tree
    void postOrderHelper(TreeNode<NODETYPE>* ptr) const {
        if (ptr != nullptr) {
            postOrderHelper(ptr->leftPtr); // traverse left subtree
            postOrderHelper(ptr->rightPtr); // traverse right subtree
            cout << ptr->data << ' '; // process node
        }
    }
};

#endif
```

图 19.22 **Tree** 类模板定义。
