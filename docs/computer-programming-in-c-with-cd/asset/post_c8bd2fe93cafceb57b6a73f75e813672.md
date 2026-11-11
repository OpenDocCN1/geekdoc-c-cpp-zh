
```cpp
A=B;
B=temp;
}

void main()
{
    clrscr();
    int P,Q;
    cout<<"\n Enter the numbers  :";
    cin>>P>>Q;
    swap(P,Q);
    cout<< "\n swapped numbers "<< P<<" "<<Q;
    getch();
}
```

## Q15: Write a program to declare integer pointer. Store 10 numbers in the pointer. Use new operator to allocate memory for 10 integers. Read and display the numbers (Mumbai University, December 2008)

Ans:

```cpp
#include<iostream.h>

#include<conio.h>

void main()
{
    clrscr();
    int* A = new int[10];
    int* B=A;

    cout<<"Enter any ten numbers"<<endl;
    for(int I=1;I<=10;I++, A=A+2)
    cin>>*A;
    A=B;
    for(int I=1;I<=10;I++, A=A+2)
    cout<<" "<<*A;

    getch();
}
```

## Q16: How will you declare & initialize a pointer? Write a program for interchange (Swap) two variable using pointers (Mumbai University, May 2009)

Ans:

```cpp
#include<iostream.h>
void main()
{
 int * A= new int;
 int * B= new int;
 *A=10;
 *B=20;
 int * Temp=A;
 A=B;
 B=Temp;
 cout << "A=" << *A << " B=" << *B;
 }
```

## Q17: Develop a class for linked list (Dynamic data structure) with the following member functions to carryout the following.

- i. Create a linked list to store set of integer data
- ii. Display the Linked list
- iii. Insert a node containing data in a sorted list
- iv. Delete a node from the list containing a specific data

Use object as node rather than using a struct variable to model a node

Ans:

```cpp
#include<iostream.h>
#include<conio.h>
#include<ctype.h>

class dnode
// Class for defining a node
{
 public:
 dnode * ulink;
 // Link to the upper node
 int num;
 // Data to be stored
 dnode * llink;
 // Link to the lower node
};

class dllist
{
 dnode * head1, * head2;
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
 head1=head2=NULL;    // Initializing head1 and head2 to NULL
 n =0 ;              // Initializing n to 0
}

void dllist :: create() // To create doubly link list
{
 head1 = new dnode;     // Creating a new node of type dnode and point it by head1
 dnode * ptr = head1;   // Create a pointer ptr pointing to the node pointing by head1
 ptr->ulink = NULL;      // Assign NULL to ptr upper node link
 char choice;

 do
 {
   cout<<"\n\n Enter data   ";
   cin>>ptr->num;       // Take the data in the node pointed by ptr
   ++n;
   //Increase the counter
   dnode * p = new dnode;
   // Create a new node of type dnode pointed by p
   ptr->llink = p ;
   // Assign address of node pointed by p to ptr llink
   p->ulink = ptr;
   // Assign address of node pointed by ptr to p ulink
   ptr = p;            // Now assign p to ptr
   cout<<"\n Continue Y/N ";
 }while(toupper(choice = getche()) != 'N');
 // Execute the loop until user press 'N'

 head2= ptr->ulink;  // Assign head2 to the node pointed by ptr->ulink
 head2->llink = NULL; //Assign head2->llink to NULL

 delete (ptr);  // This will remove the memory pointed by ptr
}

void dllist :: display()    // To display the contents of linked list
{
 dnode * ptr = head1;     // Assign ptr to node pointed by head1

 while(ptr != NULL)      // while ptr does not point to NULL location
 {
   cout<<"   "<<ptr->num;   // Display the content
   ptr= ptr->llink;        // Go to the next node by ptr->llink
 }
}

void dllist:: sort()   // To sort the link list
{
 dnode * dptr = head1;
 // Create dptr and point it to the node pointed by head1
 do
 {
   dnode * ptr = head1;
   // Create ptr and point it to the node pointed by head1

   dptr=dptr->llink;
   // Increase dptr to next node
   // dptr is use for the outer loop
   while(ptr->llink != NULL)
   // while ptr does not point to NULL location
   {
      if(ptr->num > ptr->llink->num)  //If the content of ptr is greater than content of next node
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
 dnode * ptr = head1;         // Create ptr and assign head1 to it
 dnode * p = new dnode;      // Create a new node of type dnode and point it by p
 p->num=no;           //Take the element
 p->llink = NULL;     // Initialize both the links of the node to NULL
 p->ulink = NULL;

 while((no > ptr->num)&&(ptr != NULL))
 // while the element to be inserted is greater
   ptr = ptr->llink;       // then the element of the node pointed by p and ptr is not equal to NULL
                           // then assign ptr->llink to ptr

 p->llink = ptr;      // Assign ptr to p->llink
 if(ptr->ulink == NULL)        // If the node to be inserted is inserting at the first position
 {
    head1 = p;              // Assign head1 to p
    p->ulink = NULL;
 }
 else                    // else insert the node in
                        // between and adjust the pointers
 {
    p->ulink = ptr->ulink;
    ptr->ulink = p;
    p->ulink->llink = p;
 }
}

void dllist :: delete()
// To delete a node from the link list
{
 int no;
 cout << "\n Enter the number you want to delete ";
 cin >> no;             // Take the element to be deleted

 dnode* ptr = head1;    // Assign ptr to head1

 while((no != ptr->num) && (ptr != NULL))
 // while the no is not equal to the element of the node
   ptr = ptr->llink;
 // Increase ptr to the next location

 if(ptr->ulink == NULL)
 // If it is the first node
 {
    head1 = ptr->llink;
    // Assign head1 to the second node
    head1->ulink = NULL;        // Assign its upper link to null
 }
 else if(ptr->llink == NULL)     // If it is the last node
 {
    head2 = ptr->ulink;         // Assign head2 to the second last node
    head2->llink = NULL;        // Assign its lower link to null
 }
 else                    // else adjust the pointers
 {
    ptr->ulink->llink = ptr->llink;
    ptr->llink->ulink = ptr->ulink;
 }

 void main()
 {
   clrscr();
   dllist link;       //Creating a object of type dllist
   link.create();     // Calling create function
   cout<<"\n Data stored in the doubly linked list are : \n";
   cout<<endl;
   link.display();    // Calling display function
   cout<<"\n press any key to continue? ";
   getch();
   link.sort();       // Calling sort function
   cout<<endl;
   cout<<"\n Data stored in the doubly linked list in ascending order\n ";
   cout<<endl;
   link.display();    // Calling display function
   cout<<"\n press any key to continue? ";
   getch();
   link.insert();     // Calling insert function
   cout<<endl;
   cout<<"\n Data stored in the doubly linked list after insertion of data\n\n";
   link.display();
   cout<<"\n press any key to continue? ";
   getch();
   link.delet();      // Calling delet function
   cout<<endl;
   cout<<"\n Data stored in the doubly linked list after deletion of data\n\n";
   link.display();
   cout<<"\n\n press any key to terminate program execution?" ;
   getch();
 }
}
```

## Q18: Design a structure named employee to print names and no.s of employee who have 5 years or more experience & salary less than Rs.10,000 using array of structure (Name, No. Exp & Salary) (Mumbai University. May 2009)

Ans:

```cpp
#include<iostream.h>
struct employee
{
   char Name[30];
   int No;
   int Exp;
   int Salary;
};

void main()
{
   employee Emprec[200];
   int N;
   cin>>N;

   for(int I=0; I<N; I++)
   {
         cin>> Emprec[I].Name>> Emprec[I].No;
         cin>> Emprec[I].Exp>> Emprec[I].Salary;
   }
   cout<<endl;

   for(int J=0; J<N; J++)
   if((Emprec[J].Exp>=5)&&(Emprec[J].Salary<10000))
   cout<< Emprec[J].Name<<"     "<< Emprec[J].No<<endl;
}
```

## Q19: An education institution wishes to maintain a database of its employees. The database is divided into a number of classes, as shown below. Specify all the classes and define functions to create a database and retrieve individual information as and when required. Assume necessary data (Mumbai University. December 2008)
