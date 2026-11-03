
单个项目。 使用链表的根本思想是为了避免对列表中特定项目数量的任何引用，以便我们可以根据需要插入或删除项目。 这可以通过使用“匿名”位置来存储节点来实现。 这种位置不是通过名称访问，而是通过指向它们的指针来访问。 （例如，我们必须避免使用像 node1.age 和 node1.next -> age 这样的引用。）

匿名位置是使用指针和动态内存分配函数（如 malloc）创建的。 我们使用指针 head 来创建和访问匿名节点。 考虑以下内容：

```
struct linked_list
{
    int number;
    struct linked_list *next;
};
typedef struct linked_list node;
node *head;
head = (node *) malloc(sizeof(node));
```

结构体声明仅描述节点的格式，并不分配存储空间。 节点的存储空间仅在调用 malloc 函数的语句中创建

```
head = (node *) malloc(sizeof(node));
```

该语句获取一块足以存储节点的内存，并将其地址分配给指针变量 head。 该指针表示链表的开始。

![](img/65953ea584e494f3d396b2252cb5ea53_411_0.png)

以下语句将值存储在成员字段中：

```
head -> number = 10;
head -> next   = NULL;
```

![](img/65953ea584e494f3d396b2252cb5ea53_411_1.png)

第二个节点可以按如下方式添加：

```
head->next = (node *)malloc(sizeof(node));
head->next->number = 20;
head->next->next = NULL;
```

尽管此过程可以继续以创建任意数量的节点，但如果节点超过两个，则会变得繁琐和笨拙。 上述过程可使用递归和迭代技术轻松实现。 指针可以通过诸如 self-replacement 语句之类的语句从当前节点移动到下一个节点

```
head = head -> next;
```

示例 15.3 显示了使用递归创建完整的链表并打印其内容。

## 示例 15.3

编写一个程序以交互方式创建线性链表并打印出列表和列表中的项目总数。

图 15.7 所示的程序首先使用语句动态分配一块内存用于第一个节点

```
head = (node *)malloc(sizeof(node));
```

它返回一个指向先前已定义类型的 node 结构的指针。 然后由函数 create 创建链表。 该函数请求要放置在已创建的当前节点中的数字。 如果分配给当前节点的值为 −999，则将 NULL 分配给指针变量 next，列表结束。 否则，使用 malloc 函数再次为下一个节点分配内存空间，并将下一个值放入其中。 请注意，函数 create 会递归调用自身，并且该过程将一直持续到我们输入数字 −999 为止。

链表中存储的项目使用函数 print 打印，该函数接受指向当前节点的指针作为参数。 它是一个递归函数，并在接收到 NULL 指针时停止。

打印算法如下：

- 1. 从第一个节点开始。
- 2. 当仍有有效节点可打印时
  (a) 打印当前项目并
  (b) 前进到下一个节点。

同样，函数 count 递归地计算列表中的项目数并将项目总数返回给主函数。 请注意，计数不包括项目 −999（包含在虚拟节点中）。

```
Program
/* *************************************************************** */
/*          CREATING A LINEAR LINKED LIST                         */
/* *************************************************************** */
#include <stdio.h>
#include <stdlib.h>
#define NULL 0
struct linked_list
{
    int number;
    struct linked_list *next;
};
typedef struct linked_list node; /* node type defined */
```

```c
main()
{
    node *head;
    void create(node *p);
    int     count(node *p);
    void    print(node *p);

    head = (node *)malloc(sizeof(node));
    create(head);
    printf("\n");
    print(head);
    printf("\n");
    printf("\nNumber of items = %d\n",count(head));
}
void create(node *list)
{
    printf("Input a number\n");
    printf("(type -999 at end): ");
    scanf("%d",&list->number);/* create current node */
    if(list->number == -999)
    {
        list->next = NULL;
    }
    else    /* create next node */
    {
        list->next = (node *)malloc(sizeof(node));
        create(list->next);
    }
    return;
}
void print(node *list)
{
    if(list->next != NULL)
    {
        printf("%d -> ",list->number);/* print current item */
        if(list->next->next == NULL)
            printf("%d",list->next->number);
        print(list->next);  /* move to next item */
    }
    return;
}
int count(node *list)
{
    if(list->next == NULL)
        return (0);
    else
        return(1 + count(list->next));
}
```

## 输出

输入一个数字
(输入 -999 结束): 60

![](img/65953ea584e494f3d396b2252cb5ea53_414_0.png)

## 插入项目

链表的一个优点是插入新节点相对容易。 它只需要重置两个指针（而不是像数组那样移动数据列表）。

将新项目（例如 X）插入列表有三种情况：

- 1. 在列表前端插入。
- 2. 在列表中间插入。
- 3. 在列表末尾插入。

插入过程先于插入位置的搜索。 搜索涉及定位要在其后插入新项目的节点。 插入的一般算法如下：

```
*Begin*
  *if* the list is empty or
    the new node comes before the head node *then*,
    insert the new node as the head node,
  *else*
    If the new node comes after the last node, *then*,
    insert the new node as the end node,
    *else*
    insert the new node in the body of the list.
*End*
```

将新项目放在链表开头 的算法：

- 1. 为新节点获取空间。
- 2. 将数据分配给新节点的项目字段。
- 3. 设置新节点的 next 字段以指向列表的开始。
- 4. 将 head 指针更改为指向新节点。

在两个现有节点（例如 N1 和 N2）之间插入新节点 X 的算法；

- 1. 为新节点 X 设置空间。
- 2. 为 X 的项目字段分配值
- 3. 设置 X 的 next 字段以指向节点 N2
- 4. 设置 N1 的 next 字段以指向 X

在列表末尾插入项目的算法与在中间插入的算法类似，只是新节点的 next 字段被设置为 NULL（或设置为指向虚拟或哨兵节点（如果存在））。

## 示例 15.4

编写一个函数，在指定的节点（称为关键节点）之前插入给定项目。

图 15.8 所示的函数 insert 请求要插入的项目以及 'key node'。 如果插入发生在开头，则为新节点创建内存空间，将新项目的值分配给它，并将指针 head 分配给新成员。 指示新节点开头的指针 new 被分配给 head。 请注意以下语句：

```
new->number = x;
new->next = head;
head = new;
```

```
/**********************************************************************/
/*                                                                    */
/*                         FUNCTION INSERT                           */
/*                                                                    */
/**********************************************************************/
node *insert(node *head)
{
    node *find(node *p, int a);
    node *new;      /* pointer to new node */
    node *n1;       /* pointer to node preceding key node */
    int key;
    int x;          /* new item (number) to be inserted */
    printf("Value of new item?");
    scanf("%d", &x);
    printf("Value of key item? (type -999 if last )");
    scanf("%d", &key);
    if(head->number == key) /* new node is first */
    {
        new = (node *) malloc(sizeof(node));
        new->number = x;
        new->next = head;
        head = new;
    }
    else    /* find key node and insert new node */
            /* before the key node */
    {
        n1 = find(head, key);  /* find key node */
        if(n1 == NULL
