

## 3.3.4 删除首节点

当用户想要删除首节点时，首节点的指针将会丢失。因此，删除首节点需要遵循以下步骤序列。

![](img/9b7c80a1312a664ae505ba138aa3306b_69_0.png)

- 持有首节点。
- 找到第二个节点。
- 将首节点存入临时变量 temp。
- 将第二个节点的地址赋给首节点。
- 从链表中删除临时节点（即原来的首节点），以释放资源。

删除首节点的代码如下所示。

```
node *temp;
temp=first; //将首节点存入temp
```

![](img/9b7c80a1312a664ae505ba138aa3306b_69_1.png)

```
first=first->next; //将first指针移动到下一个节点
delete temp; //删除temp节点并释放空间
```

## 3.3.5 删除首节点以外的节点

删除节点的完整方法已在图3.8中说明。

假设用户需要删除值为20的第三个节点。要删除此节点，需要遵循以下步骤。

- 遍历到目标节点，同时保存前一个节点的指针。
- 将目标节点（当前节点，即待删除的节点，值为20）的指针存入temp。
- 将前一个节点连接到当前节点（待删除节点）的下一个节点。

要删除该节点，用户需要在保留前一个节点指针的同时遍历到当前节点。如果前向节点的指针为NULL，则前一个指针将指向NULL。类似地，如果待删除的节点是首节点，则前一个指针将为NULL。在这种情况下，first被移动到first->forward。刚刚遍历过的节点（即前一个节点）被删除。最后，要删除中间的节点，将前一个节点的next连接到目标节点的next指针。同时，删除目标节点（即当前节点），以释放堆中的空闲空间。

```
temp=current;
prev->next=current->next;
delete temp;
```

![](img/9b7c80a1312a664ae505ba138aa3306b_70_0.png)

完整的程序在下面的程序中讨论。

```
从链表中删除节点的程序
void list::deletenode(int element)
{
node* current,*prev=NULL;
int found=0;

current=first;
while(current!=NULL)
{
if(current->data==element)
{
found=1;
break;
}
prev=current;
current=current->next;
}
if(found)  // 如果找到了待删除的节点
{
if(prev==NULL)  // 如果是首节点
{
prev=current->next;
first=prev;
}
else // 对于首节点以外的其他节点
prev->next=current->next;
delete current;
}
else
cout<<"element not in the list"<<endl;
}//deletenode函数结束
```

## 3.4 在链表中查找元素

链表是一种线性数据结构；因此需要从头开始查找元素。在链表中，首先在首节点处查找元素。然后依次访问后续节点，直到找到元素或链表遍历完毕。在最佳情况下，要查找的元素可能就在第一个位置。在最坏情况下，要查找的元素可能在最后一个位置。因此，在最佳情况下，复杂度为O(1)。如果节点数为'n'，则最坏情况下的复杂度为O(n)。也存在中间情况的可能性。然而，在渐近表示法中，只考虑最佳和最坏情况。查找元素的程序如下所示：

```
在链表中查找元素的程序
    int list::search(int el) //查找函数
    {
        //初始时未找到任何项，因此其值初始化为零。
        int found=0;
        node *current=first;
        while(current)
        {
            if(current->data==el)
            {
                found=1;
                break;
            }
            current=current->next;
        }
        return found;
    }//查找函数结束
```

## 3.5 有序链表

在有序链表中，元素按一定顺序排列，即升序或降序。在有序链表中，创建时需要额外的开销。然而，它在查找、寻找最小值或最大值等方面提供了出色的性能。因为在搜索过程中，不需要搜索所有元素，一旦遇到值更大的元素，循环就需要终止。因此，有序链表相对于普通链表具有更好的性能。

在有序链表中，元素从构建阶段起就按升序排列。每当要在有序链表中插入一个新节点时，都需要应用插入逻辑。例如，考虑将数字20、5、13、90、100、25插入到一个有序链表中。

详细步骤如下所述：

- 如果链表为空，则将元素插入到第一个位置。
- 在所有其他情况下，继续向右移动，直到遇到值更大的元素。
- 一旦遇到更大的元素，终止遍历。

创建节点并将元素插入其中。遍历链表中的适当位置，将新节点连接到该位置，同时将先前节点的下一个节点连接到...

```
//链表构造函数
list()
{
    first=NULL;
}
void order_list(int);
void display();
};
void list::order_list(int element)
{
    if(first==NULL)    // 如果链表不存在
    {
    first=new node;
    first->data=element;
    first->next=NULL;
    return;
    }
    //如果链表不为空
    node *temp,*prev=NULL,*current;
    temp=new node;
    temp->data=element;
    //temp->next=NULL;
    current=first;
    while((current->data < element)&& (current!=NULL))
    {
        prev=current;
        current=current->next;
    }
    if(prev==NULL)    // 如果节点要插入到第一个位置
    {
    temp->next=current;
    first=temp;
    }
    else
    {
```

```
```cpp
prev->next=temp;
temp->next=current;
}
}//函数结束

void list::display()
{
    node *current;
    current=first;
    cout<<"Ordered linked list:"<<endl;
    while(current!=NULL)
    {
        cout<<current->data<<" -> ";
        current=current->next;
    }
    cout<<endl;
}

int main()
{
    list l1;
    clrscr();
    cout<<"Creating ordered list"<<endl;
    l1.order_list(29);
    l1.order_list(14);
    l1.order_list(70);
    l1.order_list(12);
    l1.order_list(30);
    l1.order_list(121);
    l1.display();
    getch();
    return 0;
}
```
```

## 3.6 反转链表

反转链表是一项复杂的操作，需要深入理解指针。丢失任何指针都会导致节点和信息的丢失。在反转链表的过程中，我们从前往后遍历到最后一个节点。在遍历过程中，最后访问到的节点将被附加到新链表的开头，类似于从开头插入的操作。我们需要反转这个链表，如图3.11所示。在所考虑的链表中，首节点是50，最初它将附加在开头。

当新节点（即10）到达时，它将被附加在50的开头，如图3.11和3.12所示。

![](img/9b7c80a1312a664ae505ba138aa3306b_76_0.png)

![](img/9b7c80a1312a664ae505ba138aa3306b_76_1.png)

链表反转在图示中逐步演示。

```
问题：编写一个程序来反转链表
解决方案：
// 反转一个由first指针指向首节点的链表。
void list::reverse()
{
```

```
cout<<" Reverse of a list is ::"<<endl;
    // 将所有节点初始化为NULL。
        node *current,*forward,*back=NULL;
    current=first;
    forward=current->next;
    while(forward!=NULL)
    {
        current->next=back;
        back=current;
        current=forward;
        forward=forward->next;
    }
        current->next=back;
        first=current;
}
```

## 3.7 合并两个链表

由于各种原因，我们需要合并链表，以便将多个链表中的数据容纳到单个链表中。在合并过程中，需要特别注意确保两个链表中的元素在合并到第三个链表时保持有序。合并链表将带来更好的性能和管理。我们创建了第三个链表，其中存储了两个链表的内容。合并两个链表的详细方法和程序如下所述。

```
list list:: merge(list l1,list l2)// 合并链表1和链表2。
    {
        list l3;
        node *one,*two,*current;
        one=l1.first;
        two=l2.first;
        if(one->data < two->data)    // 如果第一个链表的元素较小
        {
        l3.first=current=one;
        one=one->next;// 移动到下一个节点
        }
```

