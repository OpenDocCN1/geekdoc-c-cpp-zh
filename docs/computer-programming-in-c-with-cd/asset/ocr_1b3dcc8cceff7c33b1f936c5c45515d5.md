```
```cpp
// Creating two heads for the list
int n;
// For counting number of nodes
public:
dllist();
// Constructor for the class
void create();
//Function to create doubly linked list
void display();
// Function to display the data stored in the nodes
void sort();
// Function to sort nodes in the list depending on the data stored
void insert();
// Function to insert a node in the list
void delet();
// Function to delete a node from the list
};

dllist :: dllist()   // Constructor
{
head1=head2=NULL;    // Initializing head1 and head2 to

NULL
 n =0 ;              // Initializing n to 0
}

void dllist :: create() // To create doubly link list
{
head1 = new dnode;     // Creating a new node of type

dnode and point it by head1
dnode * ptr = head1;   // Create a pointer ptr pointing

to the node pointing by head1
ptr->link = NULL;      // Assign NULL to ptr upper node link
char choice;

do
{
cout<<"\n\n Enter data   ";
 cin>>ptr->num;       // Take the data in the node

pointed by ptr
 ++n;
//Increase the counter dnode * p = new dnode;
```
```