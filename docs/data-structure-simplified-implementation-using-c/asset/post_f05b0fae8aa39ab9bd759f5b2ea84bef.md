
- At the end of a link list, or
- At the beginning/front of a link list

![](img/9b7c80a1312a664ae505ba138aa3306b_61_0.png)

In the insertion from the end, a new node is placed at the end of an existing link list. For instance, inserting the node with value 20, in the link list already having the node 10 is illustrated below. Here 20, will be placed after 10 and the pointer will be appropriately adjusted. After inserting 20, consider that we have to insert 30 into the existing list. Same is illustrated in the figure 3.3(b). This is known as backward growth of a link list. Since new node is attached at the end.

Similarly, we can create a link list that can be forward growing. In forward list, the new node is inserted at the beginning, instead of at the end. Same has been illustrated in the figure 3.4. Consider the case of figure 3.4. In this case, a node with the value of 5 already existed. The new node having value 10 is created; correspondingly it will be inserted at the beginning of the existing link list. Similarly, the new node that has arrived is 20. It will be positioned at the beginning of 10 (refer figure 3.4). This type of growth in a link list is known as forward growing link list.

![](img/9b7c80a1312a664ae505ba138aa3306b_61_1.png)

## B. Display the node

Once the link list is created, irrespective of the forward growing or the backward growing, we would like to view the data that is hold by various node of a link list. To display the node element, we begin from the start i.e. first node and continue to move towards the end node. Next pointer of the last node points to the NULL that can be used to stop the traversal. Logic for the traversal has been depicted in the following program:

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

The complete program for creation and display of a link list has been depicted as follows:

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

## C. Creating the list by inserting at the beginning

Link list can also be created by inserting the element at the beginning. The new node that is attached becomes the first node of the list. For instance, if list is to be created for the series of item 10, 20, 30, 5, 9, 100, then the list will grow as illustrated in the figure 3.5.

![](img/9b7c80a1312a664ae505ba138aa3306b_64_0.png)

Once the new node is created then it will be connected to the first node of an already existing list, as a result the existing first node will move to the second position. Therefore, the new node should become the first node. The complete program for the insertion of a node in a link list has been depicted below:

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

## 3.3 INSERTING THE NODE IN AN EXISTING LINK LIST

In an existing link list, node can be inserted anywhere as intended by the user. However, for the program side, we need to consider two cases that will cover all positions of insertion. These situations can be:

- At the first position
- Position, other than the first.

All these cases along with the method of connecting them have been depicted in the following sub-sections.

### 3.3.1 Inserting at the first position

Consider a link list as illustrated in the figure 3.6. In this list, a new node is to be placed (inserted) at the beginning. To accomplish this objective, first we have to create the new node and attach this new node before the existing first node. This operation is illustrated in the figure 3.6.

![](img/9b7c80a1312a664ae505ba138aa3306b_65_0.png)

Due to insertion of a newnode at the beginning, status of existing first node will change. As first node will become the second node and the newnode will result into first node. Consequently, the first pointer has to be shifted to the newnode. The complete sequence of operation has been described as:

## Method of inserting at first position

To insert the node at the first position, the following sequence needs to be followed.

- Create the newnode
- Link it to the first node
- Change the position of first node with this newnode.
- Return the pointer of this new first node

![](img/9b7c80a1312a664ae505ba138aa3306b_66_0.png)

Assume that the link list comprise of the items as: 50,10,20,30. The new element is to be inserted is ‘70’. The first node is now moved to the second node and newnode has become the first node. The resultant link list has been illustrated in figure 3.5. Code is:

```
newnode=new node;
newnode->data=el;
newnode->next=first;
first=newnode;
```

### 3.3.2 Inserting the node other than the first position

To insert the node in between, we will determine the two nodes where new node is to be

![](img/9b7c80a1312a664ae505ba138aa3306b_66_1.png)

inserted. The node that will be before this node will be known as previous node and the node after this node will be known as forward node. In our program, we have named forward node as current node. Same is illustrated in the figure 3.6.

In the existing link list, pointer of previous node needs to be connected to the newnode, whereas pointer of the newnode to be connected to the current node.

```
prev->next=newnode;
newnode->next=current;
```

The complete method of inserting the node in a link list has been depicted in the insert function. In the discussed function, we accept the position, that is passed as an argument and examine it with the number of nodes that a link list is consisting of at that specific point in time. Users intended position should not be more than the existing list size (number of nodes) plus 1. For instance, if the total numbers of nodes are n, then the position supplied should not be more than n+1.

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

The above program is well suited for insertion at last position. Since, during positioning at last position involves placing of the newnode at last, this is preceded by connecting the existing last node with the newnode. Insertion of a newnode is illustrated in the figure 3.7.

Code written for the in-between will also support the insertion of the node at last position.

```
prev->next=newnode;      (1)
newnode->next=current    (2)
```

However, the prev node will point to the last node, whereas the current will point to the last node. Since the code of (1) will connect the last node to the newnode therefore one objective will be completed. Whereas the code (2) will connect the newnode to the current node which is already resulted in NULL, as illustrated in the figure 3.7. Consequently, the code will work for inserting the node at any position other than the first position.

### 3.3.3 Deleting the node in a link list

Link list holds the data similar to other type with the difference that it is dynamic in nature. It may happen that the data stored in a link list may no longer needed. This leads to need of another operation term as deletion to be envisioned on a link list. Since, link list is connected with the help of pointers, therefore, due care need to be exercised to ensure that link list remains connected even after the deletion of a node(s). During deletion of a node, the following possibilities related to the position need to be taken into account.

- Deleting first node.
- Deleting other than the first node.
