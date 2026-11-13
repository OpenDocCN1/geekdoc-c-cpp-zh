```
}

previous->next = node->next;
free(node);
}
```

# Output

```
ENTER A NUMBER : 43
DO YOU WANT TO CREATBE MORE NODES: Y
ENTER A NUMBER : 65
DO YOU WANT TO CREATBE MORE NODES: Y
ENTER A NUMBER : 87
DO YOU WANT TO CREATBE MORE NODES: Y
ENTER A NUMBER : 23
DO YOU WANT TO CREATBE MORE NODES: Y
ENTER A NUMBER : 44
DO YOU WANT TO CREATBE MORE NODE: N
THE CREATED LINKED LIST IS :
AFTER DELETING THE LAST NODE THE LINKED LIST IS   43 65 87 23
Process exited after 15.62 seconds with return value 8
Press any key to continue . . .
```

# 7.4.8 /* Deleting a Node From a Simple Linked List When Node Number Is Known */

```
#include<iostream>
#include<conioap>
#include<ctdlib.h>
using namespace std;
struct link
{
    int info;
    struct link *next;
};
struct link start, *previous,*node;
/* Function main */
void create(struct link *);
void display(struct link *);
void delet(struct link *);

int main()
{
```