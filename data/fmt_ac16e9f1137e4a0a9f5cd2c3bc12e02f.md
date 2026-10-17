
`struct ListNode`

{

    `string` `item`;

```

# 13.1 节点与链表

# 显示 13.1 节点与指针

![](img/ca450b03f7ea64419b139be8fdd92a4a_777_0.png)

```cpp
int count;
ListNode *link;
typedef ListNode ListNodePtr;
```

类型定义的顺序非常重要。`ListNode` 的定义必须首先，因为在 `ListNodePtr` 的定义中使用了它。

显示 13.1 中标记为 `head` 的框不是节点，而是一个可以指向节点的指针变量。该指针变量声明如下：

```cpp
ListNode head;
```

尽管我们已经调整了类型定义以避免某些非法的循环，但 `struct` 类型 `ListNode` 的定义仍然是循环的。该定义使用 `ListNode` 名称来定义成员变量。这种特定的循环没有问题，并且在 C++ 中是允许的。一个表明该定义在逻辑上与你可以绘制像显示 13.1 这样表示此类结构的图并不矛盾的迹是。

现在我们在结构内部有了指针，这些指针指向包含指针的结构，以此此类推。在这种情况下，语法有时会变得复杂，但在所有情况下，语法都遵循我们描述的关于指针和结构的几条规则。作为说明，假设声明如上所示，情况如图显示 13.1 所示，并且

`NULL` 通常用于两个不同的（通常是同时的）目的。它被用于给一个原本没有值的指针变量赋值。这防止了无意的引用。

# 13.1 节点与链表

# 显示 13.2 访问节点数据

```cpp
head->count = 12;
head->item = "bagels";
```

之前

之后

![](img/ca450b03f7ea64419b139be8fdd92a4a_779_0.png)

![](img/ca450b03f7ea64419b139be8fdd92a4a_779_1.png)

标记。程序可以像显示 13.2 所示遍历节点列表，当程序到达包含 `NULL` 的节点时，它知道已经到达列表的末尾。

`NULL` 实际上是数字 0，但我们倾向于这样思考并写成 `NULL`。这让你明确指的是可以赋值给指针变量的特殊值，因为 `NULL` 不是任何内存地址。第二种用途是结束

`NULL` 是一个常量，表示可以赋值给指针变量的特殊值。常量 `NULL` 实际上是数字 0，但我们倾向于这样思考并写成 `NULL`。

# 箭头运算符 ->

箭头运算符指定由指针变量指向的结构体成员（或类对象的成员）。其语法如下：

```
Pointer_Variable->Member_Name
```

上述内容指的是 `Pointer_Variable` 所指向的结构体或对象的成员。它指的是哪个成员由 `Member_Name` 决定。

例如，假设你有如下定义：

```cpp
struct Record
{
  int number;
  char grade;
};
```

以下代码创建了一个 `Record` 类型的动态变量，并将动态结构变量的成员变量设置为 2001 和 'A'：

```cpp
Record *p;
p = new Record;
p->number = 2001;
p->grade = 'A';
```

可以使用赋值运算符将指针设置为 `NULL`，如下所示，声明了一个名为 `there` 的指针变量并将其初始化为 `NULL`：

```cpp
double *there = NULL;
```

常量 `NULL` 可以赋值给任何指针类型的变量。

# NULL

`NULL` 是一个特殊的常量值，用于给一个原本没有值的指针变量赋值。`NULL` 可以赋值给任何类型的指针变量。标识符 `NULL` 定义在库中，包括包含 `<cdef>` 头文件的库和包含 `<iostream>` 头文件的库。

# 13.1 节点与链表

`nullptr`

常量 `NULL` 实际上是数字 0，这导致了歧义问题。考虑下面的重载函数：

```cpp
void func(int *p);
void func(int i);
```

如果我们调用 `func(NULL)`，将调用哪一个函数？由于 `NULL` 是数字 0，因此两者都是同样有效的。C++11 通过引入一个新常量 `nullptr` 解决了这个问题。`nullptr` 不是整数 0，但它是一个用于表示空指针的字面量。在任何原本使用 `NULL` 表示指针的地方，都请使用 `nullptr`。例如，我们可以写：

```cpp
double *there = nullptr;
```

> `nullptr` 是一个特殊的常量值，其用法与 `NULL` 相同，但它只能被赋值给指针。它不是数字 0。使用 `nullptr` 来区分空指针和数字 0。`nullptr` 是 C++11 中引入的。

# 自测练习题

- 1. 假设你的程序包含以下类型定义：

```cpp
struct Box {
    string name;
    int number;
    Box *next;
};
typedef Box *BoxPtr;
```

以下代码的输出是什么？

```cpp
BoxPtr head;
head = new Box;
head->name = "Sally";
head->number = 18;
cout << head->name << endl;
cout << head->number << endl;
cout << head->number << endl;
```

- 2. 假设你的程序包含了自测练习 1 中给出的类型定义和代码。该代码创建了一个包含字符串 "Sally" 和数字 18 的节点。你会添加什么代码来将该节点的成员变量的值设置为 `NULL`？

- 3. 假设你的程序包含了自测练习 1 中给出的类型定义和代码。假设指针变量的值没有改变，你如何销毁 `head` 指向的动态变量，并将其使用的内存返回给系统，以便可以重用以创建新的动态变量？

- 4. 给定以下结构定义：

```cpp
struct ListNode {
    string item;
    int count;
    ListNode *link;
}
ListNode *head = new ListNode;
```

编写代码将字符串 "Wilbur's brother Orville" 赋值给 `head` 指向的节点的 `item` 成员。

# 链表

如显示 13.2 所示的列表被称为链表。链表是一个节点列表，其中每个节点都有一个成员变量，该变量是一个指向链表中下一个节点的指针。链表中的第一个节点称为头节点（`head`），指向第一个节点的指针变量名为 `head`。请注意，名为 `head` 的指针并不是链表的头节点，而只是指向链表的头节点。最后一个节点没有特殊名称，但它有一个特殊的属性。最后一个节点的成员指针变量的值为 `NULL`。要检查一个节点是否是最后一个，只需要查看该指针变量是否等于 `NULL` 即可。

我们在本节的目标是编写一些操作链表的基本函数。为了多样化并简化表示法，我们将使用比显示 13.2 中使用的更简单的节点类型。这些节点将只包含一个整数和一个指针。我们将使用的节点和指针类型定义如下：

```cpp
struct Node {
    int data;
    Node *link;
}
typedef Node* NodePtr;
```

# 13.1 节点与链表

作为一个热身练习，让我们看看如何使用这种类型的节点构建链表的开头。我们首先声明一个名为 `head` 的指针变量，它将指向链表的头：

```cpp
NodePtr head;
```

为了创建我们的第一个节点，我们使用 `new` 运算符创建一个新的动态变量，该变量将成为我们链表的第一个节点：

```cpp
head = new Node;
```

然后我们给这个新节点的成员赋值：

```cpp
head->data = 3;
head->link = NULL;
```

注意，该节点的指针成员被设置为等于 `NULL`。这是因为该节点是链表的最后一个节点（同时也是链表的第一个节点）。在这个阶段，我们的链表看起来如下：

![](img/ca450b03f7ea64419b139be8fdd92a4a_783_0.png)

我们的单节点列表是完全随地构建的。要拥有一个更大的链表，你的程序必须能够以系统化的方式添加节点。我们描述了在链表中插入节点的一种简单方法。

# 在链表头部插入节点

在小节中，我们假设链表已经包含一个或多个节点，插入函数的第一个参数将是指向链表头的指针变量的引用传递（call-by-reference），即指向链表中节点的指针变量。另一个参数将提供要存储在新节点中的数字。我们的插入函数的函数声明如下：

```cpp
void headInsert(NodePtr& head, int theNumber);
```

# 作为参数的链表

你应该始终保留一个指向链表头的指针变量。这个指针变量是命名链表的一种。当你编写一个接受链表作为参数的函数时，这个指针（指向链表的头）可以作为链表参数使用。

为了在链表中插入新节点，我们将使用 `new` 运算符创建一个新节点。由于动态变量没有名称，我们必须使用指针变量来指向它。当我们调用 `head` 时，新节点可以被引用为 `tempPtr`。整个过程如下：

# headInsert 函数的伪代码

- 1. 创建指向 `head` 的动态变量（该变量是新节点，可以被引用为 `tempPtr`）。
- 2. 将数据放入该新节点。
- 3. 将该新节点的链成员指向链表的头（即第一个节点）。
- 4. 让指针变量 `head` 指向新节点。

整个过程在显示 13.3 中所示：

- 1. `tempPtr = new Node;`
- 2. `tempPtr->data = theNumber;`
- 3. `tempPtr->link = head;`
- 4. `head = tempPtr;`

# 显示 13.4 在链表头部插入节点

函数声明

```cpp
struct Node {
    int data;
    Node *link;
};
typedef Node* NodePtr;
void headInsert(NodePtr& head, int theNumber);
```

函数定义

```cpp
void headInsert(NodePtr& head, int theNumber)
{
    NodePtr tempPtr = new Node;
    tempPtr->data = theNumber;
    tempPtr->link = head;
    head = tempPtr;
}
```

# 显示 13.3 向链表添加节点（部分 1）

- 1. `tempPtr = new Node;`
- 2. `tempPtr->data = theNumber;`

# 显示 13.3 向链表添加节点（部分 2）

- 3. `tempPtr->link = head;`
- 4. `head = tempPtr;`

# 显示 13.5 新数据值为 12 的情况

# 陷阱 丢失节点

你可能忍不住在定义 `headInsert`（显示 13.4）时使用指针变量来创建新节点，而不是使用局部变量 `tempPtr`。如果你尝试，可能会这样开始函数：

```cpp
head = new Node;
head->data = theNumber;
```

此时，新节点已经构造，包含了正确的数据，并被指针 `head` 指向，这一切都是正确的。剩下的只需要通过设置下面的指针成员将链表的其余部分连接到它，使其指向原本链表的第一个节点：

![](img/ca450b03f7ea64419b139be8fdd92a4a_786_0.png)

# 第13 章 / 指针与链表

每当你定义一个操作列表的函数时，都应该检查它是否在空列表上有效。如果无效，你可能可以为空列表添加一个特殊情况。如果你无法设计该函数适用于空列表，那么你的程序必须以某种方式处理空列表或完全避免它们。幸运的是，空列表通常可以像其他列表一样被处理。例如，显示 13.4 中的 `headInsert` 函数是以非空列表为模型设计的，但检查会显示它也适用于空列表。

# 显示 13.5 丢失的节点

![](img/ca450b03f7ea64419b139be8fdd92a4a_787_0.png)

用户的程序可能会导致操作系统崩溃。为了避免此类节点丢失，程序必须始终保持某个指向链表表头的指针，通常将该指针保存在一个名为 `head` 的指针变量中。

# 链表的搜索

接下来，我们将设计一个函数来搜索链表，以定位特定的节点。我们将使用与之前子节中相同的节点类型，称为 `Node`。（节点和指针类型的定义已在显示 13.4 中给出。）我们设计的函数将有两个参数：链表本身和我们想要定位的整数。该函数将返回一个指向包含该整数的第一个节点的指针。如果没有节点包含该整数，该函数将返回 `NULL`。这样，我们的程序就可以通过检查函数是否返回 `NULL` 来测试链表中的某个指针值是否不等于 `NULL`。我们函数的函数声明和头部注释如下：

```
NodePtr search(NodePtr head, int target);
// 前置条件：指针 head 指向链表的表头。
// 最后一个节点中的指针变量
// 如果链表为空，则 head 为 NULL。
// 返回一个指向包含 target
// 的第一个节点的指针。如果没有节点包含 target，
// 函数返回 NULL。
```

我们将使用一个局部指针变量（在此称为 `here`）来遍历链表，或任何其他由节点和指针组成的数据结构，即跟随指针进行移动。因此，我们将从 `here` 指向第一个节点开始，并沿着每个节点引出的指针在节点与节点之间移动指针。这种技术在显示 13.6 中给出了示意。由于空链表存在一些会干扰讨论的小问题，我们首先假设链表至少包含一个节点。稍后我们将再回来，确保空链列表的算法也是正确的。这种搜索技术得出了算法：

# search 函数伪代码

使指针变量 `here` 指向链表的头节点（即第一个节点）。

```
while (here 并没有指向包含 target 的节点
and here 并没有指向最后一个节点)
{
  让 here 指向列表中的下一个节点。
  if (here 指向的节点包含 target)
    return here;
else
  return NULL;
```

为了将指针 `here` 移动到下一个节点

```
here->link
```

为了将 `here` 移动到下一个节点，我们希望改变 `here`，使其指向上述指针（成员）所指向的节点。因此，以下代码将指针 `here` 移动到列表中的下一个节点：

```
here = here->link;
```

将这些部分结合起来，得到了算法伪代码的如下改进版本。

# search 函数代码的初步版本

`here = head;`

```cpp
while (here->data != target && here->link != NULL)
  here = here->link;
if (here->data == target)
  return here;
else
  return NULL;
```

注意 `while` 语句中的布尔表达式。我们通过测试成员变量 `here->link` 是否不等于 `NULL`，来测试 `here` 是否没有指向最后一个节点。

# 13.1 节点与链表

# 显示 13.6 搜索链表

`target->s = 6`

![](img/ca450b03f7ea64419b139be8fdd92a4a_789_0.png)

![](img/ca450b03f7ea64419b139be8fdd92a4a_789_1.png)

我们仍然必须回头处理空列表的情况。如果我们检查我们的代码，发现链表为空，那么 `here` 没有指向任何节点，因此以下表达式是未定义的：

```
here->data
here->link
```

为了将 `here` 移动到下一个节点，我们希望改变 `here`，使其指向上述指针（成员）所指向的节点。因此，以下代码将指针 `here` 移动到列表中的下一个节点：

```
here = here->link;
```

将这些部分结合起来，得到了算法伪代码的如下改进版本。

# search 函数代码的初步版本

`here = head;`

```cpp
while (here->data != target && here->link != NULL)
  here = here->link;
if (here->data == target)
  return here;
else
  return NULL;
```

注意 `while` 语句中的布尔表达式。我们通过测试成员变量 `here->link` 是否不等于 `NULL`，来测试 `here` 是否没有指向最后一个节点。

# 13.1 节点与链表

# 指针作为迭代器

迭代器是一种允许你遍历列表的结构。事实上，指针是迭代器的典型示例。基本思想如下所示：

```cpp
NodePtr iter;
iter = head;
while (iter != NULL) {
    // 对 iter 进行某些操作
    iter = iter->link;
}
```

# 插入与删除节点

接下来我们设计一个在指定位置插入节点的函数。我们假设某个其他函数已经正确地放置了指针 `afterMe`。我们希望将新节点放在 `afterMe` 指向的节点之后，如显示 13.8 所示。类型定义见 13.7。

在列表中插入

```cpp
void insert(NodePtr afterMe, int theNumber);
// 前置条件：afterMe 指向列表中的一个节点。
```
