

```cpp
/*
 The 二叉搜索树类。该类的每个对象
 将代表一个 BST。
 */
class BST {
  private:
    /*
     BST 的根节点指针。它将指向
     根节点或 NULL。
    */
    BSTNode * root;
    /*
     插入节点的私有函数。将从公共函数调用。
    */
    void insert(BSTNode *, int);
    /*
     执行前序遍历的私有函数。将从公共函数调用。
     */
    void preorder(BSTNode);
    /*
     执行中序遍历的私有函数。将从公共函数调用。
     */
    void inorder(BSTNode);
    /*
     执行后序遍历的私有函数。将从公共函数调用。
     */
    void postorder(BSTNode);
public:
    /*
     BST 类的构造函数。它默认将将
     根指针置空。
    */
    BST();
    /*
     在 BST 的正确位置插入节点的函数。
     */
    void insert(int);
    /*
     执行前序遍历的函数。
     */
    void preorder();
    /*
     执行中序遍历的函数。
     */
    void inorder();
    /*
     执行后序遍历的函数。
     */
    void postorder();
    /*
     类的析构函数。
     */
    ~BST();
};

/* *
#endif
/*End of BST.h*/
```

该类仅有一个数据成员——root——它是私私的。因此，root 将是所有 BST 类对象中唯一的数据成员，并且 BST 类的构造函数将确保它在每个新创建的对象中都被置空。
如定义所示，root 将指向一个 BSTNode 类的对象。正如其名所示，它将指向 BST 的第一个节点。
现在让我们来看成员函数的实现（列表 9.34）。

# 列表 9.34 BST 类的实现

```cpp
/*Beginning of BST.cpp*/
#include <iostream.h>
#include "BST.h"
/*
插入节点的私有函数。将从公共函数调用。
*/
void BST::insert(BSTNode *nodePtr, int pValue)
{
  /*
  指针的引用作为一个参数传递。
  */
  /*
  如果指针为 NULL ...
  */
  if(nodePtr == NULL)
  {
    /*
    ... 创建一个节点并让指针指向它 ...
    */
    nodePtr = new BSTNode();
    /*
    ... 将传递给函数的值拷贝到新节点并 ...
    */
    nodePtr -> setVal(pValue);
    /*
    ... 返回。
    */
    return;
  }
  /*
  如果当前节点中的值大于传递的值 ...
  */
  if(nodePtr -> getVal() > pValue)
  {
    /*
    ... 从左孩子开始递归调用函数。
    */
    insert(nodePtr -> getLeft(), pValue);
  }

  /*
  如果当前节点中的值小于传递的值
  */
  if(nodePtr -> getVal() < pValue)
  {
    /*
    从右孩子开始递归调用函数。
    */
    insert(nodePtr -> getRight(), pValue);
  }
}

/*
执行前序遍历的私有函数。将从公共函数调用。
*/
void BST::preorder(BSTNode * nodePtr)
{
  /*
  只要传递的指针不为 NULL ...
  */
  if(nodePtr != NULL)
  {
    /*
    先显示当前节点的值 ...
    */
    cout << nodePtr -> getVal() << endl;
    /*
    ... 
    然后递归调用左孩子的函数 ...
    */
    preorder(nodePtr -> getLeft());
    /*
    ... 
    然后递归调用右孩子的函数。
    */
    preorder(nodePtr -> getRight());
  }
}

/*
执行中序遍历的私有函数。将从公共函数调用。
*/
void BST::inorder(BSTNode * nodePtr)
{
  /*
  只要传递的指针不为 NULL ...
  */
  if(nodePtr != NULL)
  {
    /*
    ... 先递归调用左孩子的函数...
    */
    inorder(nodePtr -> getLeft());
    /*
    ... 然后显示当前节点的值
    */
    cout << nodePtr -> getVal() << endl;
    /*
    ... 然后再递归调用右孩子的函数。
    */
    inorder(nodePtr -> getRight());
  }
}

/*
执行后序遍历的私有函数。将从公共函数调用。
*/
void BST::postorder(BSTNode * nodePtr)
{
  /*
  只要指针不为 NULL ...
  */
  if(nodePtr != NULL)
  {
    /*
    ... 先递归调用左孩子的函数...
    */
    postorder(nodePtr -> getLeft());
    /*
    ... 
    然后递归调用右孩子的函数 ...
    */
    postorder(nodePtr -> getRight());
  }
}
```

