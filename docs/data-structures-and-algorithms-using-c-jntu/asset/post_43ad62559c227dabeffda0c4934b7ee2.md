
## 7.4.1 OPERATIONS ON CIRCULAR QUEUE

All the operations performed on the queue can also be performed on a circular queue. Algorithms INSERTION-CQ and DELETION-CQ describe the insertion and deletion operations in the circular queue. The array implementation of a circular queue is declared as CIR-QUE[0, N-1] to provide circular movement of FRONT and REAR pointers.

```
Algorithm 7.5: INSERT-CQ(CIR-QUE,FRONT,REAR,N,ITEM)
//ITEM is the ITEM to be inserted. CIR-QUE is array representation of
//circular queue. FRONT and //REAR are pointers and N is the size of array.
1. If (FRONT = 0) then
2. Set FRONT to 1
3. Set REAR to 1
4. Set CIR-QUE[REAR] to ITEM
5. Else
6. Set REAR = (REAR + 1) mod N
7. If (FRONT = REAR) then // circular queue is full
   Write "circular queue is logically full"
8. Set CIR-QUE[REAR] to ITEM
9. End.
```

```
Algorithm 7.6: DELETE-CQ(CIR-QUE,FRONT,REAR,N,ITEM)
1. If (FRONT = 0) then
   Write "Queue is empty"
2. Else
3. Set FRONT = (FRONT + 1) mod N // UPDATE FRONT
4. Set ITEM to the FRONT ELEMENT
5. End.
```

The following example explains the working of a circular queue

Initially the circular queue is empty:

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| FRONT=0 REAR=0 | | | | | |

Insert 10, 20, 30 elements:

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| FRONT=1 REAR=3 | 10 | 20 | 30 | | |

Delete element 10:

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| FRONT=2 REAR=3 | | 20 | 30 | | |

Insert 40, 50 elements:

FRONT=2
REAR=5

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| | | 20 | 30 | 40 | 50 |

Delete 20, 30 elements:

FRONT=4
REAR=5

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| | | | | 40 | 50 |

Insert element 60:

FRONT=4
REAR=1

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| | 60 | | | 40 | 50 |

Delete element 40:

FRONT=5
REAR=1

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| | 60 | | | | 50 |

Insert 70, 80, 90 elements:

FRONT=5
REAR=5

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| | 60 | 70 | 80 | 90 | 50 |

Inserting any element at this stage fails because the circular queue is full.

Delete element 50:

FRONT=1
REAR=4

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| | 60 | 70 | 80 | 90 | |

Delete element 60:

FRONT=2
REAR=4

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| | | 70 | 80 | 90 | |

Delete 70, 80 elements:

FRONT=4
REAR=4

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| | | | | 90 | |

Delete element 90:

FRONT=0
REAR=0

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| | | | | | |

Circular queue is empty

## Program 7.3

```
// Array implementation of Circular Queue
#include<iostream.h>
#include<conio.h>
#include<stdlib.h>
template<class t>
class queue
{
int rear,front,n;
t a[50];
public:
queue(int m)
{
rear=front=-1;
n=m;
}
void push();
void pop();
void display();
};
template<class t>
void queue<t>::push()
{
t ele;
if(front==(rear+1)%n)
{
cout<<"queue is overflow\n";
return;
}
cout<<"enter the element \n";
cin>>ele;
if(front==-1)
rear=front=0;
else
rear=(rear+1)%n;
a[rear]=ele;
}
template<class t>
void queue<t>::pop()
{
t ele;
if(rear==-1)
{
cout<<"queue is underflow\n";
return;
}
ele=a[front];
if(rear==front)
rear=front=-1;
else
front=(front+1)%n;
cout<<"the deleted element is "<<ele;
}
template<class t>
void queue<t>::display()
{
int i;
if(rear==-1)
{
cout<<"queue is underflow\n";
return;
}
if(front<=rear)
{
for(i=front;i<=rear;i++)
cout<<a[i]<<" ";
}
else
{
for(i=front;i<n;i++)
cout<<a[i]<<" ";
for(i=0;i<=rear;i++)
cout<<a[i]<<" ";
}
cout<<"\n";
}
void main()
{
int ch,n;
clrscr();
cout<<"enter the size of the queue\n";
cin>>n;
queue<char>q(n);
while(1)
{
cout<<"\nmenu\n";
cout<<"1.push\n";
cout<<"2.pop\n";
cout<<"3.display\n";
cout<<"4.exit\n";
cout<<"enter your choice\n";
cin>>ch;
switch(ch)
{
case 1:
q.push();
break;
case 2:
q.pop();
break;
case 3:
q.display();
break;
case 4:
exit(0);
break;
default:
cout<<"invalid option\n";
break;
}
}
}
```

## Output

enter the size of the queue
10
menu
1.push
2.pop
3.display
4.exit
enter your choice
1
enter the element
2
menu
1.push
2.pop
3.display
4.exit
enter your choice
1
enter the element
3
menu
1.push
2.pop
3.display
4.exit
enter your choice
3
2 3
menu
1.push
2.pop
3.display
4.exit
enter your choice
2
the deleted element is 2
menu
1.push
2.pop
3.display
4.exit
enter your choice
4

## Program 7.4

```
// Linked list implementation of Circular queue
#include<iostream.h>
#include<conio.h>
#include<stdlib.h>
#include<alloc.h>
template<class t>
class queue
{
    struct node
    {
        t data;
        node*link;
    }*head,*temp,*front,*rear;
public:
    queue();
    void push();
    void pop();
    void display();
};
template<class t>
queue<t>::queue()
{
    head->link=NULL;
    rear=NULL;
    front=NULL;
}
template<class t>
void queue<t>::push()
{
    t ele;
    cout<<"enter the element\n";
    cin>>ele;
    temp=(struct node*) malloc(sizeof(struct node)) ;
    if(temp==NULL)
    {
        cout<<"memory allocation error\n";
        return;
    }
    if(front==NULL)
    {
        temp->data=ele;
        head->link=temp;
        temp->link=NULL;
        front=rear=temp;
    }
    else
    {
        temp->data=ele;
        rear->link=temp;
        temp->link=front;
        rear=temp;
    }
}
template<class t>
void queue<t>::pop()
{
    t ele;
    if(front==NULL)
    {
        cout<<"linked list is empty\n";
        return;
    }
    if(front==rear)
    {
        ele=front->data;
        front=rear=NULL;
    }
    else
    {
        ele=front->data;
        rear->link=front->link;
        temp=front;
        front=front->link;
        free(temp);
    }
    cout<<"the deleted element is "<<ele<<endl;
}
template<class t>
void queue<t>::display()
{
    if(rear==NULL)
    {
        cout<<"linked list is empty\n";
        return;
    }
    for(temp=front;temp!=rear;temp=temp->link)
    {
        cout<<temp->data<<" ";
    }
    cout<<temp->data<<" ";
}

void main()
{
    int ch;
    queue<int>q;
    clrscr();
    while(1)
    {
        cout<<"\nmenu\n";
        cout<<"1.push\n";
        cout<<"2.pop\n";
        cout<<"3.display\n";
        cout<<"4.exit\n";
        cout<<"enter your choice\n";
        cin>>ch;
        switch(ch)
        {
            case 1:
            q.push();
            break;
            case 2:
            q.pop();
            break;
            case 3:
            q.display();
            break;
            case 4:
            exit(0);
            break;
        }
    }
}
```

## Output

```
menu
1.push
2.pop
3.display
4.exit
enter your choice
1
enter the element
2
menu
1.push
2.pop
3.display
4.exit
enter your choice
1
enter the element
3
menu
1.push
2.pop
3.display
4.exit
enter your choice
3
2 3
menu
1.push
2.pop
3.display
4.exit
enter your choice
2
the deleted element is 2
menu
1.push
2.pop
3.display
4.exit
enter your choice
4
```

## 7.5 DEQUE

Another type of queue is deque, which is pronounced as "deck" or "deque". In deque, insertion and deletion operations can be performed on both sides of the queue. The term deque has emerged from double-ended queue. Figure 7.7 resembles the deque.

### Figure 7.7 Deque

![](img/45784b9f0334626143002ec0d63692fd_242_0.png)

Figure 7.8 illustrates that a deque is the general form of both stack and queue representation, i.e. the deque can be used as a stack or a queue.

### Figure 7.8 Comparison of stack, queue, deque

![](img/45784b9f0334626143002ec0d63692fd_242_1.png)

![](img/45784b9f0334626143002ec0d63692fd_242_2.png)

![](img/45784b9f0334626143002ec0d63692fd_242_3.png)

Deque's are of two types input restricted deque and output restricted deque. When insertion of elements into the deque is restricted to only one end and deletion can be done in both directions, such a deque is called input restricted deque. In an output restricted deque, insertion of elements can be done in both directions, but deletions can be done at only one end. Commonly deques are implemented using circular arrays. Figure 7.9 shows the different types of deques.

### Figure 7.9 Types of deques

![](img/45784b9f0334626143002ec0d63692fd_242_4.png)

![](img/45784b9f0334626143002ec0d63692fd_242_5.png)
