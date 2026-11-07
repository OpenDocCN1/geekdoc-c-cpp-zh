
第 1 行的语句将 `fParamFunc1` 声明为一个函数，该函数接受任意一个 `void` 函数作为参数，而这个 `void` 函数有一个 `int` 类型的值参数。第 2 行的语句将 `fParamFunc2` 声明为一个函数，该函数接受任意一个 `void` 函数作为参数，而这个 `void` 函数有一个 `elemType` 类型的引用参数。

现在，我们可以重写，比如说，类 `binaryTreeType` 的中序遍历函数。或者，我们可以重载现有的中序遍历函数。为了进一步说明函数重载，我们将重载中序遍历函数。因此，我们在类 `binaryTreeType` 的定义中包含以下语句：

```cpp
void inorderTraversal(void (*visit) (elemType&)) const;
    //Function to do an inorder traversal of the binary tree.
    //The parameter visit, which is a function, specifies the
    //action to be taken at each node.
    //Postcondition: The action specified by the function
    //              visit is applied to each node of the
    //              binary tree.
    //
```

```cpp
void inorder(nodeType<elemType> *p,
             void (*visit) (elemType&)) const;
    //Function to do an inorder traversal of the binary tree
    //starting at the node specified by the parameter p.
    //The parameter visit, which is a function, specifies the
    //action to be taken at each node.
    //Postcondition: The action specified by the function visit
    //              is applied to each node of the binary tree
    //              to which p points.
    //
```

这些函数的定义如下：

```cpp
template <class elemType>
void binaryTreeType<elemType>::inorderTraversal
                         (void (*visit) (elemType& item)) const
{
    inorder(root, *visit);
}
```

```cpp
template <class elemType>
void binaryTreeType<elemType>::inorder(nodeType<elemType> *p,
                         void (*visit) (elemType& item)) const
{
    if (p != nullptr)
    {
        inorder(p->lLink, *visit);
        (*visit) (p->info);
        inorder(p->rLink, *visit);
    }
}
```

函数 `inorder` 定义中的语句 `(*visit) (p->info);` 调用由指针 `visit` 指向的、带有一个 `elemType` 类型引用参数的函数。

例 19-5 进一步说明了如何将函数作为参数传递给其他函数。

### 例 19-5

本示例展示如何将用户定义的函数作为参数传递给二叉树遍历算法。为便于说明，我们仅展示如何使用中序遍历函数。

下面的程序使用类 `bSearchTreeType`（它派生自类 `binaryTreeType`）来构建二叉树。遍历函数包含在类 `binaryTreeType` 中，然后由类 `bSearchTreeType` 继承。

```cpp
#include <iostream>                                                     //Line 1
#include "binarySearchTree.h"                                           //Line 2

using namespace std;                                                    //Line 3

void print(int& x);                                                     //Line 4
void update(int& x);                                                    //Line 5

int main()                                                              //Line 6
{                                                                       //Line 7
    bSearchTreeType<int> treeRoot;                                      //Line 8

    int num;                                                            //Line 9

    cout << "Line 10: Enter numbers ending "
         << "with -999." << endl;                                       //Line 10
    cin >> num;                                                         //Line 11

    while (num != -999)                                                 //Line 12
    {                                                                   //Line 13
        treeRoot.insert(num);                                           //Line 14
        cin >> num;                                                     //Line 15
    }                                                                   //Line 16

    cout << endl
         << "Line 17: Tree nodes in inorder: ";                         //Line 17
    treeRoot.inorderTraversal(print);                                   //Line 18
    cout << endl << "Line 19: Tree height: "                            //Line 19
         << treeRoot.treeHeight()
         << endl << endl;

    cout << "Line 20: ******* Update Nodes "
         << "*******" << endl;                                          //Line 20
    treeRoot.inorderTraversal(update);                                  //Line 21

    cout << "Line 22: Tree nodes in inorder "
         << "after the update: " << endl
         << "                         ";              //Line 22
    treeRoot.inorderTraversal(print);                //Line 23
    cout << endl << "Line 24: Tree Height: "
         << treeRoot.treeHeight() << endl;           //Line 24

    return 0;                                        //Line 25
}                                                    //Line 26

void print(int& x)                                   //Line 27
{
    cout << x << " ";                                //Line 29
}                                                    //Line 30

void update(int& x)                                  //Line 31
{
    x = 2 * x;                                       //Line 33
}                                                    //Line 34
```

**示例运行：** 在此示例运行中，用户输入以底纹显示。

```
Line 10: Enter numbers ending with -999.
56 87 23 65 34 45 12 90 66 -999

Line 17: Tree nodes in inorder: 12 23 34 45 56 65 66 87 90

Line 19: Tree Height: 4

Line 20: ******* Update Nodes *******

Line 22: Tree nodes in inorder after the update:
        24 46 68 90 112 130 132 174 180

Line 24: Tree Height: 4
```

该程序的工作方式如下：第 8 行的语句将 treeRoot 声明为一个二叉搜索树对象，其中每个节点的数据均为 int 类型。第 11 行至第 16 行的语句构建该二叉搜索树。第 18 行的语句使用 treeRoot 的成员函数 inorderTraversal 遍历二叉搜索树 treeRoot。第 18 行中传给函数 inorderTraversal 的参数是函数 print（定义于第 27 行）。由于函数 print 输出其参数的值，因此第 18 行的语句输出二叉搜索树 treeRoot 各节点的数据。第 19 行的语句输出该二叉搜索树的高度。

第 21 行的语句使用成员函数 inorderTraversal 遍历二叉搜索树 treeRoot。在第 21 行中，函数 inorderTraversal 的实参是函数 update（定义于第 31 行）。函数 update 将其参数的值加倍。因此，第 21 行的语句通过将该值加倍来更新二叉搜索树每个节点的数据。第 23 行和第 24 行的语句输出该二叉搜索树的节点和高度。

> **注意**
>
> **（AVL 树）** 本章还讨论 AVL 树。所需材料位于文件 AVL Trees.pdf 中。该文件可在 www.cengagebrain.com 获取。要找到该文件，请通过输入本教材的 ISBN 导航到该书页面，然后单击“Free Materials”。

## 编程示例：DVD 商店（再探）

![](img/b217c421655b51e7494cf3b89bb5432d_1450_0.png)

在第 16 章中，我们设计了一个程序，帮助 DVD 商店自动化其 DVD 租赁流程。该程序使用一个（无序）链表来跟踪商店中的 DVD 库存。由于链表上的搜索算法是顺序搜索，而且链表相当大，搜索可能很耗时。在本章中，你学习了如何将数据组织成二叉树。如果二叉树构建得当（也就是说，它不是线性的），那么搜索算法可以显著改进。此外，通常来说，二叉搜索树中的项插入和删除比链表中更快。因此，我们将重新设计 DVD 商店程序，以便可以在二叉树中维护 DVD 库存。与第 16 章一样，我们将客户列表的二叉树设计留作练习。

### DVD 对象

在第 16 章中，使用链表维护商店中的 DVD 列表。由于该链表是无序的，为了查看某个特定 DVD 是否有库存，顺序搜索算法使用相等运算符进行比较。然而，对于二叉树，我们需要其他关系运算符来进行搜索、插入和删除操作。因此，我们将重载所有关系运算符。除这一差异外，类 `dvdType` 与之前相同。为完整起见，我们给出其定义，但不附带文档说明。

```cpp
class dvdType
{
    friend ostream& operator<< (ostream&, const dvdType&);

public:
    void setDVDInfo(string title, string star1,
                    string star2, string producer,
                    string director, string productionCo,
                    int setInStock);
    int getNoOfCopiesInStock() const;
    void checkOut();
    void checkIn();
    void printTitle();
    void printInfo() const;
    bool checkTitle(string title);
    void updateInStock(int num);
    void setCopiesInStock(int num);
    string getTitle() const;
    dvdType(string title = "", string star1 = "",
            string star2 = "", string producer = "",
            string director = "", string productionCo = "",
            int setInStock = 0);
```

