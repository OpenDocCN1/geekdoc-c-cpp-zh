OUTPUT :
Linked list of integer
10->20->30->
Linked list of character
A->B->C->E->
Linked list of string
Hari->Mohan->Pandey->Lecturer
Linked list of float
123.456->34.56->456.67->4532.895->

EXPLANATION : The program is similar to the previous one with the difference that we have here made a class template which will be instantiated 4 times for different types. That is L represent a link list of integer, L1 a linked list of characters, L2 a linked list of strings and L3 a linked list of floats.

```
/*PROG 13.19 TEMPLATE BASED LINKED LIST WITHOUT USING STRUCTURE AS A NODE */
#include <iostream.h>
template <class LIST>
class Linkelist
{
    LIST data;
    linklist*next;
public :
    linklist(LIST num)
    {
        data=num;
        next=NULL;
    }
    void add_node(linklist*node)
    {
        node->next=this;
        this->next=NULL;
    }
    linklist *getnext()
    {
        return next;
    }
    LIST getdata()
    {
        return data;
    }
};
```