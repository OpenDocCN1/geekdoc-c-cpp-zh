

```cpp
current=current->next;
    i++;
}
temp->next=current;
temp->prev=current->prev;
current->prev->next=temp;
current->prev=temp;
//if the position is 1, change the first pointer
if(pos==1)
    first=temp;
}
}
else
cout<<" Cannot be inserted beyond the list length"<<endl;
}
```

## 4.9.5 从循环链表中删除一个节点

从循环双向链表中删除节点与双向链表有很大不同。在删除循环双向链表的第一个或最后一个节点时需要格外注意。如果要删除第一个节点，则 first 需要移动到现有 first 节点之后的一个节点。尽管删除了第一个节点，链表的循环特性仍需保留。因此，这个新的 first 必须连接到末尾节点。相应地，循环双向链表的最后一个节点也需要调整。最后一个节点即 End 节点的指针需要连接到双向链表的第一个节点。以下程序中已对此进行了描述。

```cpp
//To delete the node based on a user supplied value
    void dblyList::deletenode(int element)
    {
    dnode *current,*prev1=NULL,*temp;
    current=first;
    do{
        if( current->data==element)
        {
            break;
        }
        prev1=current;
```
```cpp
current=current->next;
}while(current!=first);
// if node to be deleted is first node
if(prev1==NULL)
{
temp=first;
current=first->next;
//connecting the new first to the last node
first->next->prev=first->prev;
end->next=current;
first=current;
}
// if node to be deleted is the last node
else if(current==end)
{
temp=current;
//Connecting the first node to the last node
first->prev=prev1;
// connecting the last node to the first node
prev1->next=first;
end=prev1;
}
// if the node to be deleted is the in-between node
else
{
temp=current;
prev1->next=current->next;
current->next->prev=prev1;
}
delete temp;
}
```

## 4.10 使用模板的双向链表

双向链表已进行了详细讨论，然而我们假设插入的数据为整数数据类型。如果我们需要为其他数据类型实现，则

程序需要相应修改。为解决这些情况，我们建议实现模板双向链表。此模板链表会根据要插入的类型进行修改。链表可以类似于使用指针实现的链表实现。仅由于模板形成才需要进行更改。完整的代码已如下所示，以便读者方便。

```cpp
//operations on double ended linked list
#include<iostream.h>
#include<conio.h>
template<class t>
class dnode
{
    public:
        t data;
        dnode *prev,*next;
};
template<class t>
class dlist
{
    dnode<t> *first,*last;
    public:
        //constructor to initialize the data member
        dlist();
        //to create the doubly link list
        void create(t);
        //to count the number of node
        int count();
        //to search element in doubly link list
        int search(t);
        //to insert the element at particular position
        void insert(int, t);
        //to reverse the doubly link list
        void reverse();
        //to concatenate the doubly link list
        dlist operator+(dlist);
```
```cpp
current->next->prev=current->prev;
first=current->next;
delete current;
break;
}
else
{
// any other node to be deleted
current->prev->next=current->next;
current->next->prev=current->prev;
delete current;
break;
}
}
current=current->next;
}
}

//function to create the doubly link list
template<class t>
void dlist<t>::create(t item)
{
    dnode<t> *current,*temp;
    if(first==null)
    {
    first=new dnode<t>;
    first->data=item;
    first->next=null;
    first->prev=null;
    last=first;
    }
    else
    {
    temp=new dnode<t>;
    temp->data=item;
    temp->next=null;
```
```cpp
temp->prev=last;
last->next=temp;
last=temp;
}
}
//function to display the element of doubly link list
template<class t>
void dlist<t>::display()
{
    dnode<t> *current;
    current=first;
    cout<<"data in doubly linked list(front to last):\n";
    while(current!=null)
    {
        cout<<current->data<<" <-> ";
        current=current->next;
    }
    cout<<endl;
}
// To display all the element of list
template<class t>
void dlist<t>::display1()
{
    dnode<t> *current;
    current=last;
    cout<<"Doubly link list end to  first:\n";
    while(current!=null)
    {
        cout<<current->data<<" <-> ";
        current=current->prev;
    }
    cout<<endl;
}
//reverse function
template<class t>
```
## Data Structure simplified
```cpp
void dlist<t>::reverse()
{
    int n;
        n=count();
        dnode<t> *current;
        current=last;
        cout<<"the data after reversing the linked list:\n";
        for(int i=1;i<=n;i++)
        {
                cout<<current->data<<" -> ";
                current=current->prev;
        }
}
//count function
template<class t>
int dlist<t>::count()
{
        int c=0;
        dnode<t> *current;
        current=first;
        while(current!=null)
        {
                c++;
                current=current->next;
        }
        return c;
}
//to insert el(element) at particular position
template<class t>
void dlist<t>::insert(int pos, t el)
{
        int b=count();
        cout<<"length of list :"<<b<<endl;
        if(pos<=b+1)
        {
```
## Doubly link list
```cpp
cout<<"inserting "<<el<<"  at position"<<pos<<endl;
    dnode<t> *current,*forward,*temp;
    current=first;
    temp=new dnode<t>;
    temp->data=el;
    temp->next=temp->prev=null;
    if(pos==1)
    {
        //temp->prev=null;
        temp->next=first;
        first->prev=temp;
        first=temp;
    }
    else if(pos<=b)
    {
        for(int i=1;i<pos-1;i++)
        current=current->next;
        forward=current->next;
        temp->next=forward;
        temp->prev=current;
        current->next=temp;
        forward->prev=temp;
        // forward->prev=temp;
    }
    else
    {
        last->next=temp;
        temp->prev=last;
        temp->next=null;
        last=temp;
    }
    cout<<"node inserted at position "<<pos<<endl;
}
else
cout<<"can't be inserted\n";
```
```cpp
}
//search function
template<class t>
int dlist<t>::search(t element)
{
    int flag=0;
    dnode<t> *current;
    int b=count();
    current=first;
    cout<<"searching element "<<element<<endl;
    for(int i=1;i<=b;i++)
    {
        if(current->data==element)
        {
            flag=1;
            break;
        }
        current=current->next;
    }
    return flag;
}
//overloading + operator
template<class t>
dlist<t> dlist<t>::operator +(dlist<t> l)
{
    dlist l6;
    l6.first=first;
    l6.last=last;
    l6.last->next=l.first;
    l.first->prev=l6.last;
    return l6;
}
main()
{
    int n,el;
```
## Doubly link list
```cpp
dlist<int> l1,l3,l2;// creating the doubly list for integer type
clrscr();
l1.create(34);
l1.create(7);
l1.create(153);
l1.create(40);
l1.display();
//l1.insert(4,112);
l1.display();
if(l1.search(40))
cout<<"element found"<<endl;
else
cout<<"element not in doubly link list"<<endl;
cout<<"enter element to be deleted"<<endl;
cin>>el;
l1.deletenode(el);
l1.display();
}
```

## 4.11 基于双向链表的案例研究

参考链表章节中已列举的案例，并使用双向链表实现。如果使用双向链表实现相同的程序，性能会有什么影响。通过在链表示例中列举的双向链表程序中加入更多数据成员来扩展该程序。这些成员应与学生详细信息相关。这些成员已如下所示：

### 表 4.1：学生描述

| 序号 | 数据成员 | 描述 |
|------|--------------|-------------|
| 1. | Stud_id | 所有学生的唯一 ID。 |
| 2. | Student_name | 学生姓名 |
| 3. | Subject | 科目名称（每个学生有 5 门科目） |
| 4. | Marks | 科目的成绩（对于以上 05 门科目，各自有对应的成绩）。 |
| 5. | Total | 以上所有科目成绩的总和 |

