

first = &start;
New = (struct list* ) malloc(sizeof(struct list));
New->next = node ;
first->next = New;
cout<<"\n Input the first node value: ";
cin>>New->info;
}

Output

![](img/1faaa0256577c74e8a61f42967760aa8_186_0.png)

## 7.4.3 /* Insert a Node Into a Simple Linked List at the End of the List */

```cpp
#include<iostream>
#include<conio.h>
#include<stdio.h>
#include<stdlib.h>
using namespace std;
struct list
{
    int info;
    struct list *next;
};
struct list start, *first, *New,*last;
/* Function main */
void create(struct list *);
void display(struct list *);
void insert(struct list *);
int main()
{
    struct list *node;
    create(node);
    insert(node);
    display(node);
}
```

```cpp
void create(struct list *node) /*LOGIC TO CREATE A LINK LIST*/
{
 char ch='y';
 start.next = NULL;
 node = &start; /* Point to the start of the list */
 while(ch =='y' || ch =='Y')
 {
 node->next = (struct list * )
 malloc(sizeof(struct list));
 node = node->next;
 cout<<"\n ENTER A NUMBER : ";
 cin>>node->info;
 node->next = NULL;
 cout<<"\n DO YOU WANT TO CREATE MORE NODES : ";
 cin>>ch;
 }
 }
```

```cpp
void display(struct list *node)
{
 node = start.next;
 /*DISPLAY THE LINKED LIST*/
 cout<<"\n After Inserting a node list is as follows:\n";
 while (node)
 {
 cout<<setw(5)<<node->info;
 node = node->next;
 }
}
```

```cpp
void insert(struct list *node)
{ /* LOGIC OF INSERTION(LAST NODE) */
 node = start.next;
 last = &start;
 while(node)
 {
 node = node->next;
 last = last->next;
 }
 if(node == NULL)
 {
 New = (struct list* ) malloc(sizeof(struct list));
 New->next = node ;
 last->next = New;
 cout<<"\n ENTER THE VALUE OF LAST NODE : ";
 cin>>New->info;
 } }
```

### Output

```
ENTER A NUMBER : 12
DO YOU WANT TO CREATE MORE NODES: y
ENTER A NUMBER : 65
DO YOU WANT TO CREATE MORE NODES: y
ENTER A NUMBER : 98
DO YOU WANT TO CREATE MORE NODES: y
ENTER A NUMBER : 22
DO YOU WANT TO CREATE MORE NODES: n
ENTER THE VALUE OF LAST NODE: 3
After Inserting a node list is as follows:
12 65 98 22 3
Process exited after 88.413 seconds with return value 0
Press any key to continue . . .
```

## 7.4.4 /* Insert a Node Into a Simple Linked List When the Node Is Known */

```cpp
#include<iostream>
#include<iomanip>
#include<stdio.h>
#include<stdlib.h>
using namespace std;
struct link
{
    int info;
    struct link *next;
};
struct link start,*first,*New,*previous;
/* Function main */
void create(struct link *);
void display(struct link *);
void insert(struct link *);
int main()
{
    struct link *node;
    create(node);
    insert(node);
    display(node);
}
```

```cpp
void create(struct link *node) /*LOGIC TO CREATE A LINK LIST*/
{
char ch='Y';
start.next = NULL;
node = &start; /* Point to the start of the list */
while(ch=='Y' || ch=='y')
{
node->next = (struct link* )
malloc(sizeof(struct link));
node = node->next;
cout<<"\n ENTER A NUMBER : ";
cin>>node->info;
node->next = NULL;
cout<<"\n DO YOU WANT TO CREATE MORE NODES: ";
cin>>ch;
}
}
```

```cpp
void display(struct link *node)
{
node = start.next;
cout<<"\n After Inserting a node list is as follows:\n";
while (node)
{
cout<<setw(5)<<node->info;
node = node->next;
}
}
```

```cpp
void insert(struct link *node)
{
/* * Inserting a node */
int non = 0;
int pos;
node = start.next;
previous = &start;
cout<<"\n ENTER THE POSITION TO INSERT:";
cin>>pos;
while(node)
{
if((non+1) == pos)
{
New = (struct link* ) malloc(sizeof(struct link));
New->next = node ;
previous->next = New;
cout<<endl<<"\n Input the node value : ";
cin>>New->info;
break ;
}
else
{
node = node->next;
previous= previous->next;
}
non++;
}
}
```

### Output

![](img/1faaa0256577c74e8a61f42967760aa8_190_0.png)

## 7.4.5 /* Insert a Node Into a Simple Linked List Information Is Known and Put After Some Specified Node */

```cpp
#include<iostream>
#include<conio.h>
#include<stdlib.h>
using namespace std;
struct link
{
    int info;
    struct link *next;
};
struct link start, *first, *New,*before;
/* Function main */
void create(struct link *);
void display(struct link *);
void insert(struct link *);

int main()
{
    struct link *node;
    create(node);
    insert(node);
    display(node);
}
```

```cpp
void create(struct link *node) /*LOGIC TO CREATE A LINK LIST*/
{
    char ch='y';
    start.next = NULL;
    node = &start;    /* Point to the start of the list */
    while(ch =='y' || ch =='Y')
    {
        node->next = (struct link * )
        malloc(sizeof(struct link));
        node = node->next;
        cout<<"\n ENTER A NUMBER : ";
        cin>>node->info;
        node->next = NULL;
        cout<<"\n DO YOU WANT TO CREATE MORE NODES : ";
        cin>>ch;
    }
}
```

```cpp
void display(struct link *node) /*DISPLAY THE LINKED LIST*/
{
    node = start.next;
    cout<<"\n After Inserting a node list is as follows:\n";
    while (node)
    {
        cout<<setw(5)<<node->info;
        node = node->next;
    }
}
```

```cpp
void insert(struct link *node)
{
    int no= 0;
    int ins;
    node = start.next;
    before = &start;
    cout<<" \n Input value node the node you want to insert :";
    fflush(stdin);
    cin>>ins;
    while(node)
    {
        if(node->info <= ins)
        {
            New = (struct link *) malloc(sizeof(struct link));
            New->next = node;
            before->next = New;
            New->info = ins;
            break ;
        }
        else
        {
            node = node->next;
            before= before->next;
            no++;
        }
    }
}
```

### Output

```
ENTER A NUMBER : 12
DO YOU WANT TO CREATE MORE NODES: y
ENTER A NUMBER : 32
DO YOU WANT TO CREATE MORE NODES: y
ENTER A NUMBER : 85
DO YOU WANT TO CREATE MORE NODES: y
ENTER A NUMBER : 95
DO YOU WANT TO CREATE MORE NODES: y
ENTER A NUMBER : 4
DO YOU WANT TO CREATE MORE NODES: n
Input value node the node you want to insert:95
After Inserting a node list is as follows:
95 12 32 85 95 4
Process exited after 12.81 seconds with return value 0
Press any key to continue . . .
```

## 7.4.6 /* Deleting the First Node From a Simple Linked List */

```cpp
#include<iostream>
#include<conio.h>
#include<stdio.h>
using namespace std;
struct link
{
    int info;
    struct link *next;
};
struct link start,*previous,*node;
/* Function main */
void create(struct link *);
void display(struct link *);
void delet(struct link *);
int main()
{
    create(node);
    printf("\n THE CREATED LINKED LIST IS :\n");
    display(node);
    delet(node);
    printf("\n AFTER DELETING THE FIRST NODE THE LINKED LIST IS ");
    display(node);
}
```

```cpp
void create(struct link *node) /*LOGIC TO CREATE A LINK LIST*/
{
    char ch='y';
    start.next = NULL;
    node = &start; /* Point to the start of the list */
    while(ch =='y' || ch=='Y')
    {
        node->next = (struct link *) malloc(sizeof(struct link));
        node = node->next;
        cout<<"\n ENTER A NUMBER : ";
        cin>>node->info;
        node->next = NULL;
        cout<<"\n DO YOU WANT TO CREATE MORE NODES: ";
        cin>>ch;
    }
}
```

```cpp
void display(struct link *node)
{
    node = start.next; /*DISPLAY THE LINKED LIST*/
    while (node)
    {
        cout<<setw(5)<<node->info;
        node = node->next;
    }
}
```

```cpp
void delet(struct link *node)
{
    node = start.next;
    previous = &start;
    if (node == NULL)
        cout<<"\n Under flow";
    else
    {
        previous->next = node->next;
        free(node);
    }
}
```

### Output

```
ENTER A NUMBER : 12
DO YOU WANT TO CREATE MORE NODES: Y
ENTER A NUMBER : 34
DO YOU WANT TO CREATE MORE NODES: Y
ENTER A NUMBER : 65
DO YOU WANT TO CREATE MORE NODES: Y
ENTER A NUMBER : 32
DO YOU WANT TO CREATE MORE NODES: N
THE CREATED LINKED LIST IS :
12 34 65 32
AFTER DELETING THE FIRST NODE: THE LINKED LIST IS 34 65 32
Process exited after 62.4 seconds with return value 0
Press any key to continue . . .
```

## 7.4.7 /* Deleting the Last Node From a Simple Linked List */

```cpp
#include<iostream>
#include<conio.h>
#include<stdlib.h>
using namespace std;
struct link
{
    int info;
    struct link *next;
};
struct link start,*previous,*node;
/* Function main */
void create(struct link *);
void display(struct link *);
void delete(struct link *);
int main()
{
    create(node);
    printf("\n THE CREATED LINKED LIST IS :\n");
    display(node);
    delete(node);
    printf("\n AFTER DELETING THE LAST NODE THE LINKED LIST IS ");
    display(node);
}
void create(struct link *node) /*LOGIC TO CREATE A LINK LIST*/
{
