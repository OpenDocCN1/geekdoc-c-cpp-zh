

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

## Q15：编写一个程序，声明整型指针。在指针中存储10个数字。使用new运算符为10个整数分配内存。读取并显示这些数字（孟买大学，2008年12月）

答案：

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

## Q16：如何声明和初始化指针？使用指针编写一个交换两个变量的程序（孟买大学，2009年5月）

答案：

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

## Q17：为链表（动态数据结构）开发一个类，包含以下成员函数以执行以下操作。

- i. 创建一个链表来存储一组整数数据
- ii. 显示链表
- iii. 在已排序的链表中插入一个包含数据的节点
- iv. 从链表中删除一个包含特定数据的节点

使用对象作为节点，而不是使用结构变量来模拟节点

答案：

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

## Q18：设计一个名为employee的结构，使用结构数组打印工龄5年及以上且薪金低于Rs.10,000的员工的姓名和编号（姓名、编号、工龄和薪金）（孟买大学，2009年5月）

答案：

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

## Q19：一所教育机构希望维护其员工的数据库。该数据库分为若干类，如下所示。请指定所有类，并定义函数以创建数据库，并在需要时检索个人相关信息。假定必要的数据（孟买大学，2008年12月）

