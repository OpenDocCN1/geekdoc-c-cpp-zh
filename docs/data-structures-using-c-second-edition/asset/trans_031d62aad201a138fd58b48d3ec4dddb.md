

## 删除操作

删除操作用于删除队列中最先插入的元素，即存储在 FRONT 中地址的元素。但是，在删除值之前，我们必须首先检查 FRONT=NULL 是否成立，因为如果是这种情况，则队列为空，无法再进行删除操作。如果尝试从已经为空的队列中删除值，将打印下溢消息。请考虑图 8.10 所示的队列。

![](img/be6359df08208122bec6fad1103de211_271_0.png)

![](img/be6359df08208122bec6fad1103de211_271_1.png)

要删除一个元素，我们首先检查 FRONT=NULL。如果条件为假，则删除 FRONT 指向的第一个节点。FRONT 现在将指向链式队列的第二个元素。因此，更新后的队列变为图 8.11 所示。

![](img/be6359df08208122bec6fad1103de211_271_2.png)

图 8.12 显示了从链式队列中删除元素的算法。在第 1 步中，我们首先检查下溢条件。如果条件为真，则显示相应的消息，否则在第 2 步中，我们使用指向 FRONT 的指针 PTR。在第 3 步中，FRONT 被设置为指向序列中的下一个节点。在第 4 步中，PTR 占用的内存被返还给空闲池。

## 编程示例

- 2. 编写一个程序以实现链式队列。

```c
#include <stdio.h>
#include <conio.h>
#include <malloc.h>
struct node
{
    int data;
    struct node *next;
};
struct queue
{
    struct node *front;
    struct node *rear;
};
struct queue *q;
void create_queue(struct queue *);
struct queue *insert(struct queue *,int);
struct queue *delete_element(struct queue *);
struct queue *display(struct queue *);
int peek(struct queue *);
int main()
{
    int val, option;
    create_queue(q);
    clrscr();
    do
    {
        printf("\n *****MAIN MENU*****");
        printf("\n 1. INSERT");
        printf("\n 2. DELETE");
        printf("\n 3. PEEK");
        printf("\n 4. DISPLAY");
        printf("\n 5. EXIT");
        printf("\n Enter your option : ");
        scanf("%d", &option);
        switch(option)
        {
        case 1:
            printf("\n Enter the number to insert in the queue:");
            scanf("%d", &val);
            insert(q,val);
            break;
        case 2:
            q = delete_element(q);
            break;
        case 3:
            val = peek(q);
            if(val != -1)
                printf("\n The value at front of queue is : %d", val);
            break;
        case 4:
            q = display(q);
            break;
        }
    }while(option != 5);
    getch();
    return 0;
}
```

```c
void create_queue(struct queue *q)
{
    q->rear = NULL;
    q->front = NULL;
}
```

```c
struct queue *insert(struct queue *q,int val)
{
    struct node *ptr;
    ptr = (struct node*)malloc(sizeof(struct node));
    ptr->data = val;
    if(front == NULL)
    {
        q->front = ptr;
        q->rear = ptr;
        q->front->next = q->rear->next = NULL;
    }
    else
    {
        q->rear->next = ptr;
        q->rear = ptr;
        q->rear->next = NULL;
    }
    return q;
}
```

```c
struct queue *display(struct queue *q)
{
    struct node *ptr;
    ptr = q->front;
    if(ptr == NULL)
        printf("\n QUEUE IS EMPTY");
    else
    {
        printf("\n");
        while(ptr != q->rear)
        {
            printf("%d\t", ptr->data);
            ptr = ptr->next;
        }
        printf("%d\t", ptr->data);
        return q;
    }
}
```

```c
struct queue *delete_element(struct queue *q)
{
    struct node *ptr;
    ptr = q->front;
    if(q->front == NULL)
    {
        printf("\n UNDERFLOW");
    }
    else
    {
        q->front = q->front->next;
        printf("\n The value being deleted is : %d", ptr->data);
        free(ptr);
    }
    return q;
}
int peek(struct queue *q)
{
    if(q->front == NULL)
    {
        printf("\n QUEUE IS EMPTY");
        return -1;
    }
    else
        return q->front->data;
}
```

**输出**
******主菜单******
1. 插入
2. 删除
3. 查看
4. 显示
5. 退出
请输入您的选项：3
队列为空
请输入您的选项：5

## 8.4 队列的类型

队列数据结构可以分为以下几种类型：
- 1. 循环队列
- 2. 双端队列
- 3. 优先队列
- 4. 多重队列

我们将在以下各节中详细讨论每种队列。

### 8.4.1 循环队列

在迄今讨论的线性队列中，插入操作只能在称为 rear 的一端进行，删除操作总是从称为 front 的另一端进行。请看图 8.13 所示的队列。

| 54 | 9 | 7 | 18 | 14 | 36 | 45 | 21 | 99 | 72 |
|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

图 8.13 线性队列

这里，FRONT = 0 且 REAR = 9。

现在，如果您想插入另一个值，将不可能实现，因为队列已完全填满。没有空位可插入该值。考虑进行两次连续删除的场景。队列将如图 8.14 所示。

| 0 | 1 | 7 | 18 | 14 | 36 | 45 | 21 | 99 | 72 |
|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

图 8.14 两次连续删除后的队列

这里，FRONT = 2 且 REAR = 9。

假设我们想在图 8.14 所示的队列中插入一个新元素。尽管有可用空间，上溢条件仍然存在，因为条件 REAR = MAX - 1 仍然成立。这是线性队列的一个主要缺点。

![](img/be6359df08208122bec6fad1103de211_274_0.png)

图 8.15 循环队列

为解决此问题，我们有两种方案。首先，将元素向左移动，以便占用并高效利用空闲空间。但这可能非常耗时，尤其是当队列相当大时。第二种选择是使用循环队列。在循环队列中，第一个索引紧随最后一个索引之后。概念上，您可以将循环队列视为图 8.15 所示。

循环队列仅在 FRONT = 0 且 REAR = Max - 1 时才会填满。循环队列的实现方式与线性队列相同。唯一的区别在于执行插入和删除操作的代码。对于插入，我们现在需要检查以下三个条件：

| 90 | 49 | 7 | 18 | 14 | 36 | 45 | 21 | 99 | 72 |
|---|---|---|---|---|---|---|---|---|---|
| FRONT = 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | REAR = 9 |

图 8.16 已填满的队列

将 rear 递增，使其指向位置 9，并在此处插入值。

- 如果 FRONT = 0 且 REAR = MAX - 1，则循环队列已满。请看图 8.16 所示的队列，这说明了这一点。

| 90 | 49 | 7 | 18 | 14 | 36 | 45 | 21 | 99 | 72 |
|---|---|---|---|---|---|---|---|---|---|
| FRONT = 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | REAR = 8 | 9 |

图 8.17 带有空闲位置的队列

将 REAR = 0 并在此处插入值。

- 如果 REAR != MAX - 1，则将递增 REAR 并插入值，如图 8.17 所示。

| 7 | 18 | 14 | 36 | 45 | 21 | 80 | 81 |
|---|---|---|---|---|---|---|---|
| 0 | 1 FRONT = 2 | 3 | 4 | 5 | 6 | 7 | 8 REAR = 9 |

图 8.18 在循环队列中插入元素

- 如果 FRONT != 0 且 REAR = MAX - 1，则意味着队列未满。因此，将 REAR = 0 并在此处插入新元素，如图 8.18 所示。

让我们看看图 8.19，它显示了在循环队列中插入元素的算法。在第 1 步中，我们检查上溢条件。在第 2 步中，我们进行两次检查。首先检查队列是否为空，其次检查 rear 端是否已达到最大容量，而 front 端之前存在某些空闲位置。在第 3 步中，值被存储在 REAR 指向的位置的队列中。

```
Step 1: IF FRONT = 0 and Rear = MAX - 1
    write "OVERFLOW"
    Goto step 4
Step 2: IF FRONT = -1
    FRONT = 0 and REAR = 0
ELSE IF REAR = MAX - 1 and FRONT != 0
    SET REAR = 0
ELSE
    SET REAR = REAR + 1
[END OF IF]
Step 3: SET QUEUE[REAR] = VAL
Step 4: EXIT
```

图 8.19 在循环队列中插入元素的算法

在了解如何在循环队列中添加新元素后，让我们现在讨论在这种情况下如何执行删除操作。要删除一个元素，我们同样需要检查三个条件。

