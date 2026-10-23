# 4.7 SEARCHING ELEMENT IN A DOUBLY LINK LIST

Doubly link facilitates the traversal in both the direction. For instance, we can traverse from front towards the end as well as from end towards first node. During the traversal, a node consisting of specific value can be located by matching the value held by the node. Due care is to be observed to ensure that traversal should be limited only to the number of nodes existing in the list. As soon as node consisting of the element encountered, searching should be terminated. The whole procedure is depicted in the following program.

![](bbox=[0.177, 0.251, 0.893, 0.563])

```
```cpp
//function to search an element from a doubly link list
int dlist::search(int element)
    {
        int flag=0;
        dnode *current;
        int b=count();
        current=first;
        for(int i=1;i<=b;i++)
        {
                if(current->data==element)
                {
                        flag=1;
                        break;
                }
                current=current->next;
```
```