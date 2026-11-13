
Similar to other operators, new and delete operators can be overloaded. Program Code 6.1 demonstrates dynamic variables, new and delete operators, and pointers.

```
PROGRAM CODE 6.1

#include<iostream.h>
int main()
{
 int *ptr1, *ptr2;
 ptr1 = new int;
 *ptr1 = 52;
 cout << "*ptr1 = " << *ptr1 << endl;
 cout << "*ptr2 = " << *ptr2 << endl;
 *ptr2 = 63;
 cout << "*ptr1 = " << *ptr1 << endl;
 cout << "*ptr2 = " << *ptr2 << endl;
 ptr1 = new int;
 *ptr1 = 98;
 cout << "*ptr1 = " << *ptr1 << endl;
 cout << "*ptr2 = " << *ptr2 << endl;
 return 0;
}
Output:
*ptr1 = 52
*ptr2 = Garbage
*ptr1 = 52
*ptr2 = 63
*ptr1 = 98
*ptr2 = 63
```

## 6.5 LINKED LIST ABSTRACT DATA TYPE

Although a linked list can be implemented in a variety of ways, the most flexible implementation is by using pointers. To implement the same in C++, we can view the entire linked list as an object of the class List. Figure 6.9 shows an abstract representation of a linked list.

![](img/a99ec79093c067f0bed8f1086197950e_219_0.png)

Fig. 6.9 Abstract representation of linked list

Each linked list has to have a special external link (or pointer), say, Head. We call it an external link because it is not stored in the list. We shall now extend the abstract notation to show the external link. Figure 6.10 illustrates the list with the external link, Head.

![](img/a99ec79093c067f0bed8f1086197950e_220_0.png)

Fig. 6.10 Linked list with head pointer

To represent this linked list (Fig. 6.10), we consider it as an object of class LList whose definition is as follows:

```
class LList
{
 private:
  Node *Head;
 public:
  LList();
  ~LList();
  :
  :      } member functions here
  :
};
```

The LList class has only one data member, the Head pointer, which points to the first node of the list, which is used to access the list. The member functions including the constructor and the destructor are used to process the list. Note that the Head is private and all other member functions are public. This is because particular nodes of the list are accessible to outside objects through pointers; the nodes are made inaccessible to outside objects by declaring Head private so that the information hiding principle is not really compromised. This is illustrated in Program Code 6.2.

```
PROGRAM CODE 6.2
class LList
{
 private:
  Node *Head;
  Node *Tail;    // optional data members
  int  Size;
 public:
  LList()
  {
      Head = Tail = Null;
      Size = 0;
  }
  void Create();
  void Traverse();
  void Insert( int data, position);
  void Append(int data);
  void Delete(int position);
  void Reverse();
};
```

### 6.5.1 Data Structure of Node

Each node has data and link fields. The data field holds data element(s) and the link field(s) stores the address of its successor (and/or predecessor, if any). As the link is a pointer to its successor, it should be a pointer variable, which should hold the address of its successor. The successor node is of the same type as that of the node itself. Hence, every node has one member, which points to a node of the same type as itself. As every node is a group of two (or more) data elements which are of different data types, they are logically grouped using the data type, object. The link field of a node is a pointer that references to a node of the same type as itself. Hence, we need a self-referential object.

The declaration of the data structure of a node is given as follows:

```
class Node
{
public:
    int data;
    Node *link;
};
```

```
class List
{
private:
    Node *Head;
public:
    . . . member functions here
}
};
```

Here, within the class, the statement Node *link defines the link field of a node. Here, Node is a data type of the pointer variable link.

Consider the following piece of code:

```
class Node
{
public:
    int data;
    Node *link;
} *first, A;
first = &A;
A.data = 10;
A.link = Null;
```

![](img/a99ec79093c067f0bed8f1086197950e_222_0.png)

Now, the statement

```
cout << first->data;
```

will print the output 10.

We discussed the node structure of the linked list. Let us now discuss the various operations on a linked list, illustrated in Program Code 6.3.

```
PROGRAM CODE 6.3
class Node
{
    public :
        int data;
        Node *link;
};

class Llist
{
    private:
        Node *Head,*Tail;
        void Recursive_Traverse(Node *tmp)
        {
            if(tmp == Null)
            return;
            cout << tmp->data << "\t";
            Recursive_Traverse(tmp->link);
        }

    public:
        Llist()
        {
            Head = Null;
        }
        void Create();
        void Display();
        Node* GetNode();
        void Append(Node* NewNode);
        void Insert_at_Pos(Node *NewNode, int position);
        void R_Traverse()
        {
            Recursive_Traverse(Head);
            cout << endl;
        }
        void DeleteNode(int del_position);
};

void Llist :: ~Llist()
{
    Node *Temp;
    while(Head != Null)
    {
        Temp = Head;
        Head = Head->link;
        delete Temp;
    }
}

void Llist :: Create()
{
    char ans;
    Node *NewNode;
    while(1)
    {
        cout << "Any more nodes to be added (Y/N)*";
        cin >> ans;
        if(ans == 'n') break;
        NewNode = GetNode();
        Append(NewNode);
    }
}

void Llist :: Append(Node* NewNode)
{
    if(Head == Null)
    {
        Head = NewNode;
        Tail = NewNode;
    }
    else
    {
        Tail->link = NewNode;
	Tail = NewNode;
    }
}

Node* Llist :: GetNode()
{
	Node *Newnode;
	Newnode = new Node;
	cin >> Newnode->data;
	Newnode->link = Null;
	return(Newnode);
}

void Llist :: Display()
{
	Node *temp = Head;
	if(temp == Null)
	cout << "Empty List";
	else
	{
	while(temp != Null)
	{
	cout << temp->data << "\t";
	temp = temp->link;
	}
	}
	cout << endl;
}

void main()
{
	Llist L1;
	L1.Create();
	L1.Display();
}
```

### 6.5.2 Insertion of a Node

Depending on the type of list or need of the user, insertion can be made at the beginning, middle, or at the end of the list. If the list is an ordered list, the insertion should not affect the order and this may require inserting the data at proper locations so that the order is preserved. The information about where the node is to be inserted can be decided by searching through the list, obtaining the position, and then inserting the same.

Note that the symbol ⊥ shown in all figures in this chapter indicates the end of list marker representing null. We shall use the same notation throughout the book.

### Insertion of a Node at a Middle Position

Assume that a node is to be inserted at some position other than the first position. Let Prev refer to the node after which NewNode node is to be inserted.

We need the following two steps:

```
NewNode->link = Prev->link;
Prev->link = NewNode;
```

The node NewNode is to be inserted between Prev and the successor of Prev. The link manipulation required to accomplish this is shown in Fig. 6.11 with dotted lines.

![](img/a99ec79093c067f0bed8f1086197950e_225_0.png)

Fig. 6.11 Link manipulations for insertion of a node

The steps to perform the link manipulation are as follows:

- NewNode is a node to be inserted after Prev. The node that is a successor of Prev will now become the successor of NewNode. Currently, Prev->link holds the pointer to the successor of Prev. Set the link field of the NewNode such that Prev's successor node becomes the successor of NewNode.

```
NewNode->link = Prev->link;
```

In other words, NewNode becomes the predecessor of the node whose predecessor was Prev, because NewNode is to be placed in between Prev and its successor (Fig. 6.12).

![](img/a99ec79093c067f0bed8f1086197950e_225_1.png)

Fig. 6.12 Link manipulations for insertion of a node (Step 1)

- Now, let us make NewNode the successor of Prev. This can achieved by setting the link field of Prev to NewNode (Fig. 6.13).

```
Prev->link = NewNode;
```

![](img/a99ec79093c067f0bed8f1086197950e_226_0.png)

Fig. 6.13 Link manipulations for insertion of a node (Step 2)

### Insertion of a Node at the First Position

Let us consider a situation when the node is to be inserted at the first position. As per the steps discussed for insertion of a node at the middle, we need Prev, which is a pointer to the node after which NewNode is to be added. To insert a node at the first position, there exists no Prev node.

The link manipulations needed to add a node at the first location is shown in Fig. 6.14 using dotted lines.

![](img/a99ec79093c067f0bed8f1086197950e_226_1.png)

Fig. 6.14 Link manipulations for insertion of a node at the first position

Head is the pointer variable pointing to the starting node of the list. The insertion of NewNode at the first position should make Head point to NewNode, and in addition, the current node which is at the first position should become the second node of the list. Hence, the link field of NewNode should be set to point to the current first node, that is, the node pointed by the pointer First.

The following two steps to insert NewNode at the beginning of the linked list.

```
NewNode->link = Head;
Head = NewNode;
```

Figure 6.15 shows NewNode to be inserted in the list.
