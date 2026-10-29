

```
front = back;
//创建第一个节点并填入数据。
//现在新节点将添加在此第一个节点之后。

temp = temp->getLink( );//现在temp指向第二个
//节点；如果没有第二个节点则为NULL。

while (temp != NULL)
{
    back->setLink(new Node<T>(temp->getData( ), NULL));
    back = back->getLink( );
    temp = temp->getLink( );
}
//back->link == NULL
```

18. 以下内容应放在命名空间 `QueueSavitch` 中：

```
//Uses cstddef:
template<class T>
Queue<T>& Queue<T>::operator =(const Queue<T>& rightSide)
{
    if (front == rightSide.front)//if the queues are the same
        return *this;
    else //send left side back to freestore
    {
        T next;
        while (! isEmpty( ))
            next = remove( );//remove calls delete.
    }

    if (rightSide.isEmpty( ))
    {
        front = back = NULL;
        return *this;
    }
    else
    {
        Node<T> *temp = rightSide.front;//temp moves
        //through the nodes from front to back of rightSide.

        back = new Node<T>(temp->getData( ), NULL);
        front = back;
        //First node created and filled with data.
        //New nodes are now added AFTER this first node.

        temp = temp->getLink( );//temp now points to second
```

```
preorderShow(subTreeRoot->rightLink);
}
```

```
template<class T> //uses iostream:
void SearchTree<T>::postorderShow() const
{
    postorderShow(root);
}
```

```
template<class T> //uses iostream:
void SearchTree<T>::postorderShow(
    TreeNode<T>* subTreeRoot) const
{
    if (subTreeRoot != NULL)
    {
        postorderShow(subTreeRoot->leftLink);
        postorderShow(subTreeRoot->rightLink);
        cout << subTreeRoot->data << " ";
    }
}
```

## 编程项目

- 1. 编写一个 void 函数，该函数接受一个整数链表并反转其节点的顺序。该函数将有一个按引用传递的参数，该参数是指向链表头部的指针。函数调用结束后，该指针将指向一个新链表的头部，新链表包含与原始链表相同的节点，但顺序与原始链表中的顺序相反。请注意，你的函数既不会创建也不会销毁任何节点，它只是重新排列节点。将你的函数放入一个合适的测试程序中。

- 2. 编写一个名为 `mergeLists` 的函数，该函数接受两个按引用传递的参数，这两个参数是指向 int 类型链表头部的指针变量。假定这两个链表已排序，使得头部的数字最小，依此类推。该函数返回一个指针，指向一个新链表的头部，新链表包含原始两个链表中的所有节点。这个更长链表中的节点也按从小到大的顺序排序。请注意，你的函数既不会创建也不会销毁任何节点。当函数调用结束时，两个指针变量参数的值应为 `NULL`。

- 3. 设计并实现一个用于多项式的类。多项式 aₙxⁿ + aₙ₋₁xⁿ⁻¹ + ... + a₀ 将实现为链表。每个节点将包含一个 int 值表示 x 的幂，以及一个 int 值表示相应的系数。类的操作应包括加法、减法、乘法和多项式求值。重载运算符 +、- 和 * 分别用于加法、减法和乘法。多项式的求值实现为一个成员函数，其参数为 int 类型。求值成员函数返回将参数代入 x 并执行指定运算后得到的值。

  包含四个构造函数：一个默认构造函数，一个复制构造函数，一个带单个 int 类型参数的构造函数（该构造函数生成一个仅包含一个常数项的多项式，该常数项等于构造函数的参数），以及一个带两个 int 类型参数的构造函数（该构造函数生成一个单项式，其系数和指数由这两个参数给出）。[在前面的表示法中，单参数构造函数生成的多项式是仅由 a0 组成的简单形式。双参数构造函数生成的多项式是稍微复杂的 a0x^n 形式。] 包含一个合适的析构函数。包含用于输入和输出多项式的成员函数。

  当用户输入多项式时，用户输入以下形式：
  a_n x^n + a_{n-1} x^{n-1} + ... + a0

  然而，如果某个系数 a_i 为 0，用户可以省略项 a_i x^i。例如，多项式
  3x^4 + 7x^2 + 5
  可以输入为
  3x^4 + 7x^2 + 5

  也可以输入为
  3x^4 + 0x^3 + 7x^2 + 0x^1 + 5

  如果系数为负数，则使用减号代替加号，如下例所示：
  3x^5 - 7x^3 + 2x^1 - 8
  -7x^4 + 5x^2 + 9

  多项式开头的减号（如上面第二个例子所示）仅适用于第一个系数；它并不对整个多项式取负。多项式以相同的格式输出。在输出时，系数为 0 的项不输出。为了简化输入，你可以假定多项式总是每行输入一项，并且总是存在常数项 a0。如果没有常数项，用户输入 0 作为常数项，如下所示：
  12x^8 + 3x^2 + 0

- 4. 部分 A。显示 17.24 中的注释说明，一个真正的 SearchTree 模板类应该有一个复制构造函数、一个重载的赋值运算符、其他重载的运算符以及其他成员函数。获取显示 17.24 的代码，并为以下函数和重载运算符添加声明：

  ![](img/9505fd46e120aa9c1406715936ff6251_748_0.png)

  默认构造函数、复制构造函数、delete、重载运算符 =、makeEmpty、height、size、preOrderTraversal、inOrderTraversal 和 postOrderTraversal。函数 preOrderTraversal、inOrderTraversal 和 postOrderTraversal 各自调用一个全局函数 process 来处理遇到的节点。函数 process 是 SearchTree 类的友元，在本练习中它只是一个存根（stub）。
  为这些函数提供前置条件和后置条件，描述每个函数应完成的工作。

  函数 height 没有参数，返回树的高度。树的高度是所有节点高度的最大值。节点的高度是它到根节点之间的链接数。

  函数 size 没有参数，返回树中节点的数量。

  函数 makeEmpty 从树中移除所有节点，并将节点占用的内存返还以供复用。makeEmpty 函数将根指针置为 NULL。

  部分 B。实现成员函数、友元函数和重载运算符。请注意，此处列出的一些函数已在正文中实现。你应充分利用正文中的代码。你应全面测试你的包。

  部分 C：为树类设计并实现一个迭代器类。你需要确定对于你的 searchTree 来说，begin 和 end 元素分别代表什么，以及 ++ 运算符指向的下一个元素是什么。

  提示 1：你可以维护一个私有的 size 变量，该变量在插入时增加，在删除时减少，其值由 size 函数返回。另一种方法（如果你知道对 size 的调用将非常少，则使用此方法）是在需要时通过遍历树来计算大小。类似的技术（尽管细节更复杂）可以用来实现 height 函数。

  提示 2：一次只编写其中几个成员。在完成每组少量成员后编译并测试。你会发现这样做是值得的。

  提示 3：在编写运算符 = 和复制构造函数之前，请注意它们的任务有一个共同点——复制另一棵树。编写一个 copyTree 函数，将复制构造函数和运算符 = 的共同任务抽象出来。然后使用这些公共代码编写这两个重要的函数。

  提示 4：函数 makeEmpty 和析构函数有一个共同的树销毁任务。

