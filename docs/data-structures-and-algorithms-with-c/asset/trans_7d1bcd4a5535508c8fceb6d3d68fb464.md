

## 栈和队列

> "编程的艺术是组织复杂性的艺术"。—— W. W. Dijkstra

### 主要特性

- 栈
- 表达式求值
- 队列
- 循环队列
- 双端队列
- 优先队列

在本章中，我们将讨论栈和队列等一些基本数据结构及其属性、对其执行的不同操作、其不同操作的算法以及它们的应用。

1946年，Alan M. Turing 首先在计算机设计中提出了栈。1955年，慕尼黑工业大学的 Klaus Samelson 和 Friedrich L. Bauer 提出了栈的概念，并于1957年申请了专利。澳大利亚人 Charles Leonard Hamblin 在1957年上半年独立地发展了相同的概念。

## 栈

栈是计算机科学中最重要、最有用的非原始数据结构之一。栈的现实生活示例包括书本堆、盘子堆、卡片堆、硬币堆等。

定义：栈是元素的一个顺序集合，新元素被插入其中，且元素仅在一端被删除。

栈中的所有插入和删除操作都在栈顶进行，最后添加的元素将首先从栈中移除。这就是栈也被称为后进先出（LIFO）数据结构的原因。请注意，栈中访问频率最高的元素是栈顶元素，而最不容易访问的元素是栈底元素。

在栈中，top 变量用于指向栈顶。top 变量执行以下任务：

- 跟踪使用了多少个单元，
- 栈是否已满或为空
- 在栈中插入新元素
- 从栈中删除元素

## 栈上的操作

栈是一种抽象数据类型，因为它是通过对其执行的操作来定义的，其实现被隐藏。因此，我们可以使用数组或链表来实现栈。栈包括相同类型项目的有限序列，并具有表 6.1 中描述的不同操作。

### 表 6.1：栈上的操作

| 操作 | 描述 |
| :--- | :--- |
| 创建 | 此操作创建一个栈并初始化栈。 |
| 判空 | 此操作检查栈是否为空。 |
| 判满 | 此操作检查栈是否已满。 |
| 插入（Push） | 当栈未满时，此操作仅在栈顶插入一个项目。 |
| 删除（Pop） | 当栈非空时，此操作仅从栈顶删除一个项目。 |
| 取栈顶 | 此操作返回栈顶的值，但不从栈中移除元素。 |

插入（或添加）操作称为 push，删除（或移除）操作称为 pop。如果栈不包含任何元素，则称栈为空。此时，栈顶位于栈底。此外，当栈变满时（即无法再将其他元素压入栈中），栈为满。此时，栈顶指针位于栈的最高位置。如果在栈为空状态时执行 pop 操作，则会发生下溢。同样，如果在已满的栈上执行 push 操作，则会发生栈上溢。

作为 ADT 的栈促进了数据抽象，并关注它执行什么操作，而不是如何执行（实现）。因此，栈可以使用数组或链表来实现。

## 数组表示的栈

数组可用于实现固定大小的栈，因此只能压入和弹出固定数量的数据项。请考虑以下图 6.1，大小为 4 的栈；因此，最多只能插入 4 个数据项。top 索引始终跟踪栈中最后插入的元素，即栈顶。最初，当栈中没有项目时（即栈为空），top 被初始化为 -1（针对基于零的数组）。

![](img/723fa3ef35f5102eb67dc45b74bb823d_143_0.png)

图 6.1：栈操作

当将新项目插入栈时，在将项目存储到栈中之前，top 会先加 1。当所有四个项目都插入后，top 为 3，如图所示。现在，如果我们尝试插入下一个项目，会导致上溢条件。这表示栈已满，我们无法插入新项目。如果数组的大小为 MAXSIZE，则当 top 等于 MAXSIZE - 1 时，栈已满。

当从栈中删除项目时，在从栈中移除项目后，top 会减 1。现在，如果 top = -1，当我们尝试删除项目时，会导致下溢条件。这表示栈为空，我们无法删除项目。

因此，每当执行 push 和 pop 操作时，都需要检查这些条件。

## 向栈中插入（push）的算法

```
Algorithm: PUSH (STACK, ITEM)
[STACK is an array of MAXSIZE and ITEM is an item to be pushed onto stack]
1. [Check for stack overflow]
   If TOP = MAXSIZE - 1 then
   a) Print: Overflow
   b) Return
2. [Increment top by 1]
   Set TOP = TOP + 1
3. [Insert item in new top position]
   Set STACK[TOP] = ITEM
4. Return
```

## 从栈中删除（pop）栈顶元素的算法

```
Algorithm: POP (STACK, ITEM)
[STACK is an array and ITEM is an item to be popped from stack]
1. [Check for stack underflow]
   If TOP = -1 then
   a) Print: Underflow
   b) Return
2. [Assign top element to item]
   Set ITEM = STACK[TOP]
3. [Decrease top by 1]
   Set TOP = TOP - 1
4. Return
```

栈可以使用以下结构表示：

```
struct STACK
{
   int a[MAXSIZE];
   int top;
};
```

## 链表表示的栈

表示栈的另一种方法是使用单链表，也称为链式栈。链表是一种动态数据结构，链表中的每个元素都是一个节点，包含一个值和指向其邻居的链接。列表是指向另一个节点的指针，该节点包含一个值和指向另一个节点的另一个指针，以此类推。

链表头部充当栈的栈顶。所有 push 或 pop 操作都在链表的前端进行。每个操作始终会更改链表的头部。当栈为空时，HEAD 为 null。如果栈至少有一个节点，则第一个节点是栈顶。在 push 操作中，需要在列表前端添加一个新节点。pop 操作在栈非空时删除链表的第一个节点。

## 使用链表的 push 操作算法

```
Algorithm: PUSH (HEAD, ITEM)
[HEAD is a pointer to the first node and ITEM is an item to be pushed onto stack]
1. [Create the new node]
   Allocate memory for NEW node
2. If NEW = NULL then
   i) Print: Out of memory
   ii) Return
3. Set NEW→DATA = ITEM
4. Set NEW→LINK = HEAD
5. Set HEAD = NEW
6. Return
```

## 使用链表的 pop 操作算法

```
Algorithm: POP (HEAD, ITEM)
[HEAD is a pointer to the first node and ITEM is an item to be popped from stack]
1. [Whether List is empty]
   If HEAD = NULL then
   i) Print: Stack is underflow
   ii) Return
2. ITEM = HEAD→DATA
3. Set P = HEAD
4. HEAD = HEAD→LINK
5. Set P→LINK = NULL
6. De-allocate memory for node P
7. Return
```

## 使用链表或数组表示栈的比较

- 数组大小固定，因此栈中的元素数量受到限制。由于链表是动态的且可以轻松更改，因此元素数量可以更改。
- 与数组相比，链表中的指针会消耗额外内存。
- 在数组和链表中，push 和 pop 操作均可在 O(1) 时间内完成。

## 栈的应用

栈是一种非常有用的数据结构。大多数现代计算机和微处理器都提供内置的硬件栈。甚至还有面向栈的计算机体系结构。

1. 栈的一个非常重要的应用是实现递归函数调用和函数调用的处理，例如传递参数。
2. 算术表达式求值。
3. 模拟递归。
4. 作用域规则和块结构也可以使用栈来实现。栈用于编译器、系统程序、操作系统以及许多优雅的应用算法的开发中。
5. 栈用于实现不同的算法，如深度优先搜索、快速排序、归并排序等。

## 函数调用的处理

栈最重要的应用之一是子程序调用及其终止的处理。

程序必须记住调用发生的位置，以便在子程序完成后可以返回。

假设我们有三个名为 A()、B()、C() 的子程序和一个主程序，main() 调用 A()，A() 调用 B()，B() 反过来调用 C()。那么，B 在 C() 完成并返回之前不会完成其工作。同样，main() 是最先开始工作的，但却是最后完成的。

![](img/723fa3ef35f5102eb67dc45b74bb823d_146_0.png)

图 6.2：函数调用处理

这些函数调用会按照调用顺序连同其参数一起被压入栈中，并按照从栈中弹出的顺序进行处理。用于函数调用的栈通常在物理内存中以逆序实现。这意味着栈顶位于最后一个地址。

