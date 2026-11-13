

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

## Output

menu

- 1 insertion at front
- 2 insertion at end
- 3 insertion at any position
- 4 deletion at front
- 5 deletion at end
- 6 deletion at any position
- 7 display
- 8 exit

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

## 5.4 CIRCULAR LINKED LIST

A singly linked list in which the link field of the last node is assigned with the address of the first node is known as a circular linked list or a circular list. Figure 5.12 illustrates the representation of a circular linked list.

![](img/45784b9f0334626143002ec0d63692fd_166_0.png)

Figure 5.12 Circular linked list

Here, the LINK field of the last node is pointing to the first node. Using the circular linked list any node from any position can be accessed without the need of starting from the first node. List based implementations such as concatenation of lists, splitting of lists and so on can be efficiently performed with circular lists.

One disadvantage with circular lists is that while processing, the list makes sure that it does not form an infinite loop since the direction of pointers in the list is circular. This can be solved with the HEAD node, which is the header node in the list. It helps us to point out the end of the list and terminate the loop.

The operations insertion into and deletion from the circular linked lists are the same as in a singly linked list except that the last node points to the first node. So, while inserting the first node, update the head node pointer and LINK field of it to point to the first node. When deleting the last node, update the previous node of the last node to point to the head node.

![](img/45784b9f0334626143002ec0d63692fd_167_0.png)

![](img/45784b9f0334626143002ec0d63692fd_167_1.png)

## Figure 5.13 Insertion in a circular linked list

In Figure 5.13(b), the node A is inserted between the head node and node B. First obtain the value of the head node LINK field and make the new node pointer to the node B. Now assign the head node pointer with the address of the new node, i.e. head node pointing to the new node.

![](img/45784b9f0334626143002ec0d63692fd_167_2.png)

![](img/45784b9f0334626143002ec0d63692fd_167_3.png)

## Figure 5.14 Deletion of the node in a circular linked list

