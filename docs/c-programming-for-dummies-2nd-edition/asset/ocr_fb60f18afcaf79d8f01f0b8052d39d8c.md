Listing 20-6 could use some cleaning. Functions scream at me, so I'll heed their cries with an improved version of the code, shown in Listing 20-8.

# LISTING 20-8: A Better Linked-List Example

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define ITEMS 5

struct stk {
    char symbol[5];
    int quantity;
    float price;
    struct stk *next;
};

struct stk *make_structure(void);
void fill_structure(struct stk *a,int c);
void show_structure(struct stk *a);

int main()
{
    struct stk *first;
    struct stk *current;
    int x;

    /* create the ITEMS-sized linked list */
    for(x=0;x<ITEMS;x++)
    {
        if(x==0)
        {
            first=make_structure();
            current=first;
        }
        else
        {
            current->next=make_structure();
            current=current->next;
        }
        fill_structure(current,x+1);
    }
    /* cap the list */
    current->next=NULL;
```