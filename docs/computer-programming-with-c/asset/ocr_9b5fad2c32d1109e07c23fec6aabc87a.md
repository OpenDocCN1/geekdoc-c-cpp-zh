```
```cpp
Node *next;
    void insert(Employee x)
    {
        if(head ==NULL)
        {
        /*Node to be inserted is the first node*/
        head= new Node;
        head->data=x;
        head->next=NULL;
        }
        else
        {
        /*Node to be inserted is the subsequent node*/
        Node *d = new Node;
        d->data=x;
        d->next=NULL;
            Node *temp;
        temp=head;

            while(temp->next !=NULL)
            {
            temp = temp -> next;
            }
        temp->next=d;
        }
    }
    void traverse()
    {
    Node *temp;
    temp=head;
    cout<<"The elements of the linked list are as below:"<<endl;
    /*Traverse the list until it ends*/
            while(temp!=NULL)
            {
            temp->data.output();
            temp = temp -> next;
            }
    }
    void remove(int id)
    {
    Node *temp;
    temp=head;
    Node *prev=NULL;
```
```