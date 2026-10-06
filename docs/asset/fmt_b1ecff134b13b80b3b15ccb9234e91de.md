
该语句为两个节点创建了空间，每个节点包含两个空字段，如下所示：

![](img/177eacb192165f90062789304b5da281_438_0.png)

![](img/177eacb192165f90062789304b5da281_438_1.png)

通过语句 `node1.next = &node2;` 可以使 `node1` 的 `next` 指指向 `node2`。该语句将 `node2` 的地址存储在 `node1.next` 字段中，从而在 `node1` 和 `node2` 之间建立了“链接”，如下：

![](img/177eacb192165f90062789304b5da281_438_2.png)

![](img/177eacb192165f90062789304b5da281_438_3.png)

`"xxxx"` 是 `node2` 的地址，变量 `node2.age` 的值将存储在这里。现在让我们给 `age` 字段赋值。

`node1.age = 35.50;`
`node2.age = 49.00;`

结果如下：

![](img/177eacb192165f90062789304b5da281_438_4.png)

![](img/177eacb192165f90062789304b5da281_438_5.png)

我们可以继续这个过程来创建具有任意数量节点的链表。例如：
`node2.next = &node3;`

我们知道列表是指一组顺序组织的项的集合。数组是列表的一个示例。在数组中，顺序组织是通过其索引隐含提供的。我们使用索引来访问和操作数组元素。数组的一个问题是，数组的大小在开始时必须精确指定。正如之前指出的，这在实际应用中可能是一项困难的任务。

表示列表的完全不同的方法是让列表中的每个项成为一个结构的一部分，该结构还包含指向下一个项的“链接”，如图 13.4 所示。这种类型的列表被称为*链*表，因为它的顺序是由从一个项到下一个项的链接给定的。

列表的每个元素都是一个*节点*，由两个字段组成：一个包含项，另一个包含列表中下一个项的地址（指向列表中下一个项的指针）。因此，链表是结构体的集合，其顺序不是根据它们在内存中的物理位置（如数组），而是根据存储在结构本身数据中的逻辑链接来排序的。链接的形式为指向相同类型另一个结构体的指针。

```c
struct node
{
  int item;
  struct node *next;
}
```

第一个成员是一个整数项，第二个成员是指向列表中下一个节点的指针，如下所示。记住，这里的项只是为了简单起见使用了整数，可以是任何复杂数据类型。

这种包含指向相同结构类型成员字段的结构体被称为自引用结构。节点可以用通用形式表示如下：

```c
struct tag-name
{
  type member1;
  type member2;
  ...
  struct tag-name *next;
}
```

该结构体可以包含多个具有不同数据类型的项。然而，成员之一可以是 `tag-name` 类型的指针。

让我们考虑一个简单的示例来阐明链接的概念。假设我们定义了如下结构体：

```c
struct link_list
{
  float age;
  struct link_list *next;
}
```

为了简单起见，我们假设列表包含两个节点 `node1` 和 `node2`。它们是 `link_list` 类型，并定义如下：

```c
struct link_list node1, node2;
```

该语句为两个节点创建了空间，每个节点包含两个空字段，如下所示：

通过语句 `node1.next = &node2;` 可以使 `node1` 的 `next` 指指向 `node2`。该语句将 `node2` 的地址存储在 `node1.next` 字段中，从而在 `node1` 和 `node2` 之间建立了“链接”，如下：

`"xxxx"` 是 `node2` 的地址，变量 `node2.age` 的值将存储在这里。现在让我们给 `age` 字段赋值。

`node1.age = 35.50;`
`node2.age = 49.00;`

# 动态内存分配与链表 431

![](img/177eacb192165f90062789304b5da281_442_0.png)

两个指针变量都指向同一个变量。
`*p = *q = 200 x <> y`

# (c) 赋值 *p = *q

此赋值语句将指针 `q` 指向变量的值存入指针 `p` 指向的变量的位置。

![](img/177eacb192165f90062789304b5da281_442_1.png)

指针 `p` 仍然指向同一个变量 `x`，但 `x` 的旧值被 `200`（由 `q` 指向）所替换。
`x = y = 200` 但 `p` 指向 `q`

# (d) NULL 指针

C 语言提供了一个特殊的常量 `NULL` (0)，用于初始化指向空内容的指针。
即语句：

```
p = 0; (或 p = NULL); -> p 0
q = 0; (或 q = NULL); -> q 0
```

使指针 `p` 和 `q` 指向空内容。它们可以用于指向任何值。
我们知道，指针在使用之前必须通过赋值内存地址来初始化。为指针分配内存地址的方法有两种：

- 1. 分配一个已存在变量的地址（静态分配）
  `ptr = &count;`
- 2. 使用内存分配函数（动态分配）
  `ptr = (int*)malloc(sizeof(int));`

# 13.1 创建链表

我们将链表视为一种抽象数据类型，并执行以下基本操作：
1. 创建列表。
2. 遍历列表。

McGraw-Hill 公司

432 ANSI C 编程

- 3. 统计列表中的项数。
4. 打印列表（或子列表）。
5. 查找项以便编辑或打印。
6. 插入项。
7. 删除项。
8. 合并两个列表。

在 13.7 节中，我们使用结构体变量 `node1` 和 `node2` 创建了一个两个元素的链表。我们还使用了地址运算符 `&` 和成员运算符来创建和访问单个项。使用链表的核心思想是避免对列表中特定数量项的任何引用，以便我们可以根据需要插入或删除项。这可以通过使用“匿名”引用来存储节点来实现。这些位置不是通过名称访问的，而是通过引用它们的指针访问的。（例如，我们必须避免诸如 `node1.age ->` 这样的引用）

匿名位置是通过指针和动态内存分配函数（如 `malloc`）创建的。我们使用指针 `head` 来创建和访问匿名节点。考虑以下：

```
struct linked_list {
    int number;
    struct linked_list *next;
};
typedef struct linked_list node;
node *head;
head = (node *)malloc(sizeof(node));
```

`struct` 声明仅仅描述了节点的结构，并不分配存储。只有在语句中调用函数 `malloc` 时，才会创建节点的存储空间：

```
head = (node *)malloc(sizeof(node));
```

该语句获取一段足够存储节点的内存，并将其地址赋值给指针变量 `head`。该指针指示链表的起始。

![](img/177eacb192165f90062789304b5da281_443_0.png)

以下语句将值存储在成员字段中：

```
head -> number = 10;
head -> next = NULL;
```

![](img/177eacb192165f90062789304b5da281_443_1.png)

可以如下添加第二个节点：

```
head -> next = (node *)malloc(sizeof(node));
head -> next -> number = 20;
head->next->next = NULL;
```

McGraw-Hill 公司

动态内存分配与链表 433

虽然这个过程可以继续创建任意数量的节点，但如果节点超过两个，就会变得繁琐笨拙。上述过程可以使用递归和迭代技术轻松实现。可以通过自替换语句指针从当前节点移动到下一个节点，例如：

```
head -> next;
```

程序 13.3 显示了如何使用递归创建一个完整的链表并打印其内容。

# 程序 13.3

编写一个程序交互地创建一个线性链表，并打印列表以及列表中的项总数。

图 13.7 所示的程序使用语句为第一个节点动态分配一块内存：

```
head = (node*)malloc(sizeof(node));
```

返回一个指向 `node` 类型结构的指针。该函数请求在函数创建的当前节点中放置数字。如果赋值给当前节点的值 -999，则将 `next` 赋值给指针变量 `next`，否则再次为下一个节点分配内存空间并将 `malloc` 函数的值放在其中。`create` 函数递归地调用自己，该过程将持续到我们输入数字 -999。

列表中存储的项使用 `print` 函数打印，该函数接受当前节点的指针作为参数。这是一个递归函数，并在接收到 `NULL` 指针时停止。算法如下：

- 1. 从第一个节点开始。
- 2. 只要还有有效的节点：
  (a) 打印当前项，
  (b) 移动到下一个。

同样，`count` 函数递归地统计列表中的项数并返回给 `main` 函数。计数不包含 -999（包含在哑节点中）。

```c
Program
#include <stdio.h>
#include <stdlib.h>
#define NULL 0
struct linked_list {
    int count;
    struct linked_list *next;
};
typedef struct linked_list node; /* node 类型 */
main()
```

McGraw-Hill 公司

434 ANSI C 编程

```c
{
    node *head;
    void create(node *p);
    int count(node *p);
    void print(node *p);
    head = (node*)malloc(sizeof(node));
}
void create(node *p) {
    printf("Enter number: ");
    scanf("%d", &p->count);
    if (p->count != -999) {
        p->next = (node*)malloc(sizeof(node));
        create(p->next);
    } else {
        p->next = NULL;
    }
}
int count(node *p) {
    if (p != NULL && p->count != -999) {
        return 1 + count(p->next);
    }
    return 0;
}
void print(node *p) {
    if (p != NULL && p->count != -999) {
        printf("%d ", p->count);
        print(p->next);
    }
}
```

McGraw-Hill 公司

动态内存分配与链表 435

# 12 插入项

链表的优势之一是插入新节点非常方便，只需要重置指针（而不是像数组那样移动元素）。

将新项（例如 X）插入列表有三种情况：

- 1. 在列表头部插入。
- 2. 在列表中间插入。
- 3. 在列表末尾插入。

插入过程发生在查找插入位置之前。查找涉及定位新项之后的节点。通用的插入算法如下：

```
Begin
if列表为空或
  新节点在头部节点之前，
  将新节点作为头部节点，
else
  如果新节点在最后一个节点之后，
  将新节点作为末尾节点，
else
  在列表主体插入新节点。
结束
```

将新项放在列表开头的算法如下：

- 1. 获取新节点的空间。
- 2. 将数据分配给新节点的项字段。
- 3. 将新节点的 `next` 字段指向列表开头。
- 4. 将头部指针指向新节点。

在两个现有节点（例如 N1 和 N2）之间插入 X 的算法如下：

- 1. 为新节点 X 设置空间。
- 2. 为 X 的项赋值。
- 3. 将 X 的 `next` 字段指向 N2。
- 4. 将 N1 的 `next` 字段指向 X。

在列表末尾插入项的算法与在中间插入的算法类似，但新节点的 `next` 字段为 NULL（如果存在则指向哑节点）。

McGraw-Hill 公司

436 ANSI C 编程

```c
node *insert(node *head, int x) {
    node *new = (node*)malloc(sizeof(node));
    new->data = x;
    if (head == NULL) {
        new->next = NULL;
        head = new;
    } else {
        node *temp = head;
        while (temp->next != NULL) {
            temp = temp->next;
        }
        temp->next = new;
        new->next = NULL;
    }
    return head;
}
```

# 13.2 删除项

要从链列表中删除项，我们必须找到被删除的节点及其前驱节点。

删除算法如下：

1. 定位要删除的节点。
2. 如果该节点是头部节点，更新头部指针指向下一个节点。
3. 如果该节点不是头部节点，更新前驱节点的 `next` 指针，指向被删除节点之后的节点。
4. 释放被删除节点的内存。

此过程可以使用递归或迭代实现。

McGraw-Hill 公司

437

# 13.3 合并两个列表

合并两个列表意味着将两个列表合并为一个。可以通过将第二个列表附加到第一个列表末尾来实现。

合并算法如下：

1. 找到第一个列表的最后一个节点。
2. 将最后一个节点的 `next` 指针指向第二个列表的头部。

```c
node *merge(node *list1, node *list2) {
    if (list1 == NULL) return list2;
    if (list2 == NULL) return list1;
    node *temp = list1;
    while (temp->next != NULL) {
        temp = temp->next;
    }
    temp->next = list2;
    return list1;
}
```

McGraw-Hill 公司

438

# 13.4 查找项

在链列表中查找项涉及遍历列表直到找到该项。

```c
int search(node *head, int key) {
    node *temp = head;
    while (temp != NULL) {
        if (temp->data == key) return 1;
        temp = temp->next;
    }
    return 0;
}
```

# McGraw-Hill 公司

# 动态内存分配与链表 437

```c
node *nl;               /*指向前一个键节点的指针 */
int key;
int x;
                            /* 要插入的新项（数字） */
printf("Value of new item?");
scanf("%d", &key);
printf("Value of key item? (type -999 if last)");
scanf("%d", &key);
if(head->number == key)     /* 新节点为第一个节点 */
    new = (node)malloc(sizeof(node));
    new->number = x;
    new->next = head;
    head = new;
else
    /* 查找键节点并插入新节点 */
    /* 在键节点之前插入 */
    nl = find(head, key);      /* 查找键节点 */
    if(nl == NULL)
        printf("\nkey is not found \n");
    else
        /* 插入新节点 */
        {
            new = (node)malloc(sizeof(node));
            new->number = x;
            new->next = nl->next;
            nl->next = new;
        }
return(head);
node *find(node, int key)
{
    if(list->next->number == key) /* 找到键节点 */
        return(list);
    else
        if(list->next->next == NULL) /* 末尾 */
            return(NULL);
        else
            find(list->next, key);
}
```
