

![](img/f2bfa570e453b020c16e048c79a3ea0e_547_0.png)

图 10.7 含有 6 个节点的二叉搜索树。

```
inOrder traverse:
if(root == null)
    return
inOrder traverse left child
visit node
inOrder traverse right child
```

该算法从二叉树的根节点开始，对每个连续节点的左子节点递归调用自身，直到遇到空值。当最终找到一个左子节点为空的节点时，该节点会被“访问”，算法会对该节点的右子节点递归调用自身。条件 root == null 是终止条件，每次递归调用都将问题缩小为遍历一棵更小的子树。对图 10.7 中的树应用中序遍历，并在访问每个节点时打印它，将产生以下输出：8 10 14 19 22 27。

为在正确位置插入新节点以维护二叉搜索树的顺序而设计的算法，从树的根节点开始。如果树为空，则将新节点插入为树中的第一个节点。如果树不为空，则将新节点的值与第一个节点的值进行比较。如果新节点的值小于根节点的值，则算法对左子节点递归调用自身，否则算法对右子节点递归调用自身。递归算法如下所示：

```
insert( node* root, int value ):
if(root == null)
    root = new node(value)
    return
else
if( value < root->value)
    insert(root->left child,value)
else
    insert(root->right child,value)
```

![](img/f2bfa570e453b020c16e048c79a3ea0e_548_0.png)

图 10.8 插入新节点后的二叉搜索树。

如果将值 17 插入图 10.7 中的二叉搜索树，则生成的树将如图 10.8 所示。

接下来描述清除树的算法。

```
clear(node* root):

if(root == null)
    return
else
    clear(root->left)
    clear(root->right)
    delete root
```

现在可以根据图 10.5 中的描述完成 BinaryTree 类的定义了。

```
/*................................................................*/
/* Binary tree declaration                                     */
/* filename: binaryTree.h                                      */
/*................................................................*/

#include "node.h" //Required for node.
#include <iostream> //Required for ostream.
using namespace std;

class BinaryTree {
public:
    //Default constructor.
    BinaryTree();
    
    //public. non recursive print and insert
    void print(ostream& out) const;
    void insert(int value);
    void clear();
private:
//private recursive overloaded print and insert
void print(ostream& out, node* rt) const;
void insert(node*& rt, int value);
void clear(node* rt);

//private attribute
Node* root;
};
/*................................................................*/
```

请注意，在 BinaryTree 类的声明中，......... print()、insert() 和 clear() 都是重载的。这些方法的公共版本不是递归的。这些方法的私有版本是递归的，并且每个都有一个类型为 Node* 的形式参数。

这些方法的公共版本必须由 BinaryTree 对象调用，因此树的根节点由调用对象提供。这些方法的私有版本会对调用对象的右子树和左子树递归调用自身，以遍历树。因此，形式参数 rt 的值在每次后续调用中都不同，必须作为参数传递以支持这些方法的递归特性。最小 BinaryTree 类的定义如下所示：

```
/*...............................................................*/
/* Binary tree implementation                                  */
/* Filename: binaryTree.cpp                                    */
/*...............................................................*/

#include "BTree.h"    //Required for BinaryTree.
#include <iostream>   //Required for ostream.
using namespace std;

//Constructor
BinaryTree::BinaryTree():root(0)
{
}

//print: Public method
void BinaryTree::print(ostream& os) const
{
    if(root == NULL)
    {
        cout << "tree is empty ";
        return;
    }
    else
        print(os, root); //call private print()
}

//print: Private recursive method
void BinaryTree::print(ostream& os, node* theRoot) const
{
    if(theRoot == NULL)
        return;
    else
    {
        print(os, theRoot->getLeft());
        os << theRoot->getData() << " ";
        print(os, theRoot->getRight());
    }
}

//insert: public method
void BinaryTree::insert(int value)
{
    if(root == NULL)
        root = new node(value);
    else
        insert(root,value); //call private insert
}

//insert: private method
void BinaryTree::insert(node* root, int val)
{
    if(val < root->getData())
    {
        //Traverse the left subtree
        if(root->getLeft() == NULL)
        {
            //insert new node here.
            root->setLeft(new node(val));
        }
        else
        {
            //recursive call to traverse left subtree
            insert(root->getLeft(),val);
        }
    }
    else
    {
        //Traverse the right subtree
        if(root->getRight() == NULL)
        {
            //insert new node here
            root->setRight(new node(val));
        }
        else
        {
            //recursive call to traverse right subtree
            insert(root->getRight(),val);
        }
    }
}//end insert

//clear: Public method
void BinaryTree::clear()
{
    if(root == NULL)
        return;
    else
    {
        clear(root); //call private clear()
        root = 0; //tree is empty
    }
}//end clear

//clear: private, recursive method
void BinaryTree::clear(node* theRoot)
{
    if(theRoot == NULL)
        return;
    else
    {
        clear(theRoot->getLeft());
        clear(theRoot->getRight());
        delete theRoot;
    }
}//end clear
```

/*--------------------------------------------------------------*/

以下程序测试 BinaryTree 类。

/*--------------------------------------------------------------*/

/* 文件名：testBTree
   ... */

#include<iostream> //Required for cout.
#include "BinaryTree.h" //Required for BinaryTree.
using namespace std;

int main()
{
    BinaryTree bt; //Test default constructor
    bt.insert(2); //Test insert on empty tree.
    bt.insert(10); //Test insert to right subtree.
    bt.insert(-2); //Test insert to left subtree.
    bt.print(cout); //Test print method.
    bt.clear(); //Test clear method.
    bt.print(cout);
    return 0;
}

我们测试程序的示例运行输出如下所示：

```
-2 2 10
tree is empty
```

现在已经编写并测试了一个可用的 BinaryTree 版本，我们将编写一个类模板来表示通用二叉树，并针对可用版本对其进行测试。

## 10.5 类模板

类模板的声明必须以如下形式的表达式开头：
`template < typename identifier >`
以下是表示二叉树节点的类模板声明示例：

```
```cpp
/* .................... class declaration for node template .................... */
/* .................... filename: nodeTemplate.h .................... */

#ifndef TNODE_H
#define TNODE_H

template < typename T >
class Node
{
   // Private attributes
   private:
      T data;
      Node *left;
      Node *right;

   // Public interface.
   public:
      Node(); // Default constructor
      Node(T); // Parameterized constructor

      // Accessors
      Node * getLeft() const;
      Node * getRight() const;
      T getData() const;

      // Mutators
      void setLeft(Node *);
      void setRight(Node *);
      void setData(T v);
};

#endif
/* .................... */
```
```

请注意，标识符 T 在类模板声明中替换了 int。此类模板的实现如下所示。

```
```cpp
/* .................... Class implementation for Node template .................... */
/* .................... filename: nodeTemplate.cpp .................... */

#include "nodeTemplate.h" // Required for Node.
using namespace std;
```
```

