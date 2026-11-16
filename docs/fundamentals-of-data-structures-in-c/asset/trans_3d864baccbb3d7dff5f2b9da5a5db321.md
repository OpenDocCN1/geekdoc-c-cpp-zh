
## 3.4.1 入队操作

入队操作是用于在队列尾部添加新元素的操作。在实现入队操作时，需要检查队列的溢出条件。（因为如果尾部位于队列的最后一个位置，则无法插入任何数据）。

以下过程可帮助您更好地理解。

- 创建一个带有两个参数的函数 ENQUEUE(，即数组和要添加的元素。
- 通过递增 REAR 变量在数组中分配新元素。

## 3.4.2 出队操作

出队操作是用于从队列前端移除元素的操作。在实现出队操作时，需要检查队列的下溢条件（即，您需要检查队列是否为空）。用户不应从空队列中删除元素。此类尝试是非法的，应予以避免。如果进行此类尝试，应向用户通知下溢条件。

以下过程可帮助您更好地理解。

- 创建一个带有两个参数的函数 DEQUEUE(，即数组和用于存储出队值的元素地址。
- 将 FRONT 变量递增 1。

## 3.4.3 窥视操作

窥视操作是用于显示队列前端元素的操作，该元素由 FRONT 指针指向，但不实际移除它。队列的窥视操作使用数组实现。在实现窥视操作时，需要检查队列的下溢条件（即，您需要检查队列是否为空）。用户不应尝试从空队列中窥视元素。此类尝试是非法的，应予以避免。如果进行此类尝试，应向用户通知下溢条件。以下过程可帮助您更好地理解。

- 创建一个带有一个参数的函数 PEEK(，即用于存储前端值的元素地址。

## 3.4.4 空队列

如果队列不包含任何元素，则称为空队列。如果要从队列中出队一个元素，您需要检查队列是否为空，因为不能从空队列中出队元素。以下过程可用于创建和检查空队列。

- 创建一个不带参数的函数 ISEMPTY(。
- 检查 FRONT 指针和 REAR 指针是否等于 -1。
- 如果条件为真，则表示队列为空。
- 否则，队列不为空。

## 3.4.5 完全占用队列

如果队列包含的元素数等于其大小（即 QSIZE），则我们说队列已满。如果要向队列中插入元素，您需要检查队列是否已满，因为当队列完全占用时无法向其中插入元素。此类尝试是非法的，应予以避免。如果进行此类尝试，应向用户通知溢出条件。

要检查队列是否已满，我们在程序 3.1 中使用了指针 REAR。我们正在检查指针 REAR 是否等于数组的最大大小减一（因为数组从零开始，如果数组大小为 5，且队列已满，则队列的最后一个元素存储在数组位置 4）。如果满足条件，将显示输出消息“Queue Overflow on ENQUEUE”。此条件称为完全占用队列。以下过程可帮助您更好地理解。

- 创建一个不带参数的函数 isFull()。
- 检查 REAR 指针是否等于 QSIZE – 1。
- 如果条件为真，则表示队列已满。否则，队列未满。

## 程序 3.2 :

```c
/* Program to implement a linear queue using arrays */
/* lqueue.c */
#define QSIZE 4										/* Maximum size of the Queue */
void displayMenu();
int isEmpty();
int isFull();
int size();
int enqueue(int value);
int dequeue(int *value);
int peek(int *value);
void view();
int queue[QSIZE], front = -1, rear = -1;
void main()
{
	int status, choice, data;
	displayMenu() ;
	while(1)
	{
		printf("\n ? ");
		scanf("%d", &choice);
		switch(choice)
		{
		    case 1 :
		        printf("Enter the element : ");
		        fflush(stdin);
		        scanf("%d", &data);
		        status = enqueue(data);
		        if(status == -1)
		            printf("Queue Overflow on ENQUEUE...");
		        break;
		    case 2 :
		        status = dequeue(&data);
		        if(status == -1)
		            printf("Queue Underflow on DEQUEUE ...");
		        else
		            printf("The Dequeued Value is %d", data);
		        break;
		    case 3 :
		        status = peek(&data);
		        if(status == -1)
		            printf("\n Queue is Empty");
		        else
		            printf("\n The Top most value is %d", data);
		        break;
		    case 4 :
		        printf("\n Queue Size is %d", QSIZE);
		        printf("\n Current Queue Elements = %d", size());
		        break;
		    case 5 :
		        view();
		        break;
		    default:
		        printf("\n End of Run of your Program . . ");
		        exit(0);
		    }
	}
}
void displayMenu()
{
 printf("\n Representation of Linear Queue using Arrays ...");
 printf("\n\t 1. Enqueue ");
 printf("\n\t 2. Dequeue ");
 printf("\n\t 3. Peek ");
 printf("\n\t 4. Size ");
 printf("\n\t 5. View ");
 printf("\n\t 6. Exit ");
}
int isEmpty()
{
 extern int queue[], front, rear;
 if(front == -1 && rear == -1)
 /* Check for Empty Queue */
 return 1;
 else
 return 0;
}
int isFull()
{
 extern int queue[], front, rear;
 if(rear == (QSIZE - 1))
 /* Check for Occupied Queue */
 return 1;
 else
 return 0;
}
int enqueue(int value)
{
 extern int queue[], front, rear;
 if(isFull())
 /* Check for Rear at last position */
 return -1;
 else if(isEmpty())
 /* Check for Empty Queue */
 front = rear = 0;
 else
 rear = rear + 1;
 queue[rear] = value;
 return 0;
}
int dequeue(int *value)
{
 extern int queue[], front, rear;
 if(isEmpty())
 {
     return -1;
 }
 *value = queue[front];
 /*Check for Queue contains only one element*/
 if(front == rear)
     front = rear = -1;
 else
     front = front + 1;
 return 0;
}

int peek(int *value)
{
    extern int queue[], front, rear;
    if(isEmpty())
    /* Check for Empty Queue */
    return -1;
    *value = queue[front];
    return 0;
}

int size()
{
    extern int queue[], front, rear;
    return (rear - front + 1);
}

void view()
{
    extern int queue[], front, rear;
    int f;
    if(isEmpty())
    {
        printf("Queue is EMPTY !!!");
        return;
    }
    printf("\nContent of the Queue is ... \n FRONT -->");
    for(f = front; f != rear+1; f = f + 1)
    {
        printf(" %d --> ", queue[f]);
    }
    printf(" REAR");
    if(isFull())
        printf("\n Queue is FULL");
}
```

## 程序显示以下输出

使用数组表示线性队列 ...
1. 入队
2. 出队
3. 窥视
4. 大小
5. 查看
6. 退出

```c
? 2
Queue Underflow on DEQUEUE ...
? 3
Queue is Empty
? 4
Queue Size is = 5
Current Queue Elements = 1
? 5
Queue is EMPTY !!!
? 1
Enter the element : 1001
? 1
Enter the element : 1002
? 1
Enter the element : 1003
? 1
Enter the element : 1004
? 1
Enter the element : 1005
Queue Overflow on ENQUEUE...
? 5
Content of the Queue is ...
FRONT -> 1001 -> 1002 -> 1003 -> 1004 -> REAR
Queue is FULL
? 4
Queue Size is = 4
Current Queue Elements = 4
? 3
The Top most value is 1001
? 2
The Dequeued Value is 1001
? 2
The Dequeued Value is 1002
? 5
Content of the Queue is ...
FRONT -> 1003 -> 1004 -> REAR
? 4
Queue Size is = 4
Current Queue Elements = 2
? 2
The Dequeued Value is 1003
? 2
The Dequeued Value is 1004
? 2
Queue Underflow on DEQUEUE ...
? 5
Queue is EMPTY !!!
? 6
End of Run of your Program . . .
```

## 3.5 链表

链表或列表是元素的有序集合。列表中的每个元素称为节点。每个节点包含两个字段，即，

- 数据字段
- 链接字段。

数据字段包含要存储在列表中的元素的实际数据（即，值），链接字段也称为下一个地址字段，包含列表中下一个节点的地址。图 3.6 可帮助您更好地理解。

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_173_0.png)

图 3.6：链表表示。

图 3.6 所示的链表包含三个节点，每个节点都有一个数据字段和一个链接字段。链表包含一个指针，称为头指针，它指向列表中的第一个节点，该节点存储列表中第一个节点的地址（即，FB12）。数据字段包含要
