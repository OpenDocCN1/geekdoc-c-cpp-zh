```
```cpp
}

void dll::display() //Function for displaying the values
{
    dnode *ptr;
    ptr=h1; /*out of the two heads, in this case the pointer is pointing to
    h1, from where we will begin to display the values */
    while(ptr!=NULL) //until there is no further node to point to
    {
        cout<<endl<<"\t"<<ptr->data<<endl; //Display the data field of the node
        ptr=ptr->flink;//Move the pointer to the next node whose data is to be
        displayed.
    }
    getch();
}

void dll::swapdown(int r,int m) //Function to swapdown as described in the
    earlier program
{
    int done=0,c=2*r; //Setting a flag to check whether the sort is done or
    not
    dnode *ptr; //A pointer pointing to nodes
    while ((!done)&&(c<=m)) /*Repeat the loop until the heap is not completely
    swapped down    */
    {
            dnode **ptr=h1;
            ptr=h1;
            for(int i=1;i<c;i++)
                    ptr=ptr->flink;

            for(i=1;i<r;i++)
                    ptr=ptr->flink;

            if((c<=m)&&(ptr->data<ptr->flink->data))
            {
                    ptr=ptr->flink;
                    c++;
            }
            if(ptr->data>ptr->data)
            {
                    int t=ptr->data;
                    ptr->data=ptr->data;
                    ptr->data=t;
                    r=c;

                    /*when you disturb a heap, you need to repeat the procedure for all
                    heaps below it, since even they get disturbed. */
                    c=2*r; //Determining the child node for each parent node

```