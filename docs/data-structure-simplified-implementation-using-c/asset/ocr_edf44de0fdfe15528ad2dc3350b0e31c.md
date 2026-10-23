By meticulous implementation of the logic, second and third conditions (insertion in between and last) can be merged into one. We have implemented the program considering all the insertion positions. Complete implementation has been depicted in the following program:

![](bbox=[0.18, 0.17, 0.91, 0.48])

```
//function to insert the node at a specific location. This function, takes two arguments, one is the position where the node is to be inserted and the second is the elements value that need to be inserted in a doubly link list.
void dlist::insert(int pos, int el)
{
    int b=count();    //finding out the number of nodes
    cout<<"Length of list :"<<b<<endl;
    if(pos<=b+1) //checking insert location is less than length+1
    {
        cout<<"Inserting "<<el<<" at position"<<pos<<endl;
        node *current,*forward,*temp; //pointer for first and next
        current=first;
        temp=new dnode;
        temp->data=el;
        temp->next=temp->prev=NULL;
        if(pos==1) //checking the first position
```