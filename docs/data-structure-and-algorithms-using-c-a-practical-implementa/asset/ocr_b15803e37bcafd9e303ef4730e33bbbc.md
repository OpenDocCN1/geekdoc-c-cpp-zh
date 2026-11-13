# Output

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

# 7.4.7 /* Deleting the Last Node From a Simple Linked List */

```
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
```