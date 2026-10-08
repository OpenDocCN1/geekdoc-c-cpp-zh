
注意，在现实中，`insertFirst` 和 `insertLast` 函数不适用于有序链表，因为新项必须插入到列表适当的位置。然而，你必须提供它们的定义，因为这些函数在父类中被声明为抽象函数。

# 删除节点

要从有序链表中删除一个项，我们首先搜索列表查看该项是否存在于列表中。实现此操作的函数与普通链表的删除操作相同。在这里，由于列表是有序的，我们可以某种程度上改进有序链表的算法。

与 `insertNode` 情况一样，我们使用两个指针 `current` 和 `trailCurrent` 遍历列表。与 `insertNode` 操作类似，会出现以下几种情况：

- 情况 1：列表初始为空。我们遇到了错误。我们不能删除空列表。
- 情况 2：要删除的项位于列表的第一个节点。我们必须调整列表的头指针——即 `first`。
- 情况 3：要删除的项位于列表某处。在这里，`current` 指向包含删除项的节点，`trailCurrent` 指向 `current` 所向节点之前的节点。
- 情况 4：列表不为空，但要删除的项不在列表中。

删除节点后，`count` 减 1。`deleteNode` 函数的定义如下：

```cpp
template <class Type>
void orderedLinkedList<Type>::deleteNode(const Type& deleteItem)
{
    node<Type>*current; //用于遍历列表的指针
    node<Type>*trailCurrent = nullptr; //指向之前的指针
    bool found;
```

```cpp
if (first == nullptr) //情况 1
cout << "Cannot delete from an empty list." << endl;
else{
    current = first;
    found = false;
    while (current != nullptr && !found)//搜索列表
        if (current->info >= deleteItem)
            found = true;
        else
            {
                trailCurrent = current;
                current = current->link;
            }
    }
    if (current == nullptr) //情况 4
        cout << "The item to be deleted is not in the "
        << "list." << endl;
    else
        if (current->info == deleteItem) //要删除的项在列表中
        {
            if (first == current) //情况 2
            {
                first = first->link;
                if (first == nullptr)
                    last = nullptr;
                delete current;
            }
            else
            {
                trailCurrent->link = current->link;
                if (current == last)
                    last = trailCurrent;
                delete current;
                count--;
            }
        else //情况 4
            cout << "The item to be deleted is not in the "
            << "list." << endl;
    }
}//deleteNode 结束
```

# 有序链表的头文件

为了保持完整性，我们将展示如何创建定义 `orderedListType` 类的头文件，以及对此类列表的操作。（我们假设 `linkedType` 类的定义以及在头文件 `linkedlist.h` 中实现操作的函数定义）

```cpp
#ifndef H_orderedListType
#define H_orderedListType
```

```cpp
#include "linkedList.h"
```

```cpp
using namespace std;
template <class Type>
class orderedLinkedList: public linkedType<Type>
{
public:
    bool search(const Type& searchItem) const;
    // 判断 searchItem 是否在列表中函数。
    // 后置条件：如果 searchItem 在列表中，则返回 true，
    // 否则返回 false。
```

```cpp
void insert(const Type& newItem);
    // 将 newItem 插入列表的函数。
    // 后置条件：first 指向新列表，newItem
    // 被插入到列表适当的位置，
    // count 增加 1。
```

```cpp
void insertFirst(const Type& newItem);
    // 在列表中插入 newItem 的函数。
    // 由于生成的列表是有序的，newItem
    // 被插入到列表适当的位置。
    // 此函数使用 insert 函数插入 newItem；
    // 后置条件：first 指向新列表，newItem
    // 被插入到列表适当的位置，
    // count 增加 1。
```

```cpp
void insertLast(const Type& newItem);
    // 在列表中插入 newItem 的函数。
    // 由于生成的列表是有序的，newItem
    // 被插入到列表适当的位置。
    // 此函数使用相关函数插入 newItem；
    // 后置条件：first 指向新列表，newItem
    // 被插入到列表适当的位置，
    // count 增加 1。
```

```cpp
void deleteNode(const Type deleteItem);
    // 从列表中删除 deleteItem 的函数。
    // 后置条件：如果找到，包含 deleteItem
    // 的节点将从列表中删除；
    // first 指向新列表的第一个节点，
    // count 减少 1。
    // 如果 deleteItem 不在列表中，则打印
    // 适当的消息。
```

```cpp
};
```

1160 | 第 17 章：链表

```cpp
//在此处放置函数 search, insert,
// insertFirst, insertLast 和 deleteNode 的定义。
```

```cpp
#endif
```

以下程序测试了有序链表的各种操作：

```cpp
// 测试有序链表上各种操作的程序
```

```cpp
#include <iostream>
#include "orderedLinkedList.h"
using namespace std;
int main() {
    orderedLinkedList<int> list1, list2;
    int num;
    cout << "第 8 行: 输入以 -999 结尾的数字。" << endl;
    cin >> num;
    while (num != -999) {
        list1.insert(num);
        cin >> num;
    }
    cout << "第 16 行: list1: ";
    list1.print();
    cout << endl;
    list2 = list1;// 测试赋值运算符
    cout << "第 20 行: list2: ";
    list2.print();
    cout << endl;
    cout << "第 23 行: 输入要删除的数字;";
    cin >> num;
    cout << endl;
    list2.deleteNode(num);
    cout << "第 27 行: 删除 " << num << " 后，list2: " << endl;
    list2.print();
    cout << endl;
    return 0;
}
```

Copyright 2018 Cengage Learning. 保留所有权利。未经许可复制、扫描或复制。WCN 020-200-233

# 示例运行：在此运行中，用户输入用阴影表示。

```
第 8 行: 输入以 -999 结尾的数字。
23 65 34 72 12 82 36 55 29 -999
```

```
第 16 行: list1: 12 23 29 34 36 55 65 72 82
第 20 行: list2: 12 23 29 34 36 55 65 72 82
第 23 行: 输入要删除的数字: 23
```

第 27 行: 删除 23 后，list2:
12 29 34 36 55 65 72 82

前面的输出是不言自明的。详细部分留给你们进行练习。

> 注意：请注意，函数 `insert` 并没有检查要插入的项是否已经在列表中，它没有检查重复项。本章末尾的编程练习 8 要求你在插入项目之前修改函数 `insert` 的定义；即检查该项目是否已在列表中。如果要插入的项已经在列表中，该函数将输出适当的错误信息。换句话说，不允许重复项。

# 逆序打印链表（重温递归）

有序链表的节点（如之前构建的）是按升序排列的。应用程序可能需要按降序打印数据，这意味着我们必须反向打印链表。我们现在讨论 `reversePrint` 函数。给定一个链表指针，该函数将逆序打印链表的元素。

考虑图 17-37 所示的链表。

![](img/d998292a174f7bfd8a26bfbada3d454e_1210_0.png)

图 17-37 链表

对于图 17-37 中的链表，输出应采用如下形式：
20 15 10 5

由于链表是单向的，我们无法从最后一个节点开始反向遍历链表。我们现在来看如何有效地使用递归来逆序打印链表。

1162 | 第 17 章：链表

让我们用递归思考。在打印链表的剩余部分（即第一个节点的尾）之前，无法打印第一个节点的节点。同样，在打印第二个节点的尾之前，无法打印第二个节点的节点。每当我们考虑一个节点的尾，链表的大小就会减 1。最终，链表的大小将减到 0，递归停止。让我们先用伪代码编写算法（假设 `current` 是指向链表的指针）。

```cpp
if (current != nullptr)
{
    reversePrint(current->link); // 打印尾节点
    cout << current->info << endl; // 打印节点
}
```

在此，请注意边界情况；它是隐藏的。只有当链表指针不为 `nullptr` 时才会打印列表。此外，在 `if` 语句体内，递归调用是在链表的尾进行的。由于链表最终为空，下一次调用的 `if` 语句将失败，递归停止。此外，注意这些语句（例如打印节点信息）出现在递归调用之后；当返回调用函数时，我们必须执行剩余的语句。记住，函数只有在执行最后语句后才会退出。（我们所说的“最后语句”不是物理链表语句。）

# 双向链表

双向链表是每个节点都有 `next` 和 `back` 指针的链表。![](img/d998292a174f7bfd8a26bfbada3d454e_1210_0.png)

图 17-37 双向

双向链表可以在任意方向遍历。也就是说，我们可以从第一个节点开始遍历链表，或者如果给定最后一个节点的指针，我们可以反向遍历链表。接下来，双向链表的典型操作有：

1. 初始化链表。
2. 销毁链表。
3. 判断链表是否为空。
4. 在链表中查找给定项。
5. 获取头元素。
6. 获取尾元素。
7. 在链表中插入项。
8. 从链表中删除项。
9. 查找链表长度。
10. 打印链表。

接下来，我们将双向链表定义为抽象数据类型（ADT）：

```cpp
// 节点定义
template <class Type>
struct nodeType {
    Type info;
    nodeType<Type> *next;
    nodeType<Type> *back;
};
```

```cpp
template <class Type>
class doublyLinkedList
{
public:
    const doublyLinkedList<Type>& operator=
    (const doublyLinkedList<Type>&);
    // 重载赋值运算符
```

```cpp
void initializeList();
// 将链表初始化为空状态的函数
// 后置条件：first = nullptr; last = nullptr;
// count = 0;
```

```cpp
bool isEmptyList() const;
// 判断链表是否为空的函数
// 后置条件：如果链表为空则返回 true，
// 否则返回 false
```

```cpp
void destroy();
// 从链表中删除所有节点的函数
// 后置条件：first = nullptr; last = nullptr;
// count = 0;
```

```cpp
void print() const;
// 输出链表中每个节点的函数
```

```cpp
void reversePrint() const;
// 逆序输出链表中每个节点的函数
```

```cpp
int length() const;
// 返回链表节点数量的函数
```

```cpp
Type front() const;
// 返回链表第一个元素的函数
```

```cpp
Type back() const;
// 返回链表最后一个元素的函数
```

```cpp
bool search(const Type& searchItem) const;
// 判断 searchItem 是否在链中的函数
```

# 1166 | 第17 章：双向链表

```cpp
void insert(const Type& insertItem);
// 将 insertItem 插入列表的函数。
// 前置条件：如果列表不为空，它必须是
//有序的。
// 后置条件：insertItem 被插入到列表适当的位置，
// first 指向第一个节点，last 指向
// 新列表的 最后一个节点，且 count 增加 1。
```

```cpp
void deleteNode(const Type deleteItem);
// 从列表中删除 deleteItem 的函数。
// 后置条件：如果找到，则包含 deleteItem 的节点
// 将从列表中删除；first 指向
// 新列表的第一个节点，last 指向
// 新列表的最后一个节点，
// 且 count 减 1；否则，
// 打印一条适当的消息。
```

```cpp
doublyLinkedList();
//默认构造函数
// 将列表初始化为空状态。
// 后置条件：first = nullptr; last = nullptr;
//count = 0;
```

```cpp
doublyLinkedList(const doublyLinkedList<Type>& other);
//拷贝构造函数
~doublyLinkedList();
//析构函数
// 后置条件：列表对象被销毁。
```

```cpp
protected:
    int count;
    nodeType<Type>*first; //指向第一个节点的指针
    nodeType<Type>*last; //指向最后一个节点的指针
```

```cpp
private:
    void copy(const doublyLinkedList<Type>& otherList);
// 创建 otherList 拷贝的函数。
// 后置条件：创建了 otherlist 的副本并将其
// 赋值给此列表。
```
