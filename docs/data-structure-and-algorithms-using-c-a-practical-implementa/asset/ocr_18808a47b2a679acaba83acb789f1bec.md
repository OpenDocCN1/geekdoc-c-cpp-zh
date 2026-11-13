```
while(node)
{
    if(n == pos)
    {
        previous->next = node->next;
        free(node);
        break ;
    }
    else
    {
        node = node->next;
        previous = previous->next;
    }
    n++;
}
}
```

# OUTPUT

```
ENTER A NUMBER : 45
DO YOU WANT TO CRETATE MORE NODES: Y
ENTER A NUMBER : 32
DO YOU WANT TO CRETATE MORE NODES: Y
ENTER A NUMBER : 95
DO YOU WANT TO CRETATE MORE NODES: Y
ENTER A NUMBER : 25
DO YOU WANT TO CREATE MORE NODES: N
THE YOU CREATED LINKED LIST IS :
45 32 95 25
Input node number you want to delete:3
AFTER DELETION THE INKED LIST IS 45 32 25
Process exited after 14.11 seconds with return value 0
Press any key to continue . . .
```

# 7.4.9 Deleting a Node From a Simple Linked List When Information of a Node Is Given

```
#include<iostream>
#include<conio.h>
#include<stdio.h>
using namespace std;
struct link
```