

```cpp
nodePtr = new BSTNode();
/*
  ... 将传递给函数的值拷贝到新
节点中并 ...
*/
nodePtr -> setVal(pValue);
/*
  ... 返回。
*/
return;
}

/* 
如果当前节点中的值大于传递的
值...（源文件中省略了注释的剩余部分）
*/
if(nodePtr -> getVal() > pValue)
{
  /*
  ... 从左
子节点开始递归地调用
  该函数。
*/
  insert(nodePtr -> getLeft(), pValue);
}

/*
如果当前节点中的值小于传递的
值...（源文件中省略了注释的剩余部分）
*/
if(nodePtr -> getVal() < pValue)
{
  /*
  ... 从右
子节点开始递归地调用
  该函数。
*/
  insert(nodePtr -> getRight(), pValue);
}
```

这个看起来很复杂的函数实际上非常简单。让我们先考虑树为空的情况（列表 9.35）。

## **Listing 9.35** 测试 insert() 函数

```cpp
/*Beginning of BSTInsert01.cpp*/
#include "BST.h"
void main()
{
  BST tree1;
  tree1.insert(20);
}
/*End of BSTInsert01.cpp*/
```

上述程序中的第一个语句将创建一个名为 tree1 的 BST 类对象。图 9.69 描绘了 tree1 在内存中被创建后的状态。

| 地址 | 值 |
| :--- | :--- |
| 2172 | NULL |
| NULL | root |
| tree1 | |

图 9.69 一个 BST 类对象。

根据 BST 类的定义，tree1 只有一个数据成员，称为 root。该对象的地址是 2172。由于 root 是对象的唯一数据成员，它的地址也是 2172。请记住，当树为空时，root 指针的值将为 NULL。

上述程序中的第二个语句如下所示调用公共 insert() 函数：

```cpp
tree1.insert(20);
```

这反过来将如下所示调用私有函数：

```cpp
insert(root, 20);
```

注意，nodePtr 是私有函数的第一个形式参数，是一个引用类型变量。因此，作为上述调的结果，nodePtr 最终将成为 root 指针的引用。因此，nodePtr 值的任何更改都会导致 root 指针值发生相同的变化。这是一个非常重要的点，必须牢记。。此外，作为第二个形式参数的 pValue 值将被设置为 20。产生的结果如图 9.70 所示。

| 地址 | 值 |
| :--- | :--- |
| 2172 | NULL |
| NULL | root |
| 2172 | NULL |
| NULL | nodePtr |
| 3922 | | |
| 20 | pValue |

图 9.70 调用 insert() 函数后产生的情况。

所示，root 和 nodePtr 具有相同的地址，均为 2172。这是因为 nodePtr 是 root 的引用。自然地，它们具有相同的值。pValue 是一个独立的整数变量，其值为 20。

现在，函数将开始执行。在第一个 if 语句块的测试表达式中，将测试 nodePtr 的值是否为 NULL。该语句块将返回真，因为 root 指针的值为 NULL，且 nodePtr 的值与 root 指针的值相同。

if 语句块将执行。将创建一个节点，其地址将被拷贝到 root，使其与新创建的 nodePtr 的地址相等，如图 9.71 所示，nodePtr 是 root 的引用。假设新创建节点的地址为 6221，则 root 和 nodePtr 的值都将变为 6221。这就是将 nodePtr 声明为引用变量的重要性。

![](img/5bfa77b13fdaa376725789bb8c00ee79_376_0.png)

图 9.71 添加到 root 指针的新节点。

if 语句块中的下一个语句将 pValue 的值拷贝到新创建节点的数据部分，从而产生图 9.72 所示的情况。

![](img/5bfa77b13fdaa376725789bb8c00ee79_376_1.png)

图 9.72 为新创建的节点填充数据。

最后，if 语句块的最后一个语句将导致函数返回，函数的剩余部分将不再执行。局部变量 nodePtr 和 pValue 将超出作用域。我们将剩下 root 指针和新创建的节点。因此，一个值为 20 的新节点将被添加到树中。图 9.73 显示了创建的树的样子。

![](img/5bfa77b13fdaa376725789bb8c00ee79_376_2.png)

图 9.73 insert() 函数结束时的情况。

因此，显然 insert() 函数在树为空时可以正常工作。现在让我们考虑树不为空的情况（列表 9.36）。

## **Listing 9.36** 测试 insert() 函数

```cpp
/*Beginning of BSTInsert02.cpp*/
#include "BST.h"
void main()
{
    BST tree;
    tree1.insert(20);
    tree1.insert(10);
}
/*End of BSTInsert02.cpp*/
```

我们已经知道，在上述 main() 函数的第二个语句结束时，场景将如图 9.74 所示。

![](img/5bfa77b13fdaa376725789bb8c00ee79_377_0.png)

## **Figure 9.74** 第一次调用 insert() 函数后 BST 的结构。

我们从图中可以看出，当 main() 函数中的第三条语句开始时，树并不为空。第三条语句是：

`tree1.insert(10);`

我们知道这反过来将如下所示调用私有 'insert() ' 函数：

`insert(root, 10);`

与之前一样，nodePtr 最终将成为 root 的引用，nodePtr 的值如图 9.75 所示。

![](img/5bfa77b13fdaa376725789bb8c00ee79_377_1.png)

## **Figure 9.75** 第二次调用 insert() 函数后 BST 的结构。

现在，函数将开始执行。在第一个 if 语句块的测试表达式中，将测试 nodePtr 的值是否为 NULL。该语句块将返回真，因为 root 指针的值为 NULL，且 nodePtr 的值与 root 指针的值相同。

if 语句块将执行。将创建一个节点，其地址将被拷贝到 root，使其与新创建的 nodePtr 的地址相等，如图 9.71 所示，nodePtr 是 root 的引用。假设新创建节点的地址为 6221，则 root 和 nodePtr 的值都将变为 6221。这就是将 nodePtr 声明为引用变量的重要性。

（注：原文中后续 377-380 部分存在文本重复和乱码，已根据前文逻辑进行处理。）

