
Let us consider the following node structure for studying the linked queue and operations:

```
class QNode
{
 public:
 int data;
 QNode *link;
};
class Queue
{
 QNode *Front, *Rear;
 int IsEmpty();
 public:
 Queue()
 {
 Front = Rear = Null;
 }
 void Add( int Element);
 int Delete();
 int FrontElement();
 ~Queue();
};
```

```
int Queue :: IsEmpty()
{
 if(Front == Null)
 return 1;
 else
 return 0;
}
```

The queue element is declared using the class QNode. Each node contains the data declaration and the link pointer to the next element in the queue. This declaration creates an empty queue and initializes the pointers front and rear to Null. Here, front always points to the first node of queue and rear points to the last node of queue. Queue empty condition is simply checking by comparing the front with Null. The function IsEmpty() returns 1 (i.e., true) if the queue is empty and returns 0 (i.e., false), otherwise.

```
int Queue :: IsEmpty()
{
 if(Front == Null)
 return 1;
 else
 return 0;
}
```

FrontElement() returns the data element at the front of the queue. Here, the front is not updated. FrontElement() just reads what is at front.

```
int Queue :: GetFront()
{
    if(!IsEmpty())
        return(Front->data);
}
```

Note that if the NewNode is a node getting added in an empty queue, then along with the rear, the front should also be set to point to the newly added node, which is at the front of the queue. Hence, as both the front and the rear may get updated. Program Code 6.20 shows the addition of an element to a linked queue.

```
void Queue :: Add(int x)
{
    QNode *NewNode;
    NewNode = new QNode;
    NewNode->data = x;
    NewNode->link = Null;
    // if the new is a node getting added in empty queue
    // then front should be set so as to point to new
    if(Rear == Null)
    {
        Front = NewNode;
        Rear = NewNode;
    }
    else
    {
        Rear->link = NewNode;
        Rear = NewNode;
    }
}
```

Delete() function first verifies if there is any data element in the queue. If there is an element, Delete() gets and returns the data at the front of the queue to the caller function. Then, the front is set to point to the new queue front node, which is next to the node being deleted. If the last node is being deleted, then the deleted node's next pointer is guaranteed to be null. Note that if the current deletion of a node results in queue empty state, then along with the front, the rear should also be set to Null.

```
int Queue :: Delete()
{
int temp;
QNode *current = Null;
if(!IsEmpty())
{
temp = Front->data;
current = Front;
Front = Front->link;
delete current;
if(Front == Null)
{
Rear = Null;
return(temp);
}
}
```

```
int Queue :: FrontElement()
{
if(!IsEmpty())
return(Front->data);
}
```

```
void main()
{
Queue Q;
Q.Add(11);
Q.Add(12);
Q.Add(13);
cout << Q.Delete() << endl;
Q.Add(14);
cout << Q.Delete() << endl;
cout << Q.Delete() << endl;
cout << Q.Delete() << endl;
Q.Add(15);
Q.Add(16);
cout << Q.Delete() << endl;
cout << Q.Delete() << endl;
}
```

```
Output
11
12
// due to FrontElement
12
13
14
15
16
```

### 6.12.2.1 Erasing a Linked Queue

The following function in Program Code 6.21 traverses through the whole queue and also releases the memory allocated for each node. This task is handled by a destructor.

```
void Queue :: ~Queue()
{
    QNode *temp;
    while(Front != Null)
    {
        temp = Front;
        Front = Front->link;
        delete temp;
    }
    Front = Rear = Null;
}
```

The linked queue may have the first node on a queue as a header node where the data field may hold some relevant information. In such a list, the first node, that is, the header node, is ignored (i.e. skipped) during Delete() operation. Similarly, the Add() function and queue empty condition will be changed accordingly.

## 6.13 GENERALIZED LINKED LIST

We have defined and represented linear list, which contains series of data elements, all of which had the same data type. In this topic, we shall extend the notion of list even further. We shall study generalized lists, which may be a list of lists.

Generalized lists are defined recursively as lists whose members may be single data elements or other generalized lists. Generalized lists are the most flexible and useful structures. We can use such lists to represent virtually all of the data structures. In addition, generalized lists provide the key data structure for several programming languages, such as LISP. Other languages, such as T and Miranda, include generalized lists and their operations as built-in capabilities. This widespread inclusion of generalized lists in many languages and environments attests the value of such lists in many applications.

### 6.13.1 Definition

A generalized list is a linear list (non-indexed) of zero or more data elements or generalized lists. In other words, a generalized list is a finite sequence of n ≥ 0 elements, α1, α2, ..., αp, which we write as list A = (α1, α2, ..., αk), where αi is either an atom or the list. The elements of αp, where 1 ≤ i ≤ n, which are not atoms are said to be the sub-lists of the list. Here A is the name of generalized list and n is its length.

Thus, a generalized list may be made up of a number of components, some of which are data elements (atoms) and others are generalized lists.

Let us use the common terms being referred to with respect to the generalized list, Head and Tail. These terms refer to parts of the generalized list, that is, Head is the first component in the generalized list, and Tail is the list with the first component removed. If n > 1, then a1 is the head of list whereas (a2, ..., an) is the tail of list.

- A = () The empty (or null) list.
- B = (a, (b, c), d) List of three elements—the first element is a, the second element is list (b, c), and the third element is d.
- C = (B, B, A) List of length 3 with the first and the second element as list B and the third element is list A, which is a null list.
- D = (a, b, D) List of length 3 which is recursive as it includes itself as one of the elements. It can also be written as D = (a, b, (a, b, (a, b, ...))...

In example 2, A is a list made up of three components. The first component is an atom, the second component is a list made up of two atoms, and the third component is the atom d.

One of the better approaches to visualize the generalized lists is using a header node. In this approach, each generalized list has a header node labelled Head. Figure 6.53 shows the pictorial representation of list B.

![](img/a99ec79093c067f0bed8f1086197950e_273_0.png)

Fig. 6.53 Representation of B = (a, (b, c), d)

In example 3, the list C has three components: the first component is list B, the second component is again list B, and the third component is list A. This can be pictorially viewed as in Fig. 6.54.

![](img/a99ec79093c067f0bed8f1086197950e_273_1.png)

Fig. 6.54 Representation of C = (B, B, A)

The list D in example 4 can be viewed as Fig. 6.55.

![](img/a99ec79093c067f0bed8f1086197950e_274_0.png)

Fig. 6.55 Representation of D = (a, b, D)

These cases represent the categories of generalized lists in the order of implementation complexity. The lists could be one of the following categories:

- Lists with no shared references—The components of one list are not members of any other list. In example 2, B is a list with no shared references.
- Lists with shared references—The components of one list can be the members of another list. The logical interpretation of lists leads to two categories as the following: (a) Static interpretation—The current status of the referenced list is anticipated. The referenced list is copied into the referencing list. (b) Dynamic interpretation—The list itself is anticipated. Any future changes in the referenced list should be reflected in the referencing list.
- Recursive list—A recursive list is the one that directly or indirectly references itself. Here D is a recursive list.

Here, the referenced list is the one that is a member of the other list, and the referencing list is the one being created.

### 6.13.2 Applications

The generalized list is the most flexible data structure that can be used for almost every data structure that is linear or non-linear. Let us represent the set and the polynomial using a generalized list to learn why generalized list is said to be the supreme data structure. For simplicity, we shall learn the implementation of generalized list with no shared references and no recursive lists. Such list has members that are not shared references, that is, members of list would not refer to other list and the list would not have the member that directly or indirectly refers itself. The popular implementation of such lists uses the linked list with a header node as in Figs. 6.56–6.58. Let us consider three lists L1, L2, and L3 as L1 = (a, b, c, d), L2 = (a, b), (c,d,d), e), and L3 = (a, (b(b), c). The pictorial representation of these lists using header node is shown in Figs 6.56-6.58, respectively.

![](img/a99ec79093c067f0bed8f1086197950e_274_1.png)

Fig. 6.56 GLL with header nodes for L1 = (a, b, c, d)
