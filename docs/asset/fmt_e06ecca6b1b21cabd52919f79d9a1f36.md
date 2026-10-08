
`template <class Type>`

`bool linkedListIterator<Type>::operator!`

    `(const linkedListIterator<Type>& right) const`

{

    return (current != right.current);

}

```
现在我们已经定义了实现链表节点的类，以及一个用于描述 `linkedListType` 类的迭代器，以实现链表的基本属性。

以下抽象类作为抽象数据类型（ADT）定义了链表的基本属性：

```cpp

template <class Type>

class linkedListType{

public:

    const linkedListType<Type>& operator=(const linkedListType<Type>&);

    // 重载赋值运算符。

    void initializeList();

    // 将列表初始化为空状态。

    // 后置条件：first = nullptr, last = nullptr,

    // count = 0;

    bool isEmpty() const;

    // 用于判断列表是否为空的函数。

    // 后置条件：如果列表为空则返回 true，

    // 否则返回 false。

    void print() const;

    // 输出每个节点中包含的数据函数。

    // 后置条件：无

    int length() const;

    // 返回列表中节点数量的函数。

    // 后置条件：返回 count 的值。

    void destroyList();

    // 从列表中删除所有节点的函数。

    // 后置条件：first = nullptr, last = nullptr,

    // count = 0;

    Type front() const;

    // 返回列表的第一个元素的函数。

    // 前置条件：列表必须存在且不能为空。

    // 后置条件：如果列表为空，程序将终止；否则 

    // 返回列表的第一个元素。

    Type back() const;

    // 返回列表的最后一个元素的函数。

    // 前置条件：列表必须存在且不能为空。

    // 后置条件：如果列表为空，程序

    // 将终止；否则返回列表的最后一个

    // 元素。

    virtual bool search(const Type& searchItem) const = 0;

    // 用于判断 searchItem 是否在列表中的函数。

    // 后置条件：如果 searchItem 在列表中

    // 则返回 true，否则返回值 false。

    virtual void insertFirst(const Type& newItem) const = 0;

    // 在列表开头插入 newItem 的函数。

    // 后置条件：first 指向新列表，newItem

    // 被插入到列表开头，

    // last 指向列表中的最后一个节点，

    // 且 count 加 1。

    virtual void insertLast(const Type& newItem) = 0;

    // 在列表末尾插入 newItem 的函数。

    // 后置条件：first 指向新列表，newItem

    // 被插入到列表末尾，

    // last 指向列表中的最后一个节点，

    // 且 count 增加 1。

    virtual void deleteNode(const Type& deleteItem) = 0;

    // 从列表中删除 deleteItem 的函数。

    // 后置条件：如果找到，则从列表中删除

    // 包含 deleteItem 的节点。

    // first 指向第一个节点，last 

    // 指向更新后列表的节点，且 count 减 1。

    linkedIterator<Type> begin();

    // 返回链表开头迭代器的函数。

    // 后置条件：返回一个迭代器，其 current 

    // 设置为 first。

    linkedIterator<Type> end();

    // 返回指向链表最后一个元素之后的

    // 迭代器的函数。

    // 后置条件：返回一个迭代器，其 current 

    // 设置为 nullptr。

    linkedList();

    // 默认将列表初始化为空状态。

    // 后置条件：first = nullptr, last = nullptr,

    // count = 0。

    linkedType(const linkedListType<Type>& otherList);

    // 拷贝构造函数

    ~linkedTypeDestructor();

    // 删除列表中所有的节点。

    // 后置条件：列表对象被销毁。

protected:

    int count; // 用于存储列表中

    // 元素数量变量

    nodeType<Type>*first; // 指向列表第一个节点的指针

    nodeType<Type>*last; // 指向列表最后一个节点的指针

private:

    void copyList(const linkedListType<Type>& otherList);

    // 制作 otherList 拷贝的函数。

    // 后置条件：创建 otherList 的拷贝并

    // 赋值给此列表。

};

```

## 作为 ADT 的链表

图 17-20 显示了 `linkedType` 类的 UML 图。

| linkedType<Type> | |
| :--- | :--- |
| #count | int |
| #first | nodeType<Type> |
| #last | nodeType<Type> |
| +operator=(const linkedType<Type>&): void |
| +initialize(const linkedType<Type>&): void |
| +isEmpty() const | bool |
| +print() const | int |
| +length() const | int |
| +destroyList(): void |
| +front() const | Type |
| +back() const | Type |
| +search(const Type&) const = 0 | bool |
| +insertFirst(const Type&) = 0 | void |
| +insertLast(const Type&) = 0 | void |
| +deleteNode(const Type&) = 0 | void |
| +begin() | linkedIterator<Type> |
| +end() | linkedIterator<Type> |
| +linkedList() | |
| +linkedType(const linkedListType<Type>&) | |
| ~linkedTypeDestructor() | |
| -copyList(const linkedListType<Type>&) | void |
| #count | int |
| #first | nodeType<Type>* |
| #last | nodeType<Type>* |

*(注：由于输入文本后续出现大量重复乱码，此处仅展示有效的表格结构翻译)*

# 列表的长度

链表的长度（即列表中包含多少个节点）存储存储在变量 `count` 中。因此，此函数返回该变量的值：

```cpp

template <class Type>

int linkedList<Type>::length() const {

    return count;

} // end length

```

# 获取第一个节点的数据

`front` 函数返回第一个节点中包含的信息，其定义非常直观：

```cpp
template <class Type>
Type linkedList<Type>::front() const {
    assert(first != nullptr);
    return first->info; // 返回第一个节点的信息
} //end front
```

注意，如果列表为空，`assert` 语句将终止程序。因此，在调用此函数之前，请检查列表是否为空。

# 获取最后一个节点的数据

`back` 函数返回最后一个节点中包含的信息，其定义非常直观：

```cpp
template <class Type>
Type linkedList<Type>::back() const {
    assert(last != nullptr);
    return last->info; // 返回最后一个节点的信息
} //end back
```

注意，如果列表为空，`assert` 语句将终止程序。因此，在调用此函数之前，请检查列表是否为空。

# 开始与结束

`begin` 函数返回指向链表第一个节点的迭代器，而 `end` 函数返回指向链表最后一个节点之后的迭代器。它们的定义如下：

```cpp
template <class Type>
linkedListIterator<Type> linkedList<Type>::begin() {
    linkedListIterator<Type> temp(first);
    return temp;
}

template <class Type>
linkedListIterator<Type> linkedListType<Type>::end()
{
    linkedListIterator<Type> temp(nullptr);
    return temp;
}
```

# 复制列表

`copyList` 函数创建一个链表的完全相同的副本。因此，我们从第一个节点开始遍历要复制的列表。对于原始列表中的每个节点，我们执行以下操作：

- a. 创建一个节点，并将其命名为 `newNode`。

- b. 将该节点（原始列表中的）的信息复制到 `newNode` 中。

- c. 将 `newNode` 插入。

```cpp
template <class Type>
void linkedList<Type>::copyList(const linkedList<Type>& otherList) {
    nodeType<Type>* current; // 用于遍历原始列表
    nodeType<Type>* newNode; // 用于创建新节点

    for (current = otherList.first; current != nullptr; current = current->link) {
        newNode = new nodeType<Type>; // 创建节点
        newNode->info = current->info; // 复制信息
        newNode->link = nullptr;

        // 插入到列表末尾
        if (first == nullptr) {
            first = last = newNode;
        } else {
            last->link = newNode;
            last = newNode;
        }
        count++;
    }
}
```

# 第 17 章：链表

```cpp
newNode->link = first; // 在 first 之前插入 newNode
first = newNode; // 让 first 指向
                   //真正的第一个节点

count++;

if (last == nullptr) // 如果列表为空，newNode 也是
    last = newNode; // 列表中的最后一个节点
```

```cpp
//结束 insertFirst 结束
```

# 插入最后一个节点

成员函数 `insertLast` 的定义与成员函数 `insertFirst` 的定义相似。在这里，我们将新节点插入到 `last` 之后。从本质上，，insertLast` 函数的实现如下：

```cpp
template <class Type>
void unorderedlist<Type>::insertLast(const Type& newItem)
{
    node<Type> *newNode; // 用于创建新节点的指针
    newNode = new node<Type>; // 创建新节点
        newNode->info = newItem; // 将新项存储在节点中
    newNode->link = nullptr; // 将 newNode 的 link 字段
                             //设置为 nullptr

    if (first == nullptr) // 如果列表为空，newNode
                           //既是第一个节点也是最后一个节点
    {
        first = newNode;
        last = newNode;
        count++; // 计数加1
    }
    else // 列表不为空，在 last 之后插入 newNode
    {
        last->link = newNode; // 在 last 之后插入 newNode
        last = newNode; // 让 last 指向列表中
                        //真正的最后一个节点
        count++; // 计数加1
    }
}
```

```cpp
//结束 insertItem 结束
```

# 删除节点

接下来，我们讨论成员函数 `deleteNode` 的实现，该函数从列表中删除具有给定 `info` 的节点。我们需要考虑几种情况：

- **情况 1**：列表为空。

- **情况 2**：第一个节点就是具有给定 info 的节点。在这种情况下，我们需要调整指针 **first**。

- **情况 3**：具有给定 info 的节点位于列表某处。如果要删除的节点是最后一个节点，则我们必须调整指针 `last`。

- **情况 4**：列表不包含给定的 info。

如果列表为空，我们只需打印一条指示列表为空的消息。如果列表不为空，我们在列表中搜索给定的 info，如果找到了该节点，则删除该节点。在伪代码中，算法如下：

```
如果 列表为空
    输出 (无法从空列表中删除);
else
    如果第一个节点是具有给定 info 的节点
        调整指针，即 first，并释放内存；
    else
        在列表中搜索给定的 info
        如果找到了该节点，将其删除，并根据需要调整 last（如有需要）和 count 的值。
```

情况 1：列表为空。如果列表为空，输出一条错误信息。情况 2：列表不为空。要删除的节点是第一个节点。这种情况有两种场景：列表仅有一个节点，以及列表有多个节点。考虑包含一个节点的列表，如图 17-22 所示（img/d99829a174f7bf8a26bfada3d45e_1194.png）。假设我们想要删除 37。删除后，列表变为空。因此，在删除后，`first` 和 `last` 都被设置为 `nullptr`，且 `count` 被置为 0。现在考虑具有多个节点的列表，如图 17-23 所示（img/d9982a174f7bf8a26bfada3d45e_1195.png）。

假设要删除的节点是 28。删除该节点后，第二个节点变为第一个节点。因此，在删除该节点后，指针 `first` 的值发生了变化；也就是说，删除后，`first` 包含 info 为 17 的节点的地址，且 `count` 减了 1。图 17-24 显示了删除 info 为 28 的节点后的列表（img/d9982a174f7bf8a26bfada3d45e_1195_1.png）。

情况 3：要删除的节点不是第一个节点，而是列表中的某处。这种情况有两个子情况：(a) 要删除的节点不是最后一个节点，以及 (b) 要删除的节点是最后一个节点。让我们来说这两种情况。

情况 3a：要删除的节点不是最后一个节点。考虑图 17-25 所示的列表（img/d9982a174f7bf8a26bfada3d45e_1195_2.png）。图 17-25 是删除 37 之前的列表。假设要删除的节点是 37。删除该节点后，得到的列表如图 17-26 所示。注意，删除 37 不需要调整 `first` 和 `last` 的值。删除 37 后，`first` 包含了 info 为 17 的节点的地址，且 `count` 减了 1。图 17-26 是删除后的列表。
