
```
struct node *link; /* Pointer to next node of the list */
};
```

![](img/a76c706396af8b310f291a5313a27079_324_0.png)

链表的节点在内存中不是连续存储的。在数组列表中，我们可以使用数组名执行操作。在链表的情况下，我们将借助指向链表第一个节点的指针执行所有操作。该指针通常命名为 start，并且是我们访问链表的唯一来源。如果指针 start 包含 NULL 值，则列表将被视为空。

现在我们取一个链表，其信息部分包含一个整数值。该列表节点的结构定义如下-

```c
struct node{
    int info;
    struct node *link;
};
```

指针变量 start 将声明为-

```c
struct node *start;
```

这里有一个包含 4 个节点的链表-

![](img/a76c706396af8b310f291a5313a27079_324_1.png)

我们可以清楚地看到，每个节点的地址存储在前一个节点的 link 部分中，第一个节点的地址存储在指针变量 start 中。最后一个节点的 link 部分包含 NULL。

我们将讨论该列表的以下操作。

- (i) 遍历列表
- (ii) 搜索元素
- 元素的插入
- 元素的删除
- 列表的创建
- 列表的反转

## 15.1 遍历链表

遍历列表意味着恰好访问每个节点一次。为此我们取一个结构指针 ptr。初始时 ptr 被赋值为 start。

```c
ptr = start;
```

现在 ptr 指向链表的第一个节点。我们可以通过编写 ptr->info 来访问第一个节点的信息部分。

现在我们将指针 ptr 向前移动，使其指向下一个元素。这可以通过将下一个元素的地址赋给 ptr 来轻松完成，如—

```c
ptr = ptr->link;
```

现在 ptr 具有下一个元素的地址。同样，我们可以通过赋值遍历链表的每个元素，直到 ptr 具有 NULL 值，即最后一个元素的 link 部分值。因此，链表可以遍历如下—

```c
while(ptr!=NULL)
{
    printf("%d ",ptr->info);
    ptr=ptr->link;
}
```

## 15.2 在链表中搜索

在搜索元素时，我们遍历链表，并在遍历过程中将每个元素的信息部分与给定元素进行比较。可以写成—

```c
while(ptr!=NULL)
{
    if(ptr->info==data)  /*Search successful*/
        ............
    else
        ptr=ptr->link;  /*Go to next element*/
}
```

这里 data 是我们想要搜索的元素。

## 15.3 向链表中插入

链表中的插入可能有两种方式—

- 在开头插入
- 在中间或末尾插入

要插入一个节点，首先我们将使用 malloc() 为该节点动态分配空间。假设 tmp 是一个指向此动态分配节点的指针。在节点的信息部分我们将放置值。

```c
tmp = (struct node *)malloc( sizeof(struct node) );
tmp->info = data;
```

节点的 link 部分包含垃圾值，我们将在两种情况下分别为其分配地址。

### 15.4 在开头插入

插入后，新节点将成为第一个节点，而当前第一个节点将排在第二位。因此我们只需要调整节点的链接。

```c
tmp->link = start;
```

现在插入的节点指向下一个节点，即链表的开始节点。

现在插入的节点是链表的第一个节点。因此 start 应重新分配为-

```c
start = tmp;
```

现在 start 将指向插入的节点，即链表的第一个节点。

下图显示了此过程，虚线表示插入前的链接。

![](img/a76c706396af8b310f291a5313a27079_326_0.png)

### 15.5 在中间或末尾插入

首先我们遍历链表以获取要在其后插入元素的节点。我们获取指针 q，该指针指向要在其后插入新节点的元素。要在节点后插入元素，我们将该节点的 link 部分赋给插入节点的 link 部分，并将插入节点的地址放入前一个节点的 link 部分。

```c
tmp->link = q->link;
```

```c
q->link = tmp;
```

这里 q 指向前一个节点。执行语句 1 后，插入节点的 link 将指向前一个节点之后的下一个节点。

执行语句 2 后，前一个节点的 link 将指向插入的节点。

如果要在末尾插入节点，以上两个语句也适用。在这种情况下，q 将指向最后一个节点，因此 q->link 将为 NULL。因此执行语句 1 后，插入节点的 link 将指向 NULL。插入节点的 link 部分将具有 NULL，因此它将成为最后一个节点。

![](img/a76c706396af8b310f291a5313a27079_327_0.png)

## 15.6 从链表中删除

要从链表中删除节点，首先我们遍历链表并与每个元素进行比较。找到元素后，删除可能有两种情况-

1. 删除第一个节点
2. 删除中间或末尾的节点

节点的删除也需要调整链接。这些链接操作会将节点从链表中删除，但它仍会占用内存。由于每个节点的内存都是由我们动态分配的，因此在删除节点后释放该内存是我们的责任。为了释放内存，我们将使用 free() 函数，为此我们需要一个指向要删除节点的指针。我们取一个指针 tmp 使其指向要删除的节点，并在删除节点后调用 free，如-

```c
free(tmp);
```

### 15.7 删除第一个节点

![](img/a76c706396af8b310f291a5313a27079_327_1.png)

由于要删除的节点是第一个节点，因此 tmp 将被赋予第一个节点的地址。

```c
tmp = start;
```

因此现在 tmp 指向要删除的第一个节点。

由于 start 指向链表的第一个节点，因此 start->link 将指向链表的第二个节点。删除第一个节点后，第二个节点将成为第一个节点，因此 start 应被赋予第二个节点的地址，如-

```c
start = start->link;
```

现在我们应该释放要删除的元素，即由 tmp 指向的。

```c
free( tmp );
```

### 15.8 删除中间或末尾的节点

![](img/a76c706396af8b310f291a5313a27079_328_0.png)

我们将遍历列表并获取一个指向要删除节点前一个节点的指针。假设该指针是 q，因此要删除的节点将被 q->link 指向，因此我们将此值赋给 tmp，如-

```c
tmp = q->link;
```

因此现在 tmp 将指向要删除的节点。现在我们将要删除节点的 link 部分赋给前一个节点的 link 部分。可以这样做-

```c
q->link = tmp->link;
```

现在前一个节点的 link 将指向要删除节点之后的节点。最后我们将释放已删除的节点，如-

```c
free(tmp);
```

如果要删除的节点是链表的最后一个节点，则第二个语句可以写成-

```c
q->link = NULL;
```

## 15.9 创建列表

如果您理解了上述操作，创建列表非常简单。它类似于在列表末尾插入元素。首先我们将为节点分配内存，如-

```c
tmp = malloc(sizeof(struct node));
tmp->info = data;
tmp->link = NULL;
```

如果列表为空并且我们正在插入第一个元素，则必须将指针 start 初始化为-

```c
if ( start == NULL ) /*If list is empty */
    start = tmp;
```

之后我们将继续在列表末尾插入新节点。

现在我们有能力编写一个创建链表并对其执行操作的程序。每个操作都已在单独的函数中实现。指针 start 被设为全局，以便所有函数都可以访问它，并且使我们的程序简单。如果我们在 main() 中声明 start，则必须将其传递给所有其他函数，并在这些函数中使用指向指针的指针。

```c
/*P10.15 Program of single linked list*/
#include <stdio.h>
#include <malloc.h>
struct node
{
    int info;
    struct node *link;
}*start;
main()
{
    int choice,n,m,position,i;
    while(1)
    {
        printf("1.Create List\n");
        printf("2.Add at beginning\n");
        printf("3.Add after \n");
        printf("4.Delete\n");
        printf("5.Display\n");
        printf("6.Search\n");
        printf("7.Quit\n");
        printf("Enter your choice : ");
        scanf("%d",&choice);
        switch(choice)
        {
            case 1:
                start=NULL;
                printf("How many nodes you want : ");
                scanf("%d",&n);
                for(i=0;i<n;i++)
                {
                    printf("Enter the element : ");
                    scanf("%d",&m);
                    create_list(m);
                }
                break;
            case 2:
                printf("Enter the element : ");
                scanf("%d",&m);
                addatbeg(m);
                break;
            case 3:
```
