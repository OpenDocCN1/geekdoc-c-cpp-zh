```
fflush(stdin);
scanf("%d",&node->expo);
node->next = NULL;
fflush(stdin);
printf("\nDO YOU WANT TO CREATE MORE
NODES[Y/N] ");
scanf("%c",&ch);
i++;
}
printf("\nNUMBER OF NODES = %d\n", i);
}
```

```
void display(struct link *node)
{
    node = &start;
    node = node->next;
    printf("%d",node->coef); // PRINTING THE FIRST
    ELEMENT
    printf("%d",node->expo);
    node=node->next;
    while(node)
    {
        printf("+ %d", node->coef);
        printf("X^%d", node->expo);
        node = node->next;
    }
}
```

```
void main()
{
    struct link *node;
    create(node);
    display(node);
}
```

# 7.9.3 Program for Linked Queue

```
#include<stdio.h>
#include<iostream>
using namespace std;
struct Q
{
    int info;
    struct Q *next;
};
struct Q *front,*rear,*New;
```