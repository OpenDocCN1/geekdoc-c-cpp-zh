
```
{
    push current and 1 onto stack;
    current = current->rlink;
}
else
{
    assign the top element of stack to current and v;
    pop stack;
    if (v == 1)
    {
        push current and 2 onto stack;
        current = current->rlink;
        v = 0;
    }
    else
    {
        visit current;
    }
}
```

我们将使用两个（并行）栈：一个用于保存指向节点的指针，另一个用于保存与该指针关联的整数值（1 或 2）。我们将实现上述后序遍历算法的 C++ 函数定义留作练习。请参见本章末尾的编程练习 6。

## 二叉树遍历与函数作为参数

假设你已将员工数据存储在二叉搜索树中，并且要在年底为每位员工加薪或发放奖金。此任务要求访问二叉搜索树中的每个节点，并更新每位员工的工资。前面几节讨论了遍历二叉树的各种方法。然而，在这些遍历算法——中序、前序和后序——中，每当我们访问一个节点时，为了简单和演示目的，我们只输出每个节点中包含的数据。我们如何使用遍历算法访问每个节点并更新每个节点中的数据？一种方法是先创建另一棵二叉搜索树，其中每个节点中的数据是原二叉搜索树更新后的数据，然后销毁旧的二叉搜索树。这将需要额外的计算机时间，可能还需要额外内存，因此效率不高。另一种解决方案是编写单独的遍历算法来更新数据。该解决方案要求你频繁修改实现二叉搜索树的类的定义。然而，如果用户可以编写适当的函数来更新每位员工的数据，然后将该函数作为参数传递给遍历算法，我们就可以显著增强程序的灵活性。本节描述如何将函数作为参数传递给其他函数。

在 C++ 中，不带任何括号的函数名被视为指向该函数的指针。要将函数指定为另一个函数的形参，我们需要指定函数类型，后跟作为指针的函数名，再后跟该函数的参数类型。例如，考虑以下语句：

```cpp
void fParamFunc1(void (*visit) (int));       //Line 1
void fParamFunc2(void (*visit) (employee&));  //Line 2
```

第 1 行中的语句声明 `fParamFunc1` 是一个函数，它接受任何带有一个 `int` 类型值参数的 `void` 函数作为参数。第 2 行中的语句声明 `fParamFunc2` 是一个函数，它接受任何带有一个 `employee` 类型引用参数的 `void` 函数作为参数。

现在我们可以重写，比如说，`class binaryTreeType` 的中序遍历函数。或者，我们可以重载现有的中序遍历函数。为了进一步说明函数重载，我们将重载中序遍历函数。因此，我们在 `class binaryTreeType` 的定义中包含以下语句。

```cpp
void inorderTraversal(void (*visit) (elemType&)) const;
    //Function to do an inorder traversal of the binary tree.
    //The parameter visit, which is a function, specifies
    //the action to be taken at each node.
    //Postcondition: The action specified by the function
    //              visit is applied to each node of the
    //              binary tree.
    //

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
    if (p != NULL)
    {
        inorder(p->llink, *visit);
        (*visit) (p->info);
        inorder(p->rlink, *visit);
    }
}
```

语句：

```cpp
(*visit) (p->info);
```

在函数 `inorder` 的定义中，该语句会调用由指针 `visit` 所指向的、带有一个 `elemType` 类型引用参数的函数。

示例 20-4 进一步说明了如何将函数作为参数传递给其他函数。

### 示例 20-4

此示例展示如何将用户定义的函数作为参数传递给二叉树遍历算法。为便于说明，我们仅展示如何使用中序遍历函数。

以下程序使用派生自 `class binaryTreeType` 的类 `bSearchTreeType` 来构建二叉树。遍历函数包含在 `class binaryTreeType` 中，并由 `class bSearchTreeType` 继承。

```cpp
#include <iostream>
#include "binarySearchTree.h"

using namespace std;

void print(int& x);
void update(int& x);

int main()
{
    bSearchTreeType<int> treeRoot;                  //Line 1

    int num;                                         //Line 2

    cout << "Line 3: Enter numbers ending "
         << "with -999." << endl;                  //Line 3
    cin >> num;                                      //Line 4

    while (num != -999)                             //Line 5
    {
        treeRoot.insert(num);                        //Line 6
        cin >> num;                                  //Line 7
    }

    cout << endl
         << "Line 8: Tree nodes in inorder: ";     //Line 8
    treeRoot.inorderTraversal(print);                //Line 9
    cout << endl << "Line 10: Tree Height: "
         << treeRoot.treeHeight()
         << endl << endl;                            //Line 10

    cout << "Line 11: ******* Update Nodes "
         << "*******" << endl;                       //Line 11
    treeRoot.inorderTraversal(update);               //Line 12

    cout << "Line 13: Tree nodes in inorder "
         << "after the update: " << endl
         << "             ";                         //Line 13
    treeRoot.inorderTraversal(print);                //Line 14

    cout << endl << "Line 15: Tree Height: "
         << treeRoot.treeHeight() << endl;           //Line 15

    return 0;                                        //Line 16
}

void print(int& x)                                  //Line 17
{
    cout << x << " ";                              //Line 18
}

void update(int& x)                                 //Line 19
{
    x = 2 * x;                                      //Line 20
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```
Line 3: Enter numbers ending with -999.
56 87 23 65 34 45 12 90 66 -999

Line 8: Tree nodes in inorder: 12 23 34 45 56 65 66 87 90
Line 10: Tree Height: 4

Line 11: ******* Update Nodes *******
Line 13: Tree nodes in inorder after the update:
        24 46 68 90 112 130 132 174 180
Line 15: Tree Height: 4
```

该程序的工作方式如下。第 1 行中的语句声明 treeRoot 为一个二叉搜索树对象，其中每个节点中的数据类型为 int。第 4 行到第 7 行中的语句构建二叉搜索树。第 9 行中的语句使用 treeRoot 的成员函数 inorderTraversal 遍历二叉搜索树 treeRoot。第 9 行中传给函数 inorderTraversal 的参数是函数 print（定义于第 17 行）。由于函数 print 输出其参数的值，第 9 行中的语句输出二叉搜索树 treeRoot 的节点数据。第 10 行中的语句输出二叉搜索树的高度。

第 12 行中的语句使用成员函数 inorderTraversal 遍历二叉搜索树 treeRoot。在第 12 行中，函数 inorderTraversal 的实参是函数 update（定义于第 19 行）。函数 update 将其参数的值加倍。因此，第 12 行中的语句通过将数据加倍来更新二叉搜索树每个节点中的数据。第 14 行和第 15 行中的语句输出二叉搜索树的节点和高度。

> **注意（AVL 树）** 本章还讨论 AVL 树。所需材料在文件 AVL Trees.pdf 中。该文件位于随本书提供的网站 `www.course.com/malik/cpp` 上。
