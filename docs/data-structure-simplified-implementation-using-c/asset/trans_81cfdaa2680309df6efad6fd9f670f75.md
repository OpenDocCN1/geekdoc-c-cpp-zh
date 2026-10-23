

- 每个节点应包含上述信息。考虑学生总数为 20 的情况。将数据保存在双向链表本身中。编写一个函数，根据总成绩对双向链表的记录（节点）进行组织。例如，获得最高成绩的学生应放在第一位，然后是第二高，依此类推。编写一个函数，在给定的双向链表中搜索节点（记录）。
- 在上述程序的基础上，在双向链表中增加一个数据成员。该数据成员的名称应为 count。根据记录（节点）被搜索的次数，count 的值应递增 1。重新排列节点。例如，如果第 4 个节点的 count 最大，则应将其置于第一位。

## EXERCISE

### A. Descriptive Questions

- 1. 编写一个函数，在双向链表中不遍历双向链表的情况下，在最后一个节点之后插入新节点。
- 2. 修改上述函数，使其无需检查第一个节点是否为 NULL。
- 3. 编写一个函数，在双向链表中插入新节点。函数应管理以下内容：
  a. 列表是否存在。
  b. 给定的位置是否在允许范围内。例如，如果节点总数为 5，而要插入节点的位置为 8，则不允许。
- 4. 编写一个函数，根据以下因素在双向链表中删除节点：
  a. 基于现有列表。
  b. 考虑给定的位置是否在允许范围内。例如，如果节点总数为 5，而要删除节点的位置为 8，则不允许。
  c. 根据用户接收到的值删除节点。
- 5. 编写一个函数从双向链表中删除一个节点。
- 6. 删除双向链表的第一个节点。
- 7. 删除位于中间的节点（除第一个和最后一个之外）。
- 8. 删除位于末尾的节点。
- 9. 删除节点后相应地调整指针。例如，如果删除了最后一个节点，则前一个节点必须指向 NULL，因为现在倒数第二个节点充当最后一个节点。

### B. Multiple Choice Questions

1. 用于定义双向链表结构的类的大小是多少。
a. 02 bytes        c. 40 bytes.
b. 06 bytes        d. 12 bytes.

2. 我们可以通过包含指针作为参数来修改现有的 create 函数吗？
a. Yes
b. No.
（写下支持和反对你陈述的要点并请其核实）。

3. 如果 current 指向双向链表的当前节点。要访问 current 节点前面的两个节点，可以使用以下语句。
a. current->next        c. current->next->next
b. current->next->prev        d. None of these

4. 如果 current 指向当前节点并且 forward 指向 current 前面的一个节点。那么代码 forward->prev 指向
a. Current node.        b. One node ahead of the forward node.
c. One node previous to the current node.
d. None of these

5. 在上述问题中，要删除位于双向链表的第一个节点和最后一个节点之间的节点，代码 current->next 删除 forward 节点：
a. True
b. False

考虑我们已经在栈中有三个元素的情况，因此栈将指向顶部位置。在图 5.2 中，栈的顶部元素是‘C’，因此 top 位于索引 2。一旦弹出一个项目，则 top 将递减一个索引并指向‘B’（参见图 5.2 b）

**Note:** 除了 push 和 pop 操作之外，还可以对栈执行另一种可能的运算，称为 NoOperation(Nop)。在 Nop 中，没有任何操作发生。换句话说，top 没有移动；相反，在不移动 top 的情况下进行活动。例如，显示栈中的元素就属于此类，因为它不涉及栈顶的移动。确定栈顶元素的另一个例子也与 Nop 相关，其中栈顶元素将被返回而不会移动 top 指针。

## 5.4 IMPLEMENTATIONS OF STACK

栈是计算机科学中广泛使用的数据结构，使用栈可以提高整体性能，同时简化代码。在栈中，有时我们事先知道需要插入的最大元素数量。然而，有时要插入的项目数量无法准确预测。相应地，为满足这些需求，栈被分为以下几类：

- Static stack
- Dynamic stack

在栈中，如果可以预先预测可以插入的项目总数，则此类栈可以用数组实现并称为 **static stack**。此类栈相对于其他类型的栈具有更好的性能。

在无法获知要插入的项目总数或要插入的最小项目数与最大项目数之间的变化很大的情况下，我们使用另一种称为 **dynamic stack** 的栈。但该栈涉及与内存分配和释放相关的性能开销。

### 5.4.1 Static Stack

静态栈是借助数组实现的。在创建栈之前，必须定义其结构以确定它将保存的信息类型。另一个约束与指向栈顶的 top 指针有关。表示数据成员和可在数据成员上完成的操作的类如下所示：

```
Program for the push, pop and display function of the static stack.
// Program that depicts push and pop operation on the stack
const int size=5; // size of the stack
// Defining the structure of the stack
class stk
{
int stack[size];
int top;
public:
// constructor to initialize the value of top
stk()
{
top=-1;
}
// To push the element in the stack
int push(int);
//To pop the element from the stack and return the top/pop element
int pop();
// To display the items in the stack.
void display();
// To display the number of element in the stack.
void count_elements();
// To examine whether the stack is empty or not
int isEmpty();
};
```

最初，栈为空，并通过将 top 的值赋为 -1 来表示。每当向栈中插入一个项目时，都会检查其容量（由 size 表示）以避免溢出。如果栈未满，则只允许将项目插入栈中。相应地，top 指针递增 +1 以表示 top 的新位置。

Push 函数返回整数值。该值用于确定 push 操作是否成功或不成功。如果成功，push 函数返回 1，而在失败的情况下，它返回 0。

```
// function to implement the push operation of stack.
int stacks::push(int element)
{
    if(top==(size-1))
    {
cout<<"overflow, more elements cannot be inserted \n";
return 0;
    }
    else
{
    stack [++top] =element;
}
return 1;
}
```

要从栈中弹出元素，首先我们会检查空条件。如果栈为空，则会向用户显示 underflow 消息。为了检查空条件，我们检查与 top 变量关联的值。

if (top== -1)

值 -1 表示空条件。如果栈中有多于零个元素，则可以执行 pop 操作。在 pop 操作之前，栈顶元素存储在 temp 变量中。之后，top 向下移动一个指针，最后将存储在 temp 变量中的 top 的值返回给调用函数，以供以后使用（如有需要）。

```
//function to pop the element from the stack
int stacks::pop ()
{
    int temp=0;
    // Examine whether stack is empty or not.
    if (top==-1)  // top=-1 indicates the empty state of stack
    {
        cout<<"underflow: \n";
    }
    else
    {
        temp=stack [top--];
    }
    return temp;
}
```

我们还设计了 isEmpty () 函数来确定栈是否为空。isEmpty() 函数可以在多个地方使用，例如在任何时间点确定栈中的元素数量。在执行 pop 操作之前可以使用此函数。如果栈为空，则不允许 pop，相反需要向用户显示合适的消息。它返回 1 表示 true，如果栈为空，否则返回 0 表示 false。相同的内容已在以下程序中说明。

