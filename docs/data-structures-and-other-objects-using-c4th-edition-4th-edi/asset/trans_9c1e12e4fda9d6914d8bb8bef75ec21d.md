

- 9. 当前在内存中的操作系统部分可以被覆盖。

- 10. 该实现将正确编译。但是，由于返回值是指向列表中节点的指针，程序员可以使用返回值来更改链表。一般来说，常量成员函数的返回值绝不应允许更改底层链表。

- 11. 将返回类型更改为 const node*，并提供第二个非 const 函数，以普通 node* 形式返回链接。

- 12. 我们只需要一个函数来访问数据字段，因为该函数返回数据的副本（仅凭节点的数据副本无法更改底层链表）。

- 13. 必须将 #include <string> 指令添加到工具包头文件中的其他包含指令中。然后我们可以将 typedef 语句更改为：typedef string value_type;

- 14. for (cursor = head_ptr; cursor != NULL; cursor = cursor->link()) {...}

- 15. 当函数访问并可能修改链表，但不需要修改指针以指向新节点时，节点指针应为值参数。

- 16. locate_ptr = locate_ptr->link(); 如果在此赋值语句之前 locate_ptr 已经指向最后一个节点，则该赋值将把 locate_ptr 设置为空指针。

- 17. 使用第 5.2 节中的函数：
```cpp
if (head_ptr == NULL)
    list_head_insert(head_ptr, 42);
else
    list_insert(head_ptr, 42);
```

- 18. if (head_ptr->link() == NULL)
    tail_ptr = head_ptr;

- 19. new 运算符用于函数 list_insert、list_copy、list_piece（如果你从练习 24 实现它）和 list_head_insert。delete 运算符用于函数 list_head_remove、list_remove 和 list_clear。

- 20. 除非你实际上正在减少节点数量，否则绝不要调用 delete。

- 21. 使用第 5.2 节中的函数：
```cpp
if (head_ptr == NULL)
{
    if (head_ptr->link() == NULL)
        list_head_remove(head_ptr);
    else
        list_remove(head_ptr);
}
```

- 22. 它将是空指针。

- 23. 这一行将是：
```cpp
previous_ptr->set_link(new node(entry, previous_ptr->link()));
```

- 24. 该实现与 list_copy 几乎相同，但复制必须在复制完尾节点时停止。

- 25. 这是 const 版本：
```cpp
const node*
const node* head_ptr,
size_t position
)
// size_t locations used: cassert, cstdlib
{
const node *cursor;
size_t i;
assert(0 <= position);
cursor = head_ptr;
for (
i = 1;
(i < position)
&&
(cursor != NULL);
++i
)
cursor = cursor->link();
return cursor;
}
```

- 26. 该定义使 bag::value_type 与 node::value_type 相同，因此程序员可以使用 bag::value_type 而无需了解链表实现的细节。

- 27. node 类中的 value_type 需要更改为 string（如自测练习 13 的答案所示）。

- 28. 假设我们已将 bag 的 value_type 设置为 string，则会编写以下代码：
```cpp
bag exercise;
exercise.insert("squash");
exercise.insert("handball");
cout << exercise.grab() << endl;
cout << exercise.size() << endl;
```

- 29. 通常我们会选择能最好地利用先前编写的函数的方法。这既节省了工作量，也减少了为完成旧工作而编写新代码可能带来的新错误。如果编写新函数能提供更好的效率，则偏好会发生变化。

- 30. 我们想到的两行代码是：
```cpp
p = p->link();
p = list_search(p, d);
```
这两行代码与单行代码相同：p = list_search(p->link(), d);

- 31. 当目标不在 bag 中时，对 cursor 的第一个赋值语句会将其设置为空指针。这意味着循环体根本不会执行，函数返回答案零。

- 32. 当目标是链表上的第一个项目时，就会出现问题。在这种情况下，目标指针位于列表头部，因此在移动目标指针之前删除头节点将是一个错误。

- 33. cstdlib 中的 rand 函数生成非负伪随机整数。伪随机生成器对调试程序有利，因为如果在相同的初始条件下再次运行程序，生成器将产生完全相同的数字序列。

- 34. (rand() % 21) - 10;

- 35. 除 remove、grab 和 count（均为线性时间）之外，所有函数都是常数时间；复制构造函数和 operator =（均为 O(n)，其中 n 是被复制 bag 的大小）；operator +=（为 O(n)，其中 n 是加数的大小）；以及 operator +（为 O(m+n)，其中 m 和 n 是两个 bag 的大小）。

- 36. 序列类中需要前驱节点指针，因为其 insert 函数在当前节点之前立即添加新项目。由于链表工具包的 insert 函数在指定节点之后添加项目，因此前驱节点被指定为该节点。

- 37. many_nodes 是 3，其他成员变量如下：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_312_0.png)

- 38. 首先检查该项目是否出现在列表中的某个位置。如果没有，则不执行任何操作直接返回。如果项目在列表中，则将当前项目设置为等于该项目，并调用普通的 erase_one 函数。

- 39. insert 和 attach 函数都会分配动态内存，复制构造函数和赋值运算符也是如此。

- 40. 复制构造函数和赋值运算符可能会使用 list_piece。

- 41. 数组对随机访问最快。

- 42. 链表在光标处插入/删除最快。

- 43. 双向链表是最佳选择。

- 44. O(n)，其中 n 是调整大小前的数组大小

- 45. 参见第 286 页的图 5.18。

46. 这是一个解决方案：
```cpp
void dlist_head_insert(
    dnode*& head_ptr,
    const dnode::value_type& entry
)
{
    dnode *insert_ptr;
    insert_ptr =
        new dnode(entry, head_ptr);
    if (head_ptr != NULL)
        head_ptr->set_back(insert_ptr);
    head_ptr = insert_ptr;
}
```

47.
```cpp
void move_to_front(
    vector<string>& data,
    vector<string>::size_type index
)
{
    assert(index > 0);
    assert(index <= data.size());
    string item = data[index]; // Save a copy
    for (i = index; i > 0; --i)
        data[i] = data[i-1];
    // Put the copy at the front of the vector:
    data[0] = item;
}
```

## 图 5.18 双向链表节点的类定义

### 类定义

```cpp
class dnode
{
public:
    // TYPEDEF
    typedef double value_type;
    // CONSTRUCTOR
    dnode(
        const value_type& init_data = value_type(),
        dnode* init_fore = NULL,
        dnode* init_back = NULL
    )
    { data_field = init_data; link_fore = init_fore; link_back = init_back; }
    // Member functions to set the data and link fields:
    void set_data(const value_type& new_data) { data_field = new_data; }
    void set_fore(dnode* new_fore) { link_fore = new_fore; }
    void set_back(dnode* new_back) { link_back = new_back; }
    // Const member function to retrieve the current data:
    value_type data() const { return data_field; }
    // Two slightly different member functions to retrieve each current link:
    const dnode* fore() const { return link_fore; }
    dnode* fore() { return link_fore; }
    const dnode* back() const { return link_back; }
    dnode* back() { return link_back; }
private:
    value_type data_field;
    dnode *link_fore;
    dnode *link_back;
};
```

- 在这个项目中，你将使用 bag 类，其 value_type 为来自 <string> 设施的 string。bag 类应包含第 270 页图 5.13 中的 grab 函数。在程序中使用此类，程序需完成以下操作：
  1. 要求用户输入 10 个名词的列表。
  2. 要求用户输入 10 个动词的列表。
  3. 使用提供的名词和动词打印一些随机句子。
  例如，如果两个名词是“monkey”和“piano”，两个动词是“eats”和“plays”，那么我们可以期望以下任何句子：
  The monkey eats the piano.
  The monkey plays the piano.
  The piano eats the monkey.
  The piano plays the monkey.
  毫无疑问，这些句子并不完全合理。你的程序需要声明两个 bag 变量：一个用于存储名词，一个用于存储动词。使用合适的自顶向下设计。

- 编写一个函数，接受一个项目链表并删除列表中的所有重复项。在你的实现中，假设项目可以使用 == 进行相等性比较。

- 编写一个带有三个参数的函数。第一个参数是项目链表的头指针，接下来两个参数是项目 x 和 y。该函数应将列表中位于 x 第一次出现和 y 第一次出现之间的所有项目写入屏幕。你可以假设项目可以使用 == 进行相等性比较。

- 编写一个带有一个参数的函数，该参数是项目链表的头指针。该函数反转节点的顺序，使最后一个节点排在第一个，第一个节点排在最后，依此类推。头指针是引用参数，因此在函数完成后，同一个指针变量将指向反转列表的头部。

- 编写一个函数，该函数以两个链表头指针作为参数。假设链表的项目按 < 运算符排序。在每个列表中，每个项目都小于同一列表上的下一个项目。该函数应创建一个新链表，包含两个列表上的所有项目，并且新链表也应有序（因此每个新项目都小于列表上的下一个项目）。新链表中的每个项目应仅出现一次（即，如果同一项目同时出现在两个输入列表中，则只将一份副本放在新构建的链表中）。为了消除重复项目，你可以假设两个项目可以使用 == 进行相等性比较。该函数应返回新构建列表的头指针。

- 编写一个函数，该函数以一个单链表和一个称为拆分值的特殊值开始。两个项目值可以使用 < 运算符进行比较——但原始链表的项目没有特定顺序。该过程将节点分为两个链表：一个包含所有包含小于拆分值的项目的节点，另一个包含所有其他节点。如果原始链表中有任何重复整数（即，任何两个或多个具有相同项目的节点），那么包含该项目的新链表应具有重复该项目的相同数量的节点。无论你是保留原始链表还是在构建两个新链表的过程中销毁它都无关紧要，但你的注释应记录原始链表的情况。

- 编写一个函数，接受一个整数链表并重新排列节点，使存储的整数按顺序排序

