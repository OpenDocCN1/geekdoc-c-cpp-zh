```
```cpp
    }
    }

void dllist :: swapdown (int r ,int m)
// Here r is the parent node number and
// m is the last node number upto which this will work
{
    int done =0;
    int c;
    c = 2 * r;

    while((!done)&& (c <= m))
    {
        dnode * parent = head1;
        // Assign parent pointer to head1
        dnode * child = head1;
        // Assign child pointer to head1

        int i = 1;
        while((i<r) && (parent->llink != NULL) )
        // This loop will take parent pointer to that node whose
        // number is 'r'
        {
            ++i;
            parent=parent->llink;
        }
        i=1;
        while((i<c ) && (child->llink != NULL))
        // This loop will take child pointer to that node whose
        // number is c
        {
            ++i;
            child=child->llink;
        }

        if(( c < m ) && ( child->num < child->llink->num))
        {
            c= c+1;
            child=child->llink;
        }

        if(child->num > parent->num)
        // If child node element is greater then parent node
        // element
```
```