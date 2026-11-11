```
```cpp
if(ptr->num > ptr->llink->num)  //If the

content of ptr is greater than content of next node
{
        int temp = ptr->num;
        ptr->num = ptr->llink->num;
        ptr->llink->num= temp;
}
                        ptr=ptr->llink;        // Point ptr to the next node
                }
}while(dptr->llink != NULL); // while dptr does not point to NULL location
}
void dllist :: insert()    // To insert a node in link list
{
        int no;
        cout<<"\n Enter the number you want to Insert ";
        cin>>no;             //Take the element to be added
dnode * ptr = head1;         // Create ptr and assign head1

to it
dnode * p = new dnode;      // Create a new node of type

dnode and point it by p
        p->num=no;           //Take the element
        p->llink = NULL;     // Initialize both the links of

the node to NULL
        p->rlink = NULL;

        while((no > ptr->num)&&(ptr != NULL))
        // while the element to be inserted is greater
                                ptr = ptr->llink;       // then the

element of the node pointed by p and ptr is not equal to

NULL

                                                // then

assign ptr->link to ptr

        p->llink = ptr;      // Assign ptr to p->llink
        if(ptr->ulink == NULL)        // If the node to be

inserted is inserting at the first position
        {
```
```