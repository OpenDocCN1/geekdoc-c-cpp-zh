

```c
node->next = (struct link*) malloc(sizeof(struct link)); /* Create header node */
i = 0;
while (ch == 'Y' || ch == 'y')
{
    node->next = (struct link*) malloc(sizeof(struct link));
    node = node->next;
    printf("\nENTER THE NUMBER");
    scanf("%d", &node->info);
    node->next = NULL;
    fflush(stdin);
    printf("\nDO YOU WANT TO CREATE MORE NODES[Y/N]");
    scanf("%c", &ch);
    i++;
}
printf("\n NUMBER OF NODES = %d", i);
node->info = i; /* ASSIGN TOTAL NUMBER OF NODES INTO THE HEADER LIST */
}

void insert(struct link *node)
{
    int n = 1;
    int no, count;
    node = start;
    count = node->info;
    node = node->next;
    printf("\nENTER THE NODE NUMBER TO INSERT");
    fflush(stdin);
    scanf("%d", &no);
    while (count)
    {
        if (n == no)
        {
            new = (struct link*) malloc(sizeof(struct link));
            new->next = node->next;
            node->next = new;
            printf("\nENTER THE VALUE");
            fflush(stdin);
            scanf("%d", &new->info);
            node = node->next;
        }
        else
        {
            node = node->next;
            count--;
            n++;
        }
    }
    node = start;
    node->info = node->info + 1;
}
void display(struct link *node)
{
    int count;
    node = start;
    count = node->info;
    node = node->next;
    printf("\n THE LINKED LIST IS \n");
    while (count)
    {
        printf("%d", node->info);
        node = node->next;
        count--;
    }
}
void main()
{
    struct link *node;
    clrscr();
    create(node);
    display(node);
    insert(node);
    display(node);
}
```

## 7.8 循环链表

正如名称所指定，这种链表形成一个圆圈。这意味着列表的最后一个节点将连接到链表的开头。这可以分为

- 单向循环链表
- 双向循环链表
- 示例

![](img/1faaa0256577c74e8a61f42967760aa8_242_0.png)

### 循环链表的优点：

- 1) 任何节点都可以作为起点。我们可以从任意点开始遍历整个列表。只需在第一个访问的节点再次被访问时停止即可。
- 2) 有助于队列的实现。与这种实现不同，如果使用循环链表，我们不需要维护两个指针来指向队首和队尾。我们可以维护一个指向最后插入节点的指针，队首始终可以通过最后一个节点的 next 获得。
- 3) 循环列表在需要反复遍历列表的应用中很有用。例如，当 PC 上运行多个应用程序时，操作系统通常将运行中的应用程序放入一个列表，然后循环遍历它们，给每个应用程序分配一段时间片执行，然后让它们等待，而将 CPU 分配给另一个应用程序。操作系统使用循环列表很方便，这样当它到达列表末尾时，可以循环回到列表的开头。
- 4) 循环双向链表用于实现斐波那契堆等高级数据结构。

### 创建循环头节点链表

```c
#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
struct link
{
    int info;
    struct link *next;
};
int i; /* Represents number of nodes in the list */
int number = 0;
struct link *start, *node, *new1;
void create()
{
    char ch;
    node = start; /* Point to the header node in the list */
    i = 0;
    do
    {
        node->next = (struct link*) malloc(sizeof(struct link));
        node = node->next;
        printf("\n Input the node : %d.", (i + 1));
        scanf("%d", &node->info);
        fflush(stdin);
        printf("\n DO YOU WANT TO CREATE MORE[Y/N] ");
        ch = getchar();
        i++;
    } while (ch == 'Y' || ch == 'y');
    node->next = start;
    start->info = i; /* Assign total number of nodes to the header node */
}
void insertion()
{
    struct link *first;
    first = start;
    node = start->next;
    int opt;
    int count = node->info;
    int node_number = 1;
    int insert_node;
    node = node->next;
    printf("\n Input node number you want to insert: ");
    printf("\n Value should be less than or equal to the");
    printf("\n number of nodes in the list: ");
    scanf("%d", &insert_node);
    while (count--)
    {
        if (node_number == insert_node)
        {
            new1 = (struct link*) malloc(sizeof(struct link));
            first->next = new1;
            new1->next = node;
            printf("\n Input the node value: ");
            scanf("%d", &new1->info);
            opt = 1;
            break;
        }
        else
        {
            node = node->next;
            first = first->next;
        }
        node_number++;
    }
    if (opt == 1)
    {
        node = start; /* Points to header node */
        node->info = node->info + 1;
    }
}

/* Display the list */
void display()
{
    node = start;
    int count = node->info;
    do
    {
        printf("\n%d ", node->info);
        node = node->next;
    } while (count--);
}

int main()
{
    create();
    printf("\n Before inserting a node list is as follows:\n");
    display();
    insertion();
    printf("\n After inserting a node list is as follows:\n");
    display();
}
```

## 7.9 链表的应用

- 1. 不同数据结构的表示：链式栈和队列、稀疏矩阵、树、图等...
- 2. 图的实现：图的邻接表表示最为流行，它使用链表存储相邻顶点。
- 3. 动态内存分配：我们使用空闲块的链表。
- 4. 维护名称目录
- 5. 对长整数进行算术运算
- 6. 通过在链表节点中存储常数来操作多项式

### 7.9.1 两个多项式的相加

```text
struct poly
{
    int coef, exp;
    struct poly *next;
};
SUM(P1, P2, P3)
STEP-1 : REPEAT WHILE ( P1 != NULL AND P2 != NULL)
 IF (DEGREE[P1] > DEGREE(P2)) THEN :
 ADD(P3, DEGREE[P1], COEF[P1])
 P1 := NEXT[P1]
 ELSE :
 IF (DEGREE[P1] < DEGREE(P2)) THEN :
 ADD(P3, DEGREE[P2], COEF[P2])
 P2 := NEXT[P2]
 ELSE :
 ADD(P3, DEGREE(P1), (COEF(P1) + COEF(P2)))
 P1 := NEXT[P1]
 P2 := NEXT[P2]
 [END OF IF]
 [END OF LOOP]
STEP-2 : IF (P1 = NULL)
 REPEAT WHILE ( P2 != NULL)
 ADD(P3, DEGREE(P2), COEF(P2))
 P2 := NEXT(P2)
 [END OF LOOP]
 [END OF IF]
STEP-3: IF (P2 = NULL)
 REPEAT WHILE (P1 != NULL)
 ADD(P3, DEGREE(P1), COEF(P1))
 P1 := NEXT(P1)
 [END OF LOOP]
 [END OF IF]
STEP-4: RETURN
```

### ADD(P3, COEF, EXP)

步骤 1：为 P3->NEXT 分配内存
步骤 2：P3 := NEXT[P3]
步骤 3：COEF[P3] := COEF
EXP[P3] := EXP
步骤 4：NEXT[P3] := NULL
步骤 5：返回

### 7.9.2 借助链表的多项式

```c
#include <stdio.h>
#include <alloc.h>
struct link
{
    int coef;
    int expo;
    struct link *next;
};
int i;
int number;
struct link *start, *previous, *new;
void create(struct link *node)
{
    char ch = 'y';
    start->next = NULL; /* Empty list */
    node = start; /* Point to the start of the list */
    i = 0;
    while (ch == 'y' || ch == 'Y')
    {
        node->next = (struct link*) malloc(sizeof(struct link));
        node = node->next;
        printf("\nENTER THE COEFFICIENT VALUE:");
        fflush(stdin);
        scanf("%d", &node->coef);
        printf("\nENTER THE EXPONENT VALUE:");
        fflush(stdin);
        scanf("%d", &node->expo);
        node->next = NULL;
        fflush(stdin);
        printf("\nDO YOU WANT TO CREATE MORE NODES[Y/N] ");
        scanf("%c", &ch);
        i++;
    }
    printf("\nNUMBER OF NODES = %d\n", i);
}

void display(struct link *node)
{
    node = start;
    node = node->next;
    printf("%d", node->coef); // PRINTING THE FIRST ELEMENT
    printf("%d", node->expo);
    node = node->next;
    while (node)
    {
        printf("+ %d", node->coef);
        printf("X^%d", node->expo);
        node = node->next;
    }
}

void main()
{
    struct link *node;
    create(node);
    display(node);
}
```

### 7.9.3 链式队列程序

```c
#include <stdio.h>
#include <iostream>
using namespace std;
struct Q
{
    int info;
    struct Q *next;
};
struct Q *front, *rear, *New;

void insert()
{
    New = (struct Q*) malloc(sizeof(struct Q));
    printf("\n Enter a number");
    scanf("%d", &New->info);
    New->next = NULL;
    if (front == NULL)
    {
        front = New;
        rear = New;
    }
    else
    {
        rear->next = New;
        rear = rear->next;
    }
}

void delete()
{
    if (front == NULL)
    {
        printf("\n QUEUE IS EMPTY");
        return;
    }
    New = front;
    if (New != NULL)
    {
        printf("%d IS DELETED", New->info);
        front = front->next;
        free(New);
    }
}

void display()
{
    New = front;
    if (New == NULL)
    {
        printf("\n QUEUE IS EMPTY");
        return;
    }
    printf("\n THE QUEUE IS ");
    while (New != NULL)
    {
        printf("%5d", New->info);
        New = New->next;
    }
}
```

