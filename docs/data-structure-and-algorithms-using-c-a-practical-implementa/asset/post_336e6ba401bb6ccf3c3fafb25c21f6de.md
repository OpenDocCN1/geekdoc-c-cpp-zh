
void insert(struct link *node)
{
    int n;
    cout<<"\nENTER THE INFORMATION VALUE TO INSERT";
    cin>>n;
    node = start.next;
    while(node)
    {
        if(node->info >= n)
        {
            New=(struct link *)malloc(sizeof(struct link));
            New->info = n;
            New->next = node;
            New->previous = node->previous;
            node->previous->next = New;
            node->previous = New;
            break;
        }
        else
        {
            node=node->next;
        }
    }
}

int main()
{
    struct link *node;
    create(node);
    cout<<"\n AFTER CREATING THE LINKED LIST IS \n";
    display(node);
    insert(node);
    cout<<"\n List after insertion of first node \n";
    display (node);
}

# OUTPUT

```
ENTER THE NUMBER 25
DO YOU WANT TO CREATE MORE NODES(Y/N) Y
ENTER THE NUMBER 9
DO YOU WANT TO CREATE MORE NODES(Y/N) Y
ENTER THE NUMBER 35
DO YOU WANT TO CREATE MORE NODES(Y/N) Y
ENTER THE NUMBER 21
DO YOU WANT TO CREATE MORE NODES(Y/N) N
AFTER CREATING THE LINKED LIST IS
Link list elements printing in Forward Direction
25 95 35 21
Link list elements printing in Backward Direction
21 35 95 25
ENTER THE INFORMATION VALUE TO INSERT 50
List after insertion of first node
Link list elements printing in Forward Direction
25 50 95 35 21
Link list elements printing in Backward Direction
21 35 95 50 25
Process exited after 21.42 seconds with return value 0
Press any key to continue . . .
```

## 7.6.5 /* Delete First Node From a Double Linked List */

```
# include <iostream>
#include<iostream.h>
#include <stdlib.h>
using namespace std;
struct link
{
    int info;
    struct link *next;
    struct link *previous;
};
struct link start,*New;
void create (struct link *);
void display (struct link *);
void Delete(struct link *);
```

```
void create(struct link *node)
{
    char ch='y';
    start.next = NULL; /* Empty list */
    start.previous = NULL;
    node = &start; /* Point to the start of the list */
    while( ch == 'y' || ch=='Y')
    {
        node->next = (struct link *) malloc(sizeof(struct link));
        node->next->previous = node;
        node = node->next;
        cout<<"\n ENTER THE NUMBER";
        fflush(stdin);
        cin>>node->info;
        node->next = NULL;
        fflush(stdin);
        cout<<"\nDO YOU WANT TO CREATE MORE NODES[Y/N] ";
        cin>>ch;
    }
}

void display (struct link *node)
{
    node = start.next;
    cout<<endl<<"Link list elements printing in Forward Direction\n";
    while(node->next)
    {
        cout<<setw(5)<<node->info;
        node = node->next;
    }
    cout<<setw(5)<<node->info;
    cout<<endl<<"Link list elements printing in Backward Direction\n";
    do {
        cout<<setw(5)<<node->info;
        node = node->previous;
    } while (node->previous);
}

void Delete(struct link *node)
{
    node = start.next;
    if( node == NULL)
    {
        printf("\n Underflow");
    }
    else
    {
        node->previous->next = node->next ;
        node->next->previous = node->previous ;
        free(node) ;
    }
}
```

```
int main()
{
    struct link *node;
    create(node);
    cout<<"\n AFTER CREATING THE LINKED LIST IS \n";
    display(node);
    Delete(node);
    cout<<"\n List Deletion of first node \n";
    display (node);
}
```

# OUTPUT

```
ENTER THE NUMBER 25
DO YOU WANT TO CREATE MORE NODES(Y/N) Y
ENTER THE NUMBER 36
DO YOU WANT TO CREATE MORE NODES(Y/N) Y
ENTER THE NUMBER 85
DO YOU WANT TO CREATE MORE NODES(Y/N) Y
DO YOU WANT TO CREATE MORE NODES(Y/N) Y
ENTER THE NUMBER 89
DO YOU WANT TO CREATE MORE NODES(Y/N) Y
ENTER THE NUMBER 12
DO YOU WANT TO CREATE MORE NODES(Y/N) N
AFTER CREATING THE LINKED LIST IS
Link list elements printing in Forward Direction
25 36 85 9 12
Link list elements printing in Backward Direction
12 9 85 36 25
List Deletion of first node
Link list elements printing in Forward Direction
36 56 78 8 12
Link list elements printing in Backward Direction
12 8 9 85 36
Process exited after 11.9 seconds with return value 0
Press any key to continue . . .
```

## 7.6.6 /*Delete the Last Node From the Double Linked List*/

```
#include <iostream>
#include<conio.h>
# include <stdio.h>
using namespace std;
struct link
{
    int info;
    struct link *next;
    struct link *previous;
};
struct link start,*New;
void create(struct link *);
void display(struct link *);
void Delete(struct link *);
void create(struct link *node)
{
    char ch='y';
    start.next = NULL; /* Empty list */
    start.previous = NULL;
    node = &start; /* Point to the start of the list */
    while( ch == 'y' || ch=='Y')
    {
        node->next = (struct link *) malloc(sizeof(struct link));
        node->next->previous = node;
        node = node->next;
        cout<<"\n ENTER THE NUMBER";
        fflush(stdin);
        cin>>node->info;
        node->next = NULL;
        fflush(stdin);
        cout<<"\nDO YOU WANT TO CREATE MORE NODES[Y/N] ";
        fflush(stdin);
        cin>>ch;
    }
}
```

```
void display (struct link *node)
{
    node = start.next;
    cout<<endl<<"Link list elements \n";
    while(node->next)
    {
        cout<<setw(5)<<node->info;
        node = node->next;
    }
    cout<<setw(5)<<node->info;
}

void Delete(struct link *node)
{
    int n=0;
    node = start.next;
    if ( node == NULL)
    {
        cout<<"\n Underflow";
    }
    else
        while(node->next)
        {
            node = node->next;
            n++;
        }

    node = start.next;
    while(n != 1)
    {
        node = node->next;
        n--;
    }
    node->next;
    node->previous->next = NULL;
    free(node);
}
```

```
int main()
{
    struct link *node;
    int n;
    create(node);
    cout<<"\n AFTER CREATING THE LINKED LIST IS \n";
    display(node);
    Delete(node);
    cout<<"\n List Deletion of Last node \n";
    display (node);
}
```

# OUTPUT

```
ENTER THE NUMBER 12
DO YOU WANT TO CREATE MORE NODES...Y/N y
ENTER THE NUMBER 4
DO YOU WANT TO CREATE MORE NODES...Y/N y
ENTER THE NUMBER 7
DO YOU WANT TO CREATE MORE NODES...Y/N y
ENTER THE NUMBER 8
DO YOU WANT TO CREATE MORE NODES...Y/N n
AFTER CREATING THE LINKED LIST IS
Link list elements
12 54 67 8
List Deletion of Last node
Link list elements
12 54 67
Process exited after 29.63 seconds with return value 0
Press any key to continue . . .
```

## 7.7 Header Linked List

The header link list is a special type of linked list in which a special node will be used as header node. The purpose of this node is to store the total number of elements present in the linked list. On necessity we can easily access the elements of the linked list.

### Types of Header Linked List

- Basically two types of header linked list are used as
- Grounded Header Linked List and Circular Header Linked list.

### 1. Grounded Header Linked List

In this type of linked list the last node will have the NULL pointer. In the header linked list the start pointer always points to the header node. start -> next = NULL indicates that the grounded header linked list is empty. Like single linked list and double linked list we can also perform all type of operations with this type of header linked list.

![](img/1faaa0256577c74e8a61f42967760aa8_238_0.png)

### 2. Circular Header Linked List

In this type of linked list the last node will point or connected to header node. Because in circular linked list the last node will connect to the first node of linked list. So formally we can say that the list does not indicate first or last nodes. In this case, external pointers provide a frame of reference because last node of a circular linked list does not contain the NULL pointer. Like single linked list and double linked list we can also perform all type of operations with this type of header linked list.

![](img/1faaa0256577c74e8a61f42967760aa8_239_0.png)

## 7.7.1 /* Inserting a Node Into a Header Linked List */

```c
# include <stdio.h>
# include <alloc.h>
struct link
{
	int info;
	struct link *next;
};
int i;
int number;
struct link *start, *new;
void insert(struct link *);
void create(struct link *);
void display(struct link *);
void create(struct link *node)
{
	char ch='y';

	start->next = NULL; /* Empty list */

	node = start; /* Point to the header node of the
list */
```
