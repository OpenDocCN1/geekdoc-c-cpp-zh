

## 第 6.3 节自测练习

- 17. 你已经计算出大小为 10 和 40 的两个集合的并集，但答案中只有 42 个元素。这是怎么回事？

- 18. 你如何使用 set_union 函数来判断一个集合的所有元素是否也包含在另一个集合中（即，一个集合是另一个集合的子集）？

- 19. multiset 提供哪种 const 迭代器类别？

- 20. 随机访问迭代器如何访问当前项前面 n 步的一个项？

- 21. 编写一个具有一个参数的函数：非空 const 字符串 multiset。返回值是 multiset 中最长字符串的副本。如果有几个长度相等的字符串，则返回迭代器最先找到的那个。

- 22. 假设你有两个迭代器 s 和 t，遍历同一个容器，且 *s 和 *t 都是 42。(s==t) 总是为真吗？

## 6.4 节点模板类

在第 5.1 节和第 5.2 节中，我们实现了一个用于操作链表的节点类。如你所料，如果将节点实现为依赖于底层 Item 数据类型的模板类，节点将更加有用。然后，节点的每个函数都可以实现为也依赖于该项的节点函数。

下面是原始工具包的节点定义与我们新计划的对比：

| 原始节点类： | 新模板节点类： |
| :--- | :--- |
| `class node` | `template <class Item>` |
| `{` | `class node` |
| `public:` | `{` |
| `typedef double value_type;` | `public:` |
| `...` | `typedef Item value_type;` |
| | `...` |

有了新定义，节点现在是一个模板类。节点的每个函数都可以通过进行与第 6.2 节中看到的相同的更改，将其改为模板函数。

例如，下面是 list_insert 函数的原始原型：

```
void list_insert(node* previous_ptr, const node::value_type& entry);
```

list_insert 模板函数的新原型前面带有模板前缀，并在其参数列表中使用 Item，如下所示：

```
template <class Item>
void list_insert
(node<Item>* previous_ptr, const Item& entry);
```

工具包的一个函数 list_locate 需要额外小心。我们的原始节点有一个 const 版本和一个非 const 版本，两者都有一个 size_t 参数，如下所示：

```
node* list_locate(node* head_ptr, size_t position);
const node* list_locate
(const node* head_ptr, size_t position);
```

如我们在第 299 页的陷阱“模板函数参数不匹配”中解释的那样，size_t 参数的存在可能导致参数类型不匹配。解决方案与我们之前使用的方法相同：添加第二个模板参数。此外，我们实际上可以通过使用名为 NodePtr 的模板参数将两个函数合并为一个函数，如下面的新原型所示：

```
template <class NodePtr, class SizeType>
NodePtr list_locate(NodePtr head_ptr, SizeType position);
```

当程序调用 list_locate 时，头指针可以是指向节点的普通指针，也可以是使用 const 关键字声明的指针。返回类型将始终与头指针的类型匹配。

### 返回引用类型的函数

我们还有一个更改将简化以后对节点的使用。该更改涉及 data 成员函数，该函数检索节点数据字段的副本。实现的合理想法如下所示：

```
Item data( ) const { return data_field; }
```

这是一个 const 成员函数，因此不能用于实际更改节点（它只返回数据字段的副本）。

我们计划的更改是在返回类型中添加 & 符号，并修改函数使其不再是 const 函数，如下所示：

```
Item& data( ) { return data_field; }
```

& 符号将返回值更改为引用类型。引用类型在 C++ 中有多种用途，但我们只考虑一种狭义用途：将引用类型用作函数的返回值，如下文所述。

### 引用类型作为返回值

函数可以通过在返回类型名称后放置 & 符号来使用引用类型作为返回值。使用引用类型有以下效果：

- 1. 返回值必须是函数返回后仍然存在的变量或对象。特别是，返回值不能是局部变量。
- 2. 函数返回此实际变量或对象（而不是对象的副本）。

让我们看一个示例，了解如何使用新的 data 函数来更改节点的数据字段。假设 cursor 指向这个字符串链表的第二个节点：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_346_0.png)

让我们检查一些语句，了解如何使用 cursor->data() 直接操作第二个节点的数据字段：

```
cursor->data() = "myrie";
```

这只是一个赋值语句，但赋值号左边是 cursor 节点实际数据字段的引用，因此该数据将更改为字符串 "myrie"，如下所示：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_346_1.png)

对节点数据字段的赋值并不太有趣；我们本可以使用 cursor->set_data("myrie") 完成同样的事情。一个更好的示例展示了如何通过激活其成员函数之一来更改节点的数据。例如，考虑前面链表的这条语句：

```
head_ptr->data().erase(0,2);
```

字符串的 erase(0,2) 成员函数从字符串开头擦除两个字符，将 "eenie" 更改为 "nie"，并得到如下所示的链表：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_347_0.png)

### 当引用返回值被复制到其他位置时会发生什么

当引用返回值被复制到另一个变量时，很容易对会发生什么感到困惑。例如，考虑前面显示的最终链表，其中 cursor 的数据字段是 "mynie"。你能弄清楚这两条语句会发生什么吗？

```
string exclamation = cursor->data();
exclamation = "drat!";
```

exclamation 变量与 cursor 的数据完全分开。第一条语句将 cursor 数据的副本放入 exclamation。第二条语句将 exclamation 更改为 "drat!"，但不会更改 cursor 的数据。

一般来说，cursor->data() 只能通过对 cursor->data() 进行赋值或激活 cursor->data() 的成员函数之一来更改 cursor 的数据。

### data 成员函数现在需要两个版本

将 data 返回值更改为引用类型有一个缺点：data 函数的这个版本不再可以用作常量成员函数。解决方案与我们已经为 link 成员函数使用的想法类似：为 data 函数提供第二个常量版本，如下所示：

```
const Item& data( ) const { return data_field; }
```

这个版本与我们的另一个版本有两处更改：

- 返回值是对 const 值的引用。由于它是引用类型，它仍将直接引用节点的数据字段。但由于 const 关键字，它不能用于更改该数据字段。
- 由于返回值不能用于更改节点，该函数可以声明为节点类的常量成员函数。

拥有两个 data 成员函数的方法与我们在第 228 页提供两个独立 link 成员函数的动机相同。此外，编译器能够在任何情况下确定调用哪个函数。如果指针 p 是指向 const 节点的指针，则 p->data() 将激活 data 的 const 版本；否则使用非 const 版本。

### 新节点的头文件和实现文件

新节点的头文件 (node2.h) 和实现文件 (node2.template) 在图 6.4 中给出。我们还更新了文档，以指示 data 成员函数两个版本的效果。供您参考，您可能希望翻回到将容器类转换为模板类所需的完整更改列表（第 304 页）。

## 第 6.4 节自测练习

- 23. 假设第 5 章的一个函数有一个名为 insert_ptr 的局部变量，它是指向节点的指针。你将在该函数的模板版本中如何声明此变量？

- 24. 编写 list_head_remove 模板版本的实现。

- 25. 假设 p 是字符串链表中一个节点的指针，该节点的数据是字符串 "help"。执行以下两条语句后，该数据的值是多少：p->data().erase(3,1); p->data().append("lo");

- 26. 假设 p 是前一题中指向 const 节点的指针。允许这两条语句吗？

- 27. 在节点模板类中，编译器如何在任何情况下确定调用哪个 data() 成员函数？

### 图 6.4 节点模板类的头文件和实现

### 头文件

```
// FILE: node2.h (part of the namespace main_savitch_6GB)
// PROVIDES: A template class for a node in a linked list and functions for
// manipulating linked lists. The template parameter is the type of data in each node.
// 
// TYPEDEF for the node<item> template class:
// Each node of the list contains a piece of data and a pointer to the next node. The
// type of the data (node<item>::value_type) is the item type from the template parameter.
// The type may be any of the C++ built-in types (int, char, etc.), or a class with a default
// constructor, an assignment operator, and a test for equality.
// 
// CONSTRUCTOR for the node<item> class:
// node(const Item& init_data, node* init_link)
// Postcondition: The node contains the specified data and link.
// NOTE: The init_data parameter has a default value that is obtained from the default
// constructor of the item type. In the ANSI/ISO standard, this notation is also allowed
// for the built-in types, providing a default value of zero. The init_link has a default
// value of NULL.
```

