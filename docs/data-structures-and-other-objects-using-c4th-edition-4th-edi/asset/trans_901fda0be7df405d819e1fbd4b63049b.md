

由于 cursor 不为 NULL，我们进入循环体。每次迭代都会使 answer 加 1，然后执行 `cursor = cursor->link()`。`cursor = cursor->link()` 的作用是将第一个节点的链接字段复制到 cursor 本身，使得 cursor 最终指向第二个节点。一般来说，语句 `cursor = cursor->link()` 将 cursor 移动到下一个节点。因此，在循环第一次迭代完成时，情况如下：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_261_0.png)

循环继续。第二次迭代后，answer 为 2，cursor 指向列表的第三个节点，如下所示：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_261_1.png)

每次完成一次循环迭代时，cursor 指向列表中的某个位置，answer 是该位置之前的节点数量。在我们的示例中，我们即将第三次也是最后一次进入循环体。在最后一次迭代中，answer 递增到 3，cursor 变为 NULL，如下所示：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_261_2.png)

指针变量 cursor 已变为 NULL，因为循环控制语句 `cursor = cursor->link()` 将第三个节点的链接字段复制到了 cursor 中。由于此链接为 NULL，cursor 中的值现在为 NULL。此时，循环的控制测试 `cursor != NULL` 为假。循环结束，函数返回 answer 3。

## 图 5.5 计算链表长度的函数

## 函数实现

```
size_t list_length(const node* head_ptr)
// Precondition: head_ptr is the head pointer of a linked list.
// Postcondition: The value returned is the number of nodes in the linked list.
// Library facilities used: cstdlib
{
    const node *cursor;
    size_t answer;

    answer = 0;
    for (cursor = head_ptr; cursor != NULL; cursor = cursor->link())
    ++answer;
    return answer;
}
```

`list_length` 函数的完整实现如图 5.5 所示。请注意，局部变量 `cursor` 使用 `const` 关键字声明：`const node *cursor;`。这是必需的，因为 `head_ptr` 参数是 const 的，因此如果 `cursor` 不是 const，编译器将不允许赋值 `cursor = head_ptr`。一般来说，如果指针使用 `const` 关键字声明，则该指针只能赋值给另一个也使用 `const` 关键字声明的指针。

## 如何遍历链表

你应该学习遍历链表的重要模式，如在 `list_length` 函数（图 5.5）中所用。每当你需要逐个遍历链表的节点时，都可以使用相同的模式。

模式的第一部分涉及从一个节点移动到另一个节点。每当我们有一个指向某个节点的指针，并且我们希望指针指向下一个节点时，就必须使用该节点的链接。我们遵循的推理如下：

- 1. 假设 cursor 指向某个节点；
- 2. 然后 cursor->link() 指向下一个节点（如果存在），如下所示：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_263_0.png)

- 3. 要将 cursor 移动到下一个节点，我们使用赋值语句：
cursor = cursor->link();

如果没有下一个节点，则 cursor->link() 将为 NULL，因此我们的赋值语句将把 cursor 设置为 NULL。

关键是要知道，赋值语句 cursor = cursor->link() 会移动 cursor 使其指向下一个节点。如果没有下一个节点，则赋值语句将 cursor 设置为 NULL。

模式的第二部分展示了如何从头节点开始遍历链表的所有节点。循环的模式如下：

```
for (cursor = head_ptr; cursor != NULL; cursor = cursor->link())
{
    ... Inside the body of the loop, you may
    carry out whatever computation is
    needed for a node in the list.
}
```

你会发现自己在操作链表的函数中不断使用这个模式。

## 陷阱

### 忘记测试空列表

操作链表的函数应始终进行测试，以确保它们对空列表具有正确的行为。例如，当 head_ptr 为 NULL（表示空列表）时，我们的 list_length 函数应返回 0。

如何将节点指针作为参数使用

### 链表的参数

当函数操作链表时，其参数之一必须是指向列表中节点的指针——通常是头指针，但有时也会使用另一个指针。这些节点指针通常以三种方式用作参数，在我们继续介绍工具包之前，需要稍作讨论。（你可能以为自己已经了解关于参数的一切了！）

带有 const 关键字的指针参数。我们已经详细考察过这种情况。例如，list_length 函数就有这样的参数：

```
size_t list_length(const node* head_ptr);
```

该函数使用头指针访问列表的节点，但函数不会更改列表的任何部分。一般来说，这就是应该使用 `const node*` 的情况。当函数需要访问链表并且函数不会对列表的任何节点进行任何更改时，应使用指向常量节点的指针。

### 作为节点指针的值参数。

第二种节点指针参数是不带 `const` 关键字的值参数。例如，工具包中的一个函数将在列表中指定节点之后添加一个新节点。该函数带有 `node*` 的以下原型：

```
void list_insert(node* p, const node::value_type& entry)
// Precondition: previous_ptr points to a node in a linked list.
// Postcondition: A new node containing the given entry has been added
// after the node that p points to.
```

该函数使用指针 p 访问列表的节点，并在 p 节点之后添加一个新节点。指针 p 不会改变，它将继续指向同一个节点。但该节点的链接字段将发生变化，并且一个新节点将被添加到列表中。一般来说，这就是应该使用值参数的情况：当函数需要访问链表，函数可能会更改链表，但函数不需要让指针指向一个新节点时，节点指针应为值参数。

### 作为节点指针的引用参数。

有时函数必须让指针指向一个新节点。例如，工具包中的一个函数将在链表前面添加一个新节点，带有以下原型和前置/后置条件契约：

```
void list_head_insert
(node*& head_ptr, const node::value_type& entry);
// Precondition: head_ptr is the head pointer of a linked list.
// Postcondition: A new node containing the given entry has been added at
// the head of the list; head_ptr now points to the head of the new, longer
// linked list.
```

head_ptr 是一个引用参数，因为函数创建一个新头节点并使头指针指向这个新节点。当函数需要访问链表并且函数使指针指向一个新节点时，节点指针应为引用参数。对指针的这种更改将使实际参数指向一个新节点。

## 链表的参数

当函数需要访问链表时，请使用 node* 参数并遵循以下准则：

- 1. 当函数需要访问链表且不会对列表的任何节点进行任何更改时，使用指向常量节点的指针 const node*。
- 2. 当函数可能以某种方式更改列表，但不需要让指针指向一个新节点时，使用值参数 node*。
- 3. 当函数需要访问链表且可能让指针指向一个新节点时，使用引用参数 node*&。

## 在链表头部插入新节点

我们工具包中的下一个函数是前面提到的 list_head_insert 函数，它带有一个指针的引用参数。该函数在链表头部添加一个新节点。这是添加新节点最简单的位置。带有完整文档的函数原型如下：

```
void list_head_insert
(node*& head_ptr, const node::value_type& entry);
// Precondition: head_ptr is the head pointer of a linked list.
// Postcondition: A new node containing the given entry has been added at
// the head of the list; head_ptr now points to the head of the new, longer
// linked list.
// NOTE: If there is insufficient dynamic memory for a new
// node, then bad_alloc is thrown.
```

正如刚才所见，头指针是一个引用参数，因为函数使头指针指向一个新节点。另外，文档说明了如果新节点的动态内存不足会发生什么。

在链表头部插入新节点只需要一条语句：

```
head_ptr = new node(entry, head_ptr);
```

让我们逐步执行这条语句，看看新节点是如何添加到列表前面的。在示例中，假设 head_ptr 指向这里显示的短列表，并且新条目是数字 5：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_265_0.png)

