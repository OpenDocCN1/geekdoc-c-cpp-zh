

- 在链表的末尾，或
- 在链表的开头/前端

![](img/9b7c80a1312a664ae505ba138aa3306b_61_0.png)

从末尾插入时，新节点被放置在现有链表的末尾。例如，在已有节点 10 的链表中插入值为 20 的节点，如下图所示。这里，20 将被放置在 10 之后，并且指针将被适当地调整。插入 20 之后，假设我们必须在现有链表中插入 30。图 3.3(b) 中展示了相同的情况。这被称为链表的后向增长，因为新节点被附加在末尾。

类似地，我们可以创建一个前向增长的链表。在前向链表中，新节点被插入到开头，而不是末尾。图 3.4 中展示了相同的情况。考虑图 3.4 的情况。在这种情况下，已经存在一个值为 5 的节点。创建值为 10 的新节点；相应地，它将被插入到现有链表的开头。类似地，新到达的节点是 20。它将被放置在 10 的开头（参见图 3.4）。这种链表增长类型被称为前向增长链表。

![](img/9b7c80a1312a664ae505ba138aa3306b_61_1.png)

## B. 显示节点

一旦链表创建完成，无论是前向增长还是后向增长，我们都希望查看链表中各个节点保存的数据。为了显示节点元素，我们从开头即第一个节点开始，并持续向末尾节点移动。最后一个节点的 next 指针指向 NULL，可用于停止遍历。遍历的逻辑已在下面的程序中描述：

![](img/9b7c80a1312a664ae505ba138aa3306b_62_0.png)

```
dnode *current;
current=first      //initialize with the first pointer
while (current!=NULL)  // moving upto the end of a list
{
cout<<"current->info"<<current->info; //displaying info part
current=current->next; //move to the next node
}
```

创建和显示链表的完整程序如下所示：

```
Program1: Create and display the node of a list. In the program, node is to be inserted from the end.
// class to define the structure of a node
class node
{
public:
int info;
node *next;
};
// class of a link list
class list
{
node *first, *end;      // creation of first and end pointer
public:
// Defining constructor for the list
list()
{
```

```
{
    cout<<current->data<<" -> ";
    current=current->next;
}
```

## C. 通过在开头插入来创建链表

链表也可以通过将元素插入到开头来创建。被附加的新节点成为链表的第一个节点。例如，如果要为序列 10、20、30、5、9、100 创建链表，那么链表将如图 3.5 所示增长。

![](img/9b7c80a1312a664ae505ba138aa3306b_64_0.png)

一旦新节点被创建，它将被连接到已有链表的第一个节点，因此现有的第一个节点将移动到第二个位置。因此，新节点应该成为第一个节点。在链表中插入节点的完整程序如下所示：

```
//function to create the list from the beginning
void list::create_beg(int el)
{
    node *current,*temp;
    // if the list does not exist
    if(first==NULL)
    {
        first=new node;
        first->data=el;
        first->next=NULL;
        end=first;
```

```
return;
}
// If the link list exist then program will start from here
current=new node;
current->data=el;
current->next=first; //link current to first
first=current; // make the current node as first node
} //end of create_beg
```

## 3.3 在现有链表中插入节点

在现有链表中，节点可以按用户的意图插入到任何位置。然而，从程序的角度来看，我们需要考虑两种情况，它们将涵盖所有插入位置。这些情况可以是：

- 第一个位置
- 除第一个位置以外的其他位置

所有这些情况及其连接方法将在以下小节中描述。

### 3.3.1 在第一个位置插入

考虑如图 3.6 所示的链表。在这个链表中，一个新节点将被放置（插入）在开头。为了实现这个目标，首先我们必须创建新节点，并将这个新节点附加到现有第一个节点之前。此操作如图 3.6 所示。

![](img/9b7c80a1312a664ae505ba138aa3306b_65_0.png)

由于在开头插入了新节点，现有第一个节点的状态将改变。因为第一个节点将变成第二个节点，而新节点将成为第一个节点。因此，first 指针必须移动到新节点。完整的操作顺序描述如下：

## 在第一个位置插入的方法

要在第一个位置插入节点，需要遵循以下顺序。

- 创建新节点
- 将其链接到第一个节点
- 将 first 节点的位置改为这个新节点。
- 返回这个新第一个节点的指针

![](img/9b7c80a1312a664ae505ba138aa3306b_66_0.png)

假设链表包含的项目为：50、10、20、30。要插入的新元素是“70”。现在第一个节点移动到第二个节点，新节点成为第一个节点。结果链表如图 3.5 所示。代码如下：

```
newnode=new node;
newnode->data=el;
newnode->next=first;
first=newnode;
```

### 3.3.2 在非第一个位置插入节点

为了在中间插入节点，我们将确定新节点将要插入的两个节点。

![](img/9b7c80a1312a664ae505ba138aa3306b_66_1.png)

位于这个节点之前的节点将被称为前一个节点（previous node），位于这个节点之后的节点将被称为后一个节点（forward node）。在我们的程序中，我们将后一个节点命名为当前节点（current node）。图 3.6 中展示了相同的情况。

在现有链表中，前一个节点的指针需要连接到新节点，而新节点的指针需要连接到当前节点。

```
prev->next=newnode;
newnode->next=current;
```

在链表中插入节点的完整方法已在 insert 函数中描述。在讨论的函数中，我们接受作为参数传递的位置，并将其与该特定时刻链表包含的节点数进行比较。用户想要的位置不应超过现有链表大小（节点数）加 1。例如，如果节点总数为 n，那么提供的位置不应超过 n+1。

```
Program: Insert the node at any position in a list
Solution

//function to insert at particular position
void list::insert(int el, int pos)
{
node *current,*newnode,*prev=NULL;
int cnt=count();//count number of nodes
if(pos<=cnt+1)
{
current=first;
// Create a new node
newnode=new node;
newnode->data=el;
newnode->next=NULL;
int i=1;
//moving to the appropriate position
while(i<pos)
{
prev=current;
current=current->next;
i++;
}//end of while
```

```
if(prev==NULL)// to be inserted at first position
{
    newnode->next=first;
    first=newnode;
    return;
} //end of inner if
// if node is to be inserted is other than the first node
newnode->next=current;
    prev->next=newnode;
}  //end of outer if
else
cout<<"Size less than position, Try again-..\n";
}//end of function
```

上述程序非常适合在最后一个位置插入。因为当在最后一个位置插入时，涉及将新节点放置在末尾，在此之前需要将现有最后一个节点与新节点连接。新节点的插入如图 3.7 所示。

为中间位置编写的代码也支持在最后一个位置插入节点。

```
prev->next=newnode;      (1)
newnode->next=current    (2)
```

然而，prev 节点将指向最后一个节点，而 current 将指向 NULL。由于代码 (1) 将把最后一个节点连接到新节点，因此一个目标将完成。而代码 (2) 将把新节点连接到当前节点，而当前节点已经为 NULL，如图 3.7 所示。因此，该代码适用于在除第一个位置之外的任何位置插入节点。

### 3.3.3 删除链表中的节点

链表持有数据的方式与其他类型类似，区别在于它是动态的。链表中存储的数据可能不再需要。这导致需要对链表进行另一种称为删除的操作。由于链表是借助指针连接的，因此需要格外小心，以确保即使在删除一个或多个节点之后链表仍然保持连接。在删除节点期间，需要考虑以下与位置相关的可能性。

- 删除第一个节点。
- 删除除第一个节点以外的其他节点。

