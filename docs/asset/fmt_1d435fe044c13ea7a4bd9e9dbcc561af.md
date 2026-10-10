
显示 17.5 展示了当新数据值为 12 时的情况，并说明了该问题。如果你继续这样做，将没有任何指针指向包含 15 的节点。由于没有命名的指针指向它（或指向延伸到该节点的指针链），指针就无法引用该节点。该节点以及其下方所有节点都丢失了。程序无法对这些节点中的任何一个创建指针，也无法访问这些节点中的数据或与之相关的任何内容。它没有方法引用这些节点。这种情况会在整个程序运行期间导致内存泄漏。严重的内存泄漏会导致程序内存耗尽并异常终止。更糟糕的是，在少数情况下，普通用户程序中的内存泄漏（丢失节点）可能会导致操作系统崩溃。为了避免此类泄漏，程序必须始终保留一个指向列表头的指针，通常是指针变量 `head` 中的指针。

## 内存泄漏

# 在列表中插入和删除节点

我们设计了一个函数，在链表的指定位置插入节点。如果你希望节点按照特定的顺序（如数字或字母顺序），则不能简单地将节点插入列表的开头或结尾。因此，我们将设计一个函数，在链表的指定节点之后插入节点。

我们假设其他函数或程序部分已正确地让名为 `after` 的指针指向链表中的某个节点。我们希望将新节点放在 `afterMe` 所指向的节点之后，如显示 17.6 所示。相同的技术适用于带有任何数据的节点，但为了具体起见，我们正在列表中间进行插入。

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_772_0.png)

# 第17章 链式数据结构

## 显示 17.5 丢失的节点

插入前的链表 执行 `head = new IntNode; head->setData(theData);` 后的情况

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_773_0.png)

与之前小节相同类型的节点。类型定义在显示 17.4 中。我们要定义的函数声明如下所示：

```
void insert(IntNodePtr afterMe, int theData);
// 前置条件：afterMe 指向链表中的一个节点。
// 后置条件：一个包含 theData 的新节点
// 已添加到 afterMe 所指向的节点之后。
```

新节点插入到列表内部的方式，基本上与我们已经讨论过的将节点添加到列表（开头）的方式是相似的。其区别在于，我们使用的是指针 `afterMe->link` 而不是 `head`。插入操作如下：

```
afterMe->setLink(new IntNode(theData, afterMe->getLink() ));
```

`theData` 等于 5 的细节在显示 17.6 中，最终的函数定义在显示 17.4 中。

如果你查看 `insert` 函数的代码，你会发现如果 `afterMe` 指向的节点是列表中的最后一个节点，那么它可以正常工作。然而，`insert` 无法用于在链表的开头插入节点。显示 17.4 中的 `headinsert` 函数可以用于在列表开头插入节点。

通过使用 `insert` 函数，你可以维护一个数字顺序、字母顺序或其他排序的链表。无论链表有多长，无论你想在列表的哪个位置添加新数据，只需通过调整两个指针即可将新节点“挤”到正确的位置。如果你需要使用数组——在极端情况下——数组必须按顺序进行复制。

## 节点与链表

### 17.6 在链表中间插入

`head`

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_774_0.png)

`afterMe` 由以下代码创建：

```
new IntNode(5, afterMe->getLink()));
```

执行 `afterMe->setLink(`

```
new IntNode(theData, afterMe->getLink()));
```

的最终结果，以便在正确的位置为新值留出空间。尽管定位指针存在开销，但在链表中插入通常比比在数组中插入更高效。

从链表中删除节点也非常简单。显示 17.7 展示了该方法。一旦定位了 `before` 和 `discard` 指针，删除该节点只需要下条语句：

```
before->setLink(discard->getLink()));
```

## 显示 17.7 删除节点

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_775_0.png)

这足以从链表中删除该节点了。然而，如果你不再将此节点用于其他地方，你应该销毁该节点并返回它使用的内存以便回收；你可以通过如下调用 `delete` 来实现：

```
delete discard;
```

如第10章所述，动态变量的内存存储在被称为“堆”（heap）的内存区域中。由于堆内存不是无限的，当程序不再需要某个动态变量（节点）时，你应该使用 `delete` 运算符返回该内存以进行回收。我们在随附的框中包含了对 `delete` 运算符的复。

### delete 运算符

`delete` 运算符消除动态变量并将动态变量占据的内存返回给堆。该内存可以被重复用于创建新的动态变量。例如，以下代码消除了指针 `p` 指向的动态变量：

```
delete p;
```

调用 `delete` 后，指针的值（如所示 `p`）是未定义的。

### 陷阱：在动态数据结构上使用赋值运算符

如果 `head1` 和 `head2` 是指针变量，且 `head1` 指向链表的头节点，以下操作将使 `head2` 指向同一个头节点，因此同一个链表：

```
head2 = head1;
```

然而，你必须记住只有一个链表，而不是两个。如果你更改了 `head1` 指向的链表，你也会改变 `head2` 指向的链表，因为它们是同一个链表。

如果 `head1` 指向一个链表，而你希望 `head2` 是该链表的第二个完全相同的副本，那么前面的赋值语句将不起作用。相反，你必须通过节点拷贝整个链表。

## 搜索链表

接下来我们设计一个函数来搜索链表以定位特定节点。我们将使用与之前小节中相同的名为 `IntNode` 的节点类型（节点和指针类型的定义在显示 17.4 中）。我们设计的函数有两个参数：链表和我们要查找的整数。该函数将返回一个指向包含该整数的第一个节点的指针。如果没有节点包含该整数，函数将返回 `NULL`。

这样，我们的程序就可以通过检查返回的指针值是否不等于 `NULL` 来测试列表中的整数。我们函数的声明和头文件如下：

```
IntNodePtr search(IntNodePtr, int target);
// 前置条件：指针指向链表的头。
// 最后一个节点的指针变量为 NULL。
// 如果列表为空，则 head 为 NULL。
// 返回指向包含//目标的第一个节点的指针。
// 如果没有节点包含目标，函数返回 NULL。
```

### search 函数的伪代码

```
让指针变量 here 指向链表的头节点（即第一个节点）。
while (here 未指向包含目标的节点
      且 here 未指向最后一个节点）
{
    让指向列表的下一个节点。
}
if (here 指向的节点包含目标)
    return here;
else
    return NULL;
```

为了将指针 `here` 移动到下一个节点，我们必须根据与指向当前节点的指针成员所指向的指针来思考。指向当前节点的指针成员由表达式给出：

```
here->getLink()
```

为了将 `here` 移动到下一个节点，我们希望更改 `here` 使其指向上述指针指向的节点。因此，以下操作将指针 `here` 移动到列表中的下一个节点：

```
here = here->getLink();
```

## 节点与链表

### 显示 17.8 查找链表

目标值为 6

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_778_0.png)

# 第 17 章 链式数据结构

将这些部分组合在一起，得到了搜索函数算法伪代码的如下改进版本：

```
here = head;
while (here->getData() != target && here->getLink() != NULL)
    here = here->getLink();

if (here->getData() == target)
    return here;
else
    return NULL;
```

注意 `while` 语句中的布尔表达式。我们通过测试成员变量 `here->getLink()` 是否为 `NULL` 来检查 `here` 是否正指向最后一个节点。

我们仍然必须回来处理空列表的情况。在之前的代码中，我们会发现空列表存在问题。如果列表为空，那么 `here` 就是 `NULL`，此时以下表达式将没有定义：

```
here->getData()
here->getLink()
```

当 `here` 为 `NULL` 时，它没有指向任何节点，因此没有数据成员或链接成员。因此，我们对空列表引入了特例处理。完整的函数定义在显示 17.9 中。

# 双向链表

普通链表允许你沿着一个方向在链表中移动（顺着链接）。双向链表有两个链接：一个是指向下一个节点的指针，另一个是指向前一个节点的额外链接。在某些情况下，指向前一个节点的链接可以简化我们的代码。例如，在从列表中删除一个节点时，我们不再需要记住连接到我们想要丢弃的那个节点。从图上看，双向链表看起来像显示 17.10 中的示例列表。

## 显示 17.9 在链表中定位节点的函数（第 1 部分，共 2 部分）

### 函数声明

```
IntNodePtr search(IntNodePtr head, int target);
// 前置条件：指针 head 指向链表的表头。
// 最后一个节点中的指针变量为 NULL。
// 如果列表为空，则 head 为 NULL。
// 返回指向包含 target 的第一个节点的指针。
// 如果没有节点包含 target，函数返回 NULL。
```

### 函数定义

```
// 使用 cstddef:
```

## 显示 17.9 在链表中定位节点的函数（第 2 部分，共 2 部分）

`IntNodePtr search(IntNodePtr head, int target)`

```
IntNodePtr here = head;
if (here == NULL) // 空列表
    return NULL;
else
    while (here->getData() != target && here->getLink() != NULL)
        here = here->getLink();
    if (here->getData() == target)
            return here;
    return NULL;
```

> `IntNode` 和 `IntNodePtr` 的定义在显示 17.4 中。

## 显示 17.10 双向链表

### 表头 (head)

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_780_0.png)

整数双向链表的节点类可以定义如下：

```
class DoublyLinkedIntNode {
public:
    DoublyLinkedIntNode(int data, DoublyLinkedIntNode* previous, DoublyLinkedIntNode* next)
        : data(data), nextLink(next), previousLink(previous) {}
    DoublyLinkedIntNode* getNext() const { return nextLink; }
    DoublyLinkedIntNode* getPrevious() const {
        return previousLink;
    }
    int getData() const { return data; }
    void setData(int data) { data = data; }
    void setNextLink(DoublyLinkedIntNode* pointer) {
        nextLink = pointer; }
```

# 第 17 章 链式数据结构

```
void setPreviousLink(DoublyLinkedListNode* pointer)
  { previousLink = pointer; }
```

```
private:
  int data;
  DoublyLinkedListNode *nextLink;
  DoublyLinkedListNode *previousLink;
  DoublyLinkedListNode* DoublyLinkedListPtr;
```

该代码与单链表版本完全相同，只是我们添加了一个私有变量 `previousLink`，用于存储指向列表中前一个节点的链接。添加了 `setPreviousLink` 和 `getPreviousLink` 函数来获取和设置链接，并在构造函数中增加了一个额外的参数以初始化 `previousLink`。以前称为 `link` 的成员已重命名为 `nextLink`，以区分指向前一个节点还是下一个节点。

## 在双向链表中添加节点

要在列表前端添加一个 `DoublyLinkedListNode`，我们必须设置两个节点的链接而不是一个。通用过程如显示 17.11 所示。插入函数的声明与单链表基本相同：

```
void insert(DoublyLinkedListPtr& head, int data);
```

我们创建一个新节点，指向 `head` 且其 `previousLink` 为 `NULL`，因为它将成为新的头：

```
DoublyLinkedListNode* newHead = new DoublyLinkedListNode(data, NULL, head);
```

`head` 指向新节点：

```
head->setPreviousLink(newHead);
```

完整的函数位于显示 17。

## 从双向链表中删除节点

从双向链表中删除一个节点时，需要更新要丢弃节点的两侧链接。得益于反向链接，我们不需要像单链表那样使用单独变量来跟踪前一个节点。删除节点的通用过程如显示 17.12 所示。某些特殊情况必须单独处理，例如从列表开头或末尾删除节点。

## 节点与链表

### 显示 17.11 在双向链表头部添加节点

删除节点前的列表

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_780_0.png)

创建一个新节点

```
newHead = new DoublyLinkedListNode(data, NULL, head);
```

`head` 指向新节点：

```
head->setPreviousLink(newHead);
```

最后，将 `head` 设置为新头：

```
head = newHead;
```

完整的函数位于显示 17.13。

## 从双向链表中删除节点

从双向链表中删除一个节点时，需要更新要丢弃节点的两侧链接。得益于反向链接，我们不需要像单链表那样使用单独变量来跟踪前一个节点。删除节点的通用过程如显示 17.12 所示。某些特殊情况必须单独处理，例如从列表开头或末尾删除节点。

# 第 17 章 链式数据结构

删除节点前的列表

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_780_0.png)

设置前一个和下一个节点

```
DoublyLinkedListNode prev = discard->getPreviousLink();
DoublyLinkedListNode next = discard->getNextLink();
```

跳过节点

```
prev->setNext(next);
if (next != NULL) {
    next->setPreviousLink(prev);
}
```

删除节点

```
delete discard;
```

# 第17章 链表数据结构

## 显示 17.13 从双向链表中添加和删除节点的函数（3部分中的2部分）

```
DoublyLinkedList* getPreviousLink() const
    { return previousLink; }
int getData() const
    { return data; }
void setData(int theData)
    { data = theData; }
void setNextLink(DoublyLinkedListNode* pointer)
    { nextLink = pointer; }
void setPreviousLink(DoublyLinkedListNode* pointer)
    { previousLink = pointer; }
```

private:

    int data;

    DoublyLinkedListNode *nextLink;

    DoublyLinkedListNode *previousLink;

}

```

```

typedef DoublyLinkedListNode* DoublyLinkedListNodePtr;

```

## 向链表头部插入节点的函数

### 函数声明

```

void headInsert(DoublyLinkedListNode& head, int theData)

//前置条件：指针变量 head 指向

//链表的头部。

//后置条件：一个包含 theData 的新节点

//已添加到链表的头部。

```

### 函数定义

```

void headInsert(DoublyLinkedListNode& head, int theData)

{

    DoublyLinkedListNode* newHead = new DoublyLinkedListNode

        (theData, NULL, head);

    head->setPreviousLink(newHead);
