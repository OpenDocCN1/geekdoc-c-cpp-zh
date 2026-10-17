
```cpp
JustTesting *pc1, *pc2;

pc1 = new (buffer) JustTesting; // 将对象放入缓冲区

pc2 = new JustTesting("Heap1", 2); // 在堆上创建对象

// (此处由于原文重复，已按核心逻辑翻译)

delete pc2; // 释放堆

delete[] buffer; // 释放缓冲区

return 0;

}
```

# 使用指针指向对象

```cpp
private:
    string words;
    int number;
public:
```

```cpp
JustTesting(const string & s = "Just Testing", int n = 0)
{
    words = s; number = n; cout << words << " constructed\n";
}
~JustTesting() { cout << words << " destroyed\n"; }
void Show() const { cout << words << " " << number << endl; }
int main()
{
    char * buffer = new char[BUF]; // 获取一块内存
    JustTesting *pc1, *pc2;
    pc1 = new (buffer) JustTesting(); // 将对象置于缓冲区中
    pc2 = new JustTesting("Heap1", 20); // 将对象置在堆上
    cout << "Memory addresses:\n";
    cout << "buffer: " << (void*) buffer << " heap: " << (void*) pc2 << endl;
    cout << "Memory contents:\n";
    cout << pc1 << "\n";
}
```

以下是列表 12.9 中程序的输出：

```
Just Testing constructed
Heap1 constructed
Memory block addresses:
buffer: 00320AB0 heap: 00320CE0
Memory contents:
0320AD0: Just Testing, 0
0320CE0: Heap1, 20
Better Idea constructed
Heap2 constructed
Memory contents:
0320AD: Better Idea, 6
0320EC8: Heap2, 10
Heap1 destroyed
Heap2 destroyed
Better Idea destroyed
Just Testing destroyed
Done
```

列表 12.9 中的程序将两个定位 `new`（placement new）对象放置在相邻的位置，并调用了相应的析构函数。

# 技术复习

到为止，你已经遇到了几种处理各种类相关问题的编程技术，你可能在记住所有这些技术方面遇到困难。以下章节总结了几种技术及其使用时机。

# 重载 `<<` 运算符

为了重定义与 `cout` 配合使用的显示对象内容的 `<<` 运算符，你需要定义一个如下形式的友元运算符 `&<<`：

```cpp
ostream & operator<< (ostream & os, const c_name & obj)
{
  os << obj; // 显示对象内容
  return os;
}
```

这里 `c_name` 代表类名。如果该类提供了公共方法来返回所需内容，你可以在运算符函数中使用这些方法，而无需使用友元 状态。

# 转换函数

要将单个值转换为类类型，你需要创建一个具有以下原型的类构造函数：
`c_name(type_name value);`

这里 `c_name` 代表类名，`type_name` 代表你想要转换的类型名称。
要将类类型转换为其他类型，你需要创建一个具有以下原型的类成员函数：
`operator type_name();`
尽管此函数没有声明返回类型，但它应该返回一个目标类型的值。
请记住谨慎地使用转换函数。在声明构造函数时可以使用 `explicit` 关键字来防止其被用于隐式转换。

# 构造函数使用 `new` 的类

在设计使用 `new` 运算符来分配类成员所指向的内存的类时，你需要采取几项注意事项（是的，我们最近总结了这些注意事项，但记住这些规则非常重要，特别是因为编译器并不知道它们，也不会计算你的错误）：

- 任何指向由 `new` 分配内存的类成员都应该在类的析构函数对其应用 `delete` 运算符。这会释放内存。
- 如果析构函数通过对类成员指针应用 `delete` 来释放内存，则该类的每个构造函数都应该初始化该指针，要么使用 `new`，要么将指针设置为空指针。
- 构造函数应该统一使用 `new []` 或 `new`，而不要混合使用。如果构造函数使用 `new []`，则析构函数应该使用 `delete []`。
- 你应该定义一个分配内存而非拷贝现有类的构造函数。该构造函数具有以下原型：
`className(className &)`
- 你应该定义一个重载赋值运算符的类成员函数，其原型如下（其中 `pointer` 是该类的成员）。以下示例假设构造函数使用了 `new []`：

# 第12章 类与动态内存分配

```cpp
c_name & c_name::operator=(const c_name & cn)
{
    if (this == &cn)
        return *this; // 如果自赋值则完成
    delete [] pointer;
    // 将 type_name 单元设置为
    pointer = new type_name[size];
    // 拷贝 pointer 指向的数据
    ...
    return *this;
}
```

# 队列模拟

让我们把对类的改进理解应用于编程问题。Heather 超市想在超市中使用自动柜员机（ATM）。Heather 的管理层担心 ATM 会干扰市场流量，并希望限制排队人数。他们想要客户等待多久。你的任务是准备一个模拟该情况的程序，以便管理层查看其影响。

表示该问题的自然方法是使用队列。队列是一种抽象数据类型（ADT），它存储有序序列。新元素添加到队列尾部，元素可以从头部移除。队列类似于栈，但栈是 LIFO（后进先出）结构，而队列是 FIFO（先进先出）结构。从概念上说，队列就像结账处或 ATM，因此它非常适合这项任务。你的项目的一部分是定义一个队列类。（在第16章中，你将学习标准模板库类，但自己实现比只阅读它们受益更多。）

队列模拟 681

![](img/cd111a87c1db9aff4db4b18834327463_695_0.png)

图 12.8 链表。

```cpp
class Queue
private:
// 类作用域定义
// Node 是一个局限于此类的嵌套结构体定义
struct Node {Item item; struct Node *next};
enum {Q_SIZE = 10};
// 私有类成员
Node * front;      // 指向队列头的指针
Node * rear;       // 指向队列尾的指针
int items;          // 队列中当前项目数
const int qsize;   // 队列的最大项目数
public:
// ...
};
```

该声明使用了 C++ 在类内部嵌套结构体或类声明的能力。通过将 `Node` 声明放置在 `Queue` 类内部，你赋予了它类作用域。这意味着，`Node` 是一个你可以用它来声明类成员并在类方法中作为名称的类型，但该类型被限制在类内部。这样你就不必担心 `Node` 的声明会与某些全局声明或在其他类内部声明的 `Node` 冲突。一些过时的编译器不支持嵌套结构体和类。如果你的编译器不支持，那么你必须在全局定义一个 `Node` 结构体，赋予它文件作用域。

# 嵌套结构体与类

在类声明内部声明的结构体、类或枚举被称为嵌套在类中。它具有类作用域。这种声明不会创建数据对象，而是指定了一个可以在类内部使用的类型。如果声明是在类的私私有部分进行的，那么通过使用作用域解析运算符，声明的类型也可以在类外部使用。例如，如果 `Node` 声明在 `Queue` 类的公共部分，你可以在 `Queue` 类外部声明类型为 `Queue::Node` 的变量。

在确定了数据表示形式后，下一步是编写类方法。

# 类方法

类构造函数应该为类成员提供值。由于示例中的队列从空状态开始，你应该将 `front` 和 `rear` 指针设置为 `NULL`（或 `nullptr`），并将 `items` 设置为 0。此外，你还应该将最大队列尺寸 `qsize` 设置为构造函数参数 `qs`。这里有一个不可行的实现：

```cpp
Queue::Queue(int qs) {
    front = rear = NULL;
    items = 0;
    qsize = qs;    // 不可接受！
}
```

问题在于 `qsize` 是 `const`，所以它可以被初始化为一个值，但不能被赋值赋值。从概念上讲，调用构造函数会在括号内的代码执行之前创建一个对象。因此，调用 `Queue(int qs)` 构造函数会导致程序首先为四个成员变量分配空间。然后程序进入括号，并使用普通的赋值将值放入分配的空间中。因此，如果你想初始化一个 `const` 成员，必须在对象创建时、在执行到达构造函数体之前完成。C++ 提供了一种特殊的语法来执行该操作，被称为**成员初始化列表**。成员初始化列表由冒号开头的逗号分隔的初始化列表组成。它位于参数列表的右括号之后、函数体左大括号之前。如果一个数据成员名为 `mdata` 且要将其初始化为值 `val`，则初始化器的形式为 `mdata(val)`。使用这种表示法，你可以这样写 `Queue` 构造函数：

```cpp
Queue::Queue(int qs) : qsize(qs)    // 将 qsize 初始化为 qs {
    front = rear = NULL;
    items = 0;
}
```

通常，初始值可以包含常量和来自构造函数参数列表的参数。这种技术不仅限于初始化常量；你也可以这样写 `Queue` 构造函数：

```cpp
Queue::Queue(int qs) : qsize(qs), front (NULL), rear (NULL), items(0) {
```

只有构造函数可以使用这种初始化列表语法。正如你所见的，你必须为 `const` 类成员使用这种语法。你还必须为声明为引用的类成员使用它：

```cpp
class Agent {
private:
    Agent& belong;    // 必须使用初始化列表来初始化
};
Agent::Agent(Agent & a) : belong(a) {...}
```

这是因为引用像 `const` 数据一样，只能在创建时进行初始化。对于如 `front` 和 `items` 这样的简单数据成员，使用成员初始化列表还是在函数体中使用赋值并没有太大区别。正如你在第 14 章看到的，对于那些本身是类对象的成员，使用成员初始化列表更高效。

# 成员初始化列表语法

如果 `Class` 是一个类，且 `mem1`、`mem2` 和 `mem3` 是类数据成员，类构造函数使用以下语法初始化数据成员：

```cpp
Classy::Classy(int n, int m) :mem1(n), mem2(0), mem3(n*m + 2)
{
  //...
}
```

这会将 `mem1` 初始化为 `n`，`mem2` 初始化为 0，`mem3` 初始化为 `n*m + 2`。从概念上讲，这些初始化发生在对象创建时、括号内代码执行之前。注意以下几点：

- 这种形式只能用于构造函数。
- 你必须使用这种形式初始化 `const` 数据成员。
- 你必须使用这种形式初始化引用数据成员。

数据成员的初始化顺序取决于它们在类声明中出现的顺序。

# 注意

C++11 允许你做这种直觉上明显的事：

```cpp
class Classy
{
  int mem1 = 10; // 类内初始化
  const int mem2 = 20; // 类内初始化
```

这等同于在构造函数中使用初始化列表：

```cpp
Classy::Classy() : mem1(10), mem2(20) {...}
```

成员 `mem1` 和 `mem2` 被初始化为 10 和 20，除非调用初始化列表的构造函数。此时实际列表会覆盖这些默认初始化：

```cpp
Classy::Classy(int n) : mem1(n) {...}
```

在这种情况下，构造函数将使用值 `n` 来初始化 `mem1`，而 `mem2` 仍设置为 20。

返回 `items` 的值回答队列中有多少项目。你将在 12.11 节看到代码。

向队列尾添加项目（入队）更为复杂。这里是一种方法：

```cpp
bool Queue::enqueue(const Item &item)
{
    if (isfull())
        return false;
    Node *add = new Node;      // 创建节点
    // 如果失败，new 会抛出 std::bad_alloc 异常
    add->item = item;          // 设置节点
    add->next = NULL;          // nullptr
    items++;
    if (front == NULL)         // 如果队列为空
        front = add;           // 放在头部
    else
        rear->next = add;      // 否则放在队尾
        rear = add;            // 让 rear 指向新节点
    return true;
}
```

简而言，该方法经历以下阶段（见图 12.10）：

- 1. 终止队列已满。（对于此实现，最大尺寸由用户通过构造函数选择。）
- 2. 创建新节点。如果无法创建，`new` 会抛出异常，该主题将在第15章“朋友、异常及更多”中讨论。实际结果是，除非提供了额外的编程来处理异常，否则程序将终止。

# 第 12 章 类与动态内存分配

- 3. 在节点中存适当的值。在这种情况下，代码将值复制到节点的数据部分，并将节点的 `next` 指针设置为 NULL（或在 C++11 中设置为 0、`nullptr`）。这为该节点成为队列中的最后一个元素做了准备。

- 4. 将项目计数（`items`）加1。

- 5. 将节点附加到队列的尾部。这个过程包含两个部分。第一部分是将节点与列表中的其他节点连接。这是通过让当前尾节点的 `next` 指针指向新的尾部节点来实现。第二部分是设置队列成员指针指向新节点，这样队列就可以直接访问最后一个节点。如果队列为空，你还必须将 `front` 指针指向新节点。（如果队列中只有一个节点，则它既是头部节点也是尾部节点。）

![](img/cd111a87c1db9aff4db4b18834327463_700_0.png)

# 队列模拟 687

从队列头部移除元素（出队）也有几个步骤。这里是一种方法：

```cpp
bool Queue::dequeue(Item &item)
{
    if (front == NULL)
        return false;
    item = front->item; // 设置 item 为队列中的第一个元素
    items--;
    Node * temp = front; // 保存第一个元素的位置
    front = front->next; // 重置 front 指向下一个元素
    delete temp;
    if (items == 0)
        rear = NULL; // 删除之前的第一个元素
    return true;
}
```
