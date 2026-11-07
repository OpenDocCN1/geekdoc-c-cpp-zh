
- 16. 通过添加以下函数来扩展类 `linkedListType`：

    ```cpp
    void rotate();
    //Function to remove the first node of a linked list and put it
    //at the end of the linked list.
    ```

    还要编写一个程序来测试你的函数。使用类 `unorderedLinkedList` 创建链表。

- 17. 编写一个程序，提示用户输入一个字符串，然后以 Pig Latin 形式输出该字符串。将字符串转换为 Pig Latin 形式的规则在第8章的编程示例“Pig Latin 字符串”中描述。你的程序必须将字符串的字符存储到链表中，并使用编程练习16中所述的函数 `rotate` 来旋转该字符串。

![](img/f97f778697507bb6fdd80c5991210cba_1124_0.png)

# 第18章：栈和队列

**本章中，你将：**

- 学习栈
- 考察各种栈操作
- 学习如何将栈实现为数组
- 学习如何将栈实现为链表
- 了解栈的应用
- 学习如何使用栈消除递归
- 学习队列
- 考察各种队列操作
- 学习如何将队列实现为数组
- 学习如何将队列实现为链表
- 了解队列的应用

本章讨论两种非常有用的数据结构：栈和队列。栈和队列在计算机科学中都有大量应用。

## 栈

假设你有一个包含多个函数的程序。具体来说，假设程序中有函数 A、B、C 和 D。现在假设函数 A 调用函数 B，函数 B 调用函数 C，函数 C 调用函数 D。当函数 D 终止时，控制权返回到函数 C；当函数 C 终止时，控制权返回到函数 B；当函数 B 终止时，控制权返回到函数 A。在程序执行期间，你认为计算机如何跟踪函数调用？递归函数又如何呢？计算机如何跟踪递归调用？在第17章中，我们设计了一个递归函数来反向打印链表。如果你想编写一个非递归算法来反向打印链表，该怎么办？

本节讨论一种称为**栈**的数据结构，计算机用它来实现函数调用。你也可以使用栈将递归算法转换为非递归算法，尤其是非尾递归的递归算法。栈在计算机科学中有大量应用。在开发出实现栈所需的工具之后，我们将考察栈的一些应用。

栈是相同类型元素的列表，其中元素的添加和删除只在一端进行，这一端称为栈的**栈顶**。例如，在自助餐厅中，一摞托盘中的第二个托盘只有在第一个托盘被取走后才能被取走。再比如，要拿到你最喜欢的计算机科学书，而它在你数学书和历史书下面，你必须先移走数学书和历史书。移走这些书后，计算机科学书就成为最上面的书——也就是栈的栈顶元素。图18-1展示了栈的一些示例。

![](img/f97f778697507bb6fdd80c5991210cba_1125_0.png)

栈底部的元素在栈中存放的时间最长。栈顶元素是最后添加到栈中的元素。由于元素只从一端（即栈顶）添加和删除，因此最后添加的项将最先被删除。由于这个原因，栈也称为**后进先出（LIFO）**数据结构。

**栈：** 一种只从一端添加和删除元素的数据结构；一种后进先出（LIFO）数据结构。

现在你知道了什么是栈，让我们看看可以对栈执行哪些操作。由于可以向栈中添加新项，我们可以执行添加操作，称为**入栈（push）**，将元素添加到栈上。类似地，由于可以检索和/或删除栈顶项，我们可以执行**取栈顶（top）**操作来检索栈顶元素，并执行**出栈（pop）**操作来删除栈顶元素。

push、top 和 pop 操作的工作方式如下：假设地板上放着一些箱子，需要把它们堆叠到桌子上。最初，所有箱子都在地板上，栈为空（见图18-2）。

![](img/f97f778697507bb6fdd80c5991210cba_1126_0.png)

**图18-2** 空栈

首先，我们将箱子 A 压入栈中。执行 push 操作后，栈如图18-3(a)所示。

![](img/f97f778697507bb6fdd80c5991210cba_1126_1.png)

**图18-3** 栈操作

然后，我们将箱子 B 压入栈中。执行这次 push 操作后，栈如图18-3(b)所示。接下来，我们将箱子 C 压入栈中。执行这次 push 操作后，栈如图18-3(c)所示。接下来，我们查看，也就是窥视栈顶元素。执行此操作后，栈保持不变，如图18-3(d)所示。然后，我们将箱子 D 压入栈中。执行这次 push 操作后，栈如图18-3(e)所示。接下来，我们弹出栈。执行 pop 操作后，栈如图18-3(f)所示。

只有当栈中有元素时，才能从栈中删除元素；只有当栈中有空间时，才能向栈中添加元素。由 push、top 和 pop 直接引出的两个操作是 isFullStack（检查栈是否已满）和 isEmptyStack（检查栈是否为空）。由于随着我们添加和删除元素，栈会不断变化，因此在第一次开始使用栈之前，栈必须为空。因此，我们需要另一个操作，称为 initializeStack，它将栈初始化为空状态。所以，要成功实现一个栈，我们至少需要这六个操作，下一节将描述它们。根据具体实现，我们可能还需要对栈执行其他操作。

### 栈操作

- `initializeStack`：将栈初始化为空状态。
- `isEmptyStack`：判断栈是否为空。如果栈为空，则返回值 `true`；否则返回值 `false`。
- `isFullStack`：判断栈是否已满。如果栈已满，则返回值 `true`；否则返回值 `false`。
- `push`：向栈顶添加一个新元素。此操作的输入由栈和新元素组成。在执行此操作之前，栈必须存在且不能已满。
- `top`：返回栈顶元素。在执行此操作之前，栈必须存在且不能已满。
- `pop`：删除栈顶元素。在执行此操作之前，栈必须存在且不能为空。

以下抽象类 `stackADT` 将这些操作定义为 ADT。

```cpp
template <class Type>
class stackADT
{
public:
    virtual void initializeStack() = 0;
        //Method to initialize the stack to an empty state.
        //Postcondition: Stack is empty.

    virtual bool isEmptyStack() const = 0;
        //Function to determine whether the stack is empty.
        //Postcondition: Returns true if the stack is empty.
        //              otherwise returns false.

    virtual bool isFullStack() const = 0;
    //Function to determine whether the stack is full.
    //Postcondition: Returns true if the stack is full,
    //               otherwise returns false.

    virtual void push(const Type& newItem) = 0;
    //Function to add newItem to the stack.
    //Precondition: The stack exists and is not full.
    //Postcondition: The stack is changed and newItem
    //               is added to the top of the stack.

    virtual Type top() const = 0;
    //Function to return the top element of the stack.
    //Precondition: The stack exists and is not empty.
    //Postcondition: If the stack is empty, the program
    //               terminates; otherwise, the top element
    //               of the stack is returned.

    virtual void pop() = 0;
    //Function to remove the top element of the stack.
    //Precondition: The stack exists and is not empty.
    //Postcondition: The stack is changed and the top
    //               element is removed from the stack.
};
```

图18-4展示了类 `stackADT` 的 UML 类图。

![](img/f97f778697507bb6fdd80c5991210cba_1128_0.png)

**图18-4** 类 `stackADT` 的 UML 类图

现在我们考虑抽象栈数据结构的实现。由于栈的所有元素都是同一类型，栈可以实现为数组或链式结构。这两种实现都很有用，本章将讨论它们。

