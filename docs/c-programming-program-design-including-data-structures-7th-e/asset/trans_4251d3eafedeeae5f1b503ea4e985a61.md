
第 1 行的语句将 `fParamFunc1` 声明为一个函数，该函数接受任意一个带有一个 `int` 类型值参数的 `void` 函数作为参数。第 2 行的语句将 `fParamFunc2` 声明为一个函数，该函数接受任意一个带有一个 `elemType` 类型引用参数的 `void` 函数作为参数。

现在，我们可以重写，比如说，`class` `binaryTreeType` 的中序遍历函数。或者，我们可以重载现有的中序遍历函数。为了进一步说明函数重载，我们将重载中序遍历函数。因此，我们在 `class` `binaryTreeType` 的定义中包含以下语句：

```cpp
void inorderTraversal(void (*visit) (elemType&)) const;
//Function to do an inorder traversal of the binary tree.
//The parameter visit, which is a function, specifies
//the action to be taken at each node.
//Postcondition: The action specified by the function
//              visit is applied to each node of the
//              binary tree.

void inorder(nodeType<elemType> * p,
             void (*visit) (elemType&)) const;
//Function to do an inorder traversal of the binary tree
//Starting at the node specified by the parameter p.
//The parameter visit, which is a function, specifies the
//action to be taken at each node.
//Postcondition: The action specified by the function visit
//              is applied to each node of the binary tree
//              to which p points.
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
void binaryTreeType<elemType>::inorder(nodeType<elemType>* p,
                         void (*visit) (elemType& item)) const
{
    if (p != nullptr)
    {
        inorder(p->lLink, *visit);
        (*visit)(p->info);
        inorder(p->rLink, *visit);
    }
}
```

语句：

```cpp
(*visit)(p->info);
```

在函数 `inorder` 的定义中，该语句调用由指针 `visit` 所指向的、带有一个 `elemType` 类型引用参数的函数。

```cpp
cout << endl << "Line 15: Tree Height: "
     << treeRoot.treeHeight() << endl;          //Line 15
return 0;                                      //Line 16
}

void print(int& x)                             //Line 17
{
    cout << x << " ";                          //Line 18
}
void update(int& x)                            //Line 19
{
    x = 2 * x;                                 //Line 20
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```
Line 3: Enter numbers ending with -999.
```

```
56 87 23 65 34 45 12 90 66 -999
```

```
Line 8: Tree nodes in inorder: 12 23 34 45 56 65 66 87 90
Line 10: Tree Height: 4
```

```
Line 11: ******** Update Nodes ********
Line 13: Tree nodes in inorder after the update:
         24 46 68 90 112 130 132 174 180
Line 15: Tree Height: 4
```

该程序的工作方式如下。第 1 行的语句将 `treeRoot` 声明为一个二叉搜索树对象，其中每个节点中的数据类型为 `int`。第 4 行到第 7 行的语句构建二叉搜索树。第 9 行的语句使用 `treeRoot` 的成员函数 `inorderTraversal` 遍历二叉搜索树 `treeRoot`。第 9 行中函数 `inorderTraversal` 的参数是函数 `print`（定义于第 17 行）。因为函数 `print` 输出其参数的值，所以第 9 行的语句输出二叉搜索树 `treeRoot` 各节点的数据。第 10 行的语句输出二叉搜索树的高度。

第 12 行的语句使用成员函数 `inorderTraversal` 遍历二叉搜索树 `treeRoot`。在第 12 行中，函数 `inorderTraversal` 的实参是函数 `update`（定义于第 19 行）。函数 `update` 将其参数的值翻倍。因此，第 12 行的语句通过将该值翻倍来更新二叉搜索树每个节点的数据。第 14 行和第 15 行的语句输出二叉搜索树的节点和高度。

**注意** **(AVL 树)** 本章还讨论 AVL 树。所需材料位于文件 AVL Trees.pdf 中。该文件可在 www.cengagebrain.com 获取。要找到该文件，请通过输入本书的 ISBN 导航到该书页面，然后单击 Free Materials。

## 编程示例：DVD 商店（重访）

![](img/d0be7fc6d804b63484835c6c8bc67a07_1437_0.png)

在第 16 章中，我们设计了一个程序，帮助 DVD 商店自动化其 DVD 租赁流程。该程序使用一个（无序）链表来跟踪商店中的 DVD 库存。因为链表中的搜索算法是顺序的，而且链表相当大，所以搜索可能很耗时。在本章中，你学习了如何将数据组织成二叉树。如果二叉树构建良好（即它不是线性的），那么搜索算法可以得到显著改进。此外，一般来说，二叉搜索树中的项插入和删除比链表中更快。因此，我们将重新设计 DVD 商店程序，以便 DVD 库存可以维护在二叉树中。与第 16 章一样，我们将客户列表的二叉树设计留作你的练习。

### DVD 对象

在第 16 章中，使用链表来维护商店中的 DVD 列表。因为该链表是无序的，所以为了查看某个特定 DVD 是否有库存，顺序搜索算法使用相等运算符进行比较。然而，在二叉树的情况下，我们需要其他关系运算符来进行搜索、插入和删除操作。因此，我们将重载所有关系运算符。除了这一差异外，`dvdType` 类与之前相同。不过，为了完整性，我们给出它的定义。

```cpp
//***************************************************************
// Author: D.S. Malik
//
// class dvdType
// This class specifies the members to implement a DVD. It
// overloads the stream insertion operator and relational
// operators.
//***************************************************************

class dvdType
{
    friend ostream& operator<< (ostream&, const dvdType&);

public:
    void setDVDInfo(string title, string star1,
                    string star2, string producer,
                    string director, string productionCo,
                    int setInStock);
    //Function to set the details of a DVD.
    //The member variables are set according to
    //parameters.
    //Postcondition: dvdTitle = title; movieStar1 = star1;
    //                movieStar2 = star2;
    //                movieProducer = producer;
    //                movieDirector = director;
    //                movieProductionCo = productionCo;
    //                copiesInStock = setInStock;

    int getNoOfCopiesInStock() const;
    //Function to check the number of copies in stock.
    //Postcondition: The value of copiesInStock is returned.

    void checkOut();
    //Function to rent a DVD.
    //The number of copies in stock is decremented by one.
    //Postcondition: copiesInStock--;

    void checkIn();
    //Function to check in a DVD.
    //The number of copies in stock is incremented by one.
    //Postcondition: copiesInStock++;

    void printTitle() const;
    //Function to print the title of a movie.

    void printInfo() const;
    //Function to print the details of a DVD.
    //Postcondition: The title of the movie, stars, director,
    //              and so on are output on the screen.

    bool checkTitle(string title);
    //Function to check whether the title is the same as the
    //title of the DVD.
    //Postcondition: Returns the value true if the title is
    //              the same as the title of the DVD, and
    //              false otherwise.

    void updateInStock(int num);
    //Function to increment the number of copies in stock by
    //adding the value of the parameter num.
    //Postcondition: copiesInStock = copiesInStock + num;

    void setCopiesInStock(int num);
    //Function to set the number of copies in stock.
    //Postcondition: copiesInStock = num;

    string getTitle() const;
    //Function to return the title of the DVD.
    //Postcondition: The title of the DVD is returned.

    dvdType(string title = "", string star1 = "",
            string star2 = "", string producer = "",
            string director = "", string productionCo = "",
            int setInStock = 0);
    //Constructor
    //The member variables are set according to the incoming
    //parameters. If no values are specified, the default
    //values are assigned.
```
