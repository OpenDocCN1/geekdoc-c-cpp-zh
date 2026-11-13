```
```cpp
//driver program
int main()
{
    struct student *node;
    create(node);    //create the link list
    int opt;
    //infinite loop
    while(1)
    {
        //display the menu
        cout<<endl<"1. Add Friend \n2. Display
        friends\n8. Print Average age of friends\n 9. Print Male
        Friends\n0. Exit\n";
        cout<<"Enter choice";
        cin>>opt;    //read the choice
        //call to the corresponding methods according
        to the users input
        if(opt==1)
        insert(node);
        else
        if(opt==2)
        display(node);
        else
        if(opt==8)
        average(node);
        else
        if(opt==9)
        printmale(node);
        else
        if(opt==0)
        exit(0);
        else
        cout<<endl<<"Invalid choice";
    }
}
//create method read the data from file and stores it into
link list
void create(struct student *node)
{
    int n;
    char ch;
    string name;
    string next = NULL;   //* Empty list */
    node = &start;    //* Point to the start of the list */
    while(1)
    {
        //allocate memory for a node of list
```
```