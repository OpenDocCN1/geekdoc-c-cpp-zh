

```cpp
else
{
  temp->link=head->link;
  head->link=temp;
  temp->data=ele;
}
```

```cpp
template<class t>
void llist<t>::insert()
{
  t ele;
  cout<<"enter the element\n";
  cin>>ele;
  temp=(struct node*) malloc(sizeof( struct node) );
  if (temp==NULL)
  {
    cout<<"memory allocation error\n";
    return;
  }
  if (head->link==NULL)
  {
    temp->data=ele;
    head->link=temp;
    temp->link=NULL;
  }
  else
  {
    for (temp1=head->link; temp1->link!=NULL; temp1=temp1->link)
    {
    }
    temp1->link=temp;
    temp->data=ele;
    temp->link=NULL;
  }
}
```

```cpp
template<class t>
void llist<t>::insert()
{
  t ele;
  int pos,i;
  cout<<"enter the element\n";
  cin>>ele;
  cout<<"enter the position\n";
  cin>>pos;
  temp=(struct node*) malloc(sizeof( struct node) );
  if (temp==NULL)
  {
    cout<<"memory allocation error\n";
    return;
  }
  if (head->link==NULL)
  {
    temp->data=ele;
    head->link=temp;
    temp->link=NULL;
  }
  else
  {
    for (temp1=head, i=1; i<pos; i++)
      temp1=temp1->link;
    temp->link=temp1->link;
    temp1->link=temp;
    temp->data=ele;
  }
}
```

```cpp
template<class t>
void llist<t>::deletef ()
{
    t ele;
    if (head->link==NULL)
    {
    cout<<"linked list is empty\n";
    return;
    }
    temp=head->link;
    temp1=temp->link;
    head->link=temp1;
    ele=temp->data;
    free (temp);
    cout<<"the deleted element is "<<ele<<endl;
}
```

```cpp
template<class t>
void llist<t>::deletee ()
{
    t ele;
    if (head->link==NULL)
    {
    cout<<"linked list is empty\n";
    return;
    }
    for (temp1=head; temp1->link!=NULL; temp1=temp1->link)
    {
    temp=temp1;
    }
    temp->link=NULL;
    ele=temp1->data;
    free(temp1);
    cout<<"the deleted element is "<<ele<<endl;
}
```

```cpp
template<class t>
void llist<t>::deletea()
{
    t ele;
    int pos,i;
    if(head->link==NULL)
    {
        cout<<"linked list is empty\n";
        return;
    }
    cout<<"enter the position\n";
    cin>>pos;
    for(temp1=head, i=0; i<pos; i++, temp1=temp1->link)
    {
    temp=temp1;
    temp->link=temp1->link;
    ele=temp1->data;
    cout<<"the deleted element is "<<ele<<endl;
    free(temp1);
    }
}
```

```cpp
template<class t>
void llist<t>::display()
{
    if(head->link==NULL)
    {
        cout<<"linked list is empty\n";
        return;
    }
    for(temp=head->link; temp!=NULL; temp=temp->link)
    {
        cout<<temp->data<<" ";
    }
}
```

```cpp
void main()
{
    int ch;
    llist<int> l;
    clrscr();
    while(1)
    {
    cout<<"...\n";
    cout<<"1.insertion at front\n";
    cout<<"2.insertion at end\n";
    cout<<"3.insertion at any position\n\n";
    cout<<"4.deletion at front\n";
    cout<<"5.deletion at end\n";
    cout<<"6.deletion at any position\n";
    cout<<"7.display\n\n";
    cout<<"8.exit\n";
    cout<<"enter your choice\n";
    cin>>ch;
    switch(ch)
    {
    case 1:
    l.insertf();
    break;
    case 2:
    l.insert();
    break;
    case 3:
    l.inserta();
    break;
    case 4:
    l.deletef();
    break;
    case 5:
    l.deletee();
    break;
    case 6:
    l.deletea();
    break;
    case 7:
    l.display();
    break;
    case 8:
    exit(0);
    break;
    }
    }
}
```

## 输出

菜单

- 1 头部插入
- 2 尾部插入
- 3 任意位置插入
- 4 头部删除
- 5 尾部删除
- 6 任意位置删除
- 7 显示
- 8 退出

```
menu
1.insertion at front
2.insertion at end
3.insertion at any position
4.deletion at front
5.deletion at end
6.deletion at any position
7.display
8.exit
enter your choice
1
enter the element
10
menu
1.insertion at front
2.insertion at end
3.insertion at any position
4.deletion at front
5.deletion at end
6.deletion at any position
7.display
8.exit
enter your choice
1
enter the element
20
menu
1.insertion at front
2.insertion at end
3.insertion at any position
4.deletion at front
5.deletion at end
6.deletion at any position
7.display
8.exit
enter your choice
7
20 10
menu
1.insertion at front
2.insertion at end
3.insertion at any position
4.deletion at front
5.deletion at end
6.deletion at any position
7.display
8.exit
enter your choice
2
enter the element
30
menu
1.insertion at front
2.insertion at end
3.insertion at any position
4.deletion at front
5.deletion at end
6.deletion at any position
7.display
8.exit
enter your choice
3. insertion at any position
4. deletion at front
5. deletion at end
6. deletion at any position
7. display
8. exit
enter your choice
2
enter the element
40
menu
1. insertion at front
2. insertion at end
3. insertion at any position
4. deletion at front
5. deletion at end
6. deletion at any position
7. display
8. exit
enter your choice
7
menu
1. insertion at front
2. insertion at end
3. insertion at any position
4. deletion at front
5. deletion at end
6. deletion at any position
7. display
8. exit
enter your choice
20 10 30 40
menu
1. insertion at front
2. insertion at end
3. insertion at any position
4. deletion at front
5. deletion at end
6. deletion at any position
7. display
8. exit
enter your choice
3
enter the element
50
enter the position
3
menu
1. insertion at front
2. insertion at end
3. insertion at any position
4. deletion at front
5. deletion at end
6. deletion at any position
7. display
8. exit
enter your choice
7 10 50 30 40
menu
1.insertion at front
2.insertion at end
3.insertion at any position
4.deletion at front
5.deletion at end
6.deletion at any position
7.display
8.exit
enter your choice
4
the deleted element is 20
menu
1.insertion at front
2.insertion at end
3.insertion at any position
4.deletion at front
5.deletion at end
6.deletion at any position
7.display
8.exit
enter your choice
7
10 50 30 40
menu
1.insertion at front
2.insertion at end
3.insertion at any position
4.deletion at front
5.deletion at end
6.deletion at any position
7.display
8.exit
enter your choice
5
the deleted element is 40
menu
1.insertion at front
2.insertion at end
3.insertion at any position
4.deletion at front
5.deletion at end
6.deletion at any position
7.display
8.exit
enter your choice
8
exit
7
10 50 30
menu
1.insertion at front
2.insertion at end
3.insertion at any position
4.deletion at front
5.deletion at end
6.deletion at any position
7.display
8.exit
enter your choice
6
enter the position
2
menu
the deleted element is 50
menu
1.insertion at front
2.insertion at end
3.insertion at any position
4.deletion at front
5.deletion at end
6.deletion at any position
7.display
8.exit
enter your choice
7
10 30
menu
1.insertion at front
2.insertion at end
3.insertion at any position
4.deletion at front
5.deletion at end
6.deletion at any position
7.display
8.exit
enter your choice 8
```

## 5.4 循环链表

将最后一个节点的链接字段赋为第一个节点地址的单链表称为循环链表或循环列表。图 5.12 说明了循环链表的表示。

![](img/45784b9f0334626143002ec0d63692fd_166_0.png)

图 5.12 循环链表

在这里，最后一个节点的 LINK 字段指向第一个节点。使用循环链表，可以从任意位置访问任何节点，而无需从第一个节点开始。基于列表的实现，例如列表的连接、分割等，可以使用循环列表高效地执行。

循环列表的一个缺点是，在处理过程中，列表必须确保不会形成无限循环，因为列表中指针的方向是循环的。可以通过 HEAD 节点来解决这个问题，它是列表中的头节点。它帮助我们指示列表的末端并终止循环。

循环链表的插入和删除操作与单链表相同，只是最后一个节点指向第一个节点。因此，在插入第一个节点时，更新头节点指针及其 LINK 字段以指向第一个节点。在删除最后一个节点时，更新最后一个节点的前一个节点以指向头节点。

![](img/45784b9f0334626143002ec0d63692fd_167_0.png)

![](img/45784b9f0334626143002ec0d63692fd_167_1.png)

## 图 5.13 循环链表中的插入

在图 5.13(b) 中，节点 A 被插入到头节点和节点 B 之间。首先获取头节点 LINK 字段的值，并使新节点指向节点 B。现在将头节点指针赋为新节点的地址，即头节点指向新节点。

![](img/45784b9f0334626143002ec0d63692fd_167_2.png)

![](img/45784b9f0334626143002ec0d63692fd_167_3.png)

## 图 5.14 循环链表中节点的删除

