```
private :
    node*start;
public :
    link_list() //constructor
    {
        start=NULL;  //intitially the list has no node
    }
    void create (int i)
    {
        node*new_node= new node;     //create a new node
        new_node->data=i;
        new_node->next=start;     //make new node to point
                                to the first node
        start=new_node;     //make new node as the first
                        node in the list
    }
    void display(int);  //function prototype
    void insert(int,int);   //function prototype
};  //end of the class
//function definition display()
void link_list ::display(int delete_node)
{
    node*move=start;
    node*temp;
    while(move)
    {
        cout<< move->data<<"->";   //display the data
        temp=move;
        move=move->next;  //move to next node
        if(delete_node)
            delete(temp);
    }
    cout<<"NULL";
}
//function definition insert()
void link_list ::insert(int position,int data)
{
    node*move=start;
    int steps=1;
    while(steps<position-1)
```