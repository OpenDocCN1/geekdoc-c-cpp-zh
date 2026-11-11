
```cpp
int loc , i ;

if( n < 99 ) // if array is not full
{
        for( i = 0 ; a[i] < no ; i++ ) //traverse until the location found
                loc = i ; // mark the location

        for( i = n - 1 ; i >= loc ; i-- ) //make the space for new element
                a[i+1] = a[i] ;

        a[loc] = no ; // insert the element
        n ++ ;
        return( 0 ) ; // returns indication of successful insert
}
return(1) ; // otherwise array is full

}
int dmanip :: delete1( int no )
{
        int i , loc ;
        for( i = 0 ; a[i] != no && i < n ; i++ ) // traverse to find the value
        if( i == n ) // if value not found
        {
                return( 1 ) ; // return indication of value not found
        }
        loc = i ; // mark the location
        // shift the elements to remove the desired element
        for( i = loc ; i < n - 1 ; i++ )
                a[i] = a[i+1] ;

        n -- ;
        return( 0 ) ; // indication of successful deletion

}
void dmanip :: sort() //function for bubble sort
{
        int i , j , t ;
        for( i = 0 ; i < n - 1 ; i ++ ) // loop to iterate n - 1 times
                for( j = 0 ; j < n - i ; j ++ ) //loop to iterate n-i times
                        if( a[j] > a[j+1] )
                        {
                                t = a[j] ;    // logic to interchange values
                                a[j] = a[j+1] ;
                                a[j+1] = t ;
                        }
}
void stat :: mean()
{
    int sum = 0 ;

    for( int i = 0 ; i < n ; i ++ ) //loop to iterate n times
        sum += a[i] ; // add the value of element into sum

    men = float (sum) / n ; //divide sum by the no. of elements
}
void stat :: median()
{
    sort() ; // first sort the elements of the array

    if( n % 2 == 0 ) // if array has even no. of elements
        med = a[n/2] + a[n/2 + 1] / 2.0 ;
    else      // if array has odd no. of elements
        med = a[n/2 + 1] ;
}
void stat :: stddev()
{

    mean() ; // first count the mean
    float am = men ;
    int sum = 0 ;

    for( int i = 0 ; i < n ; i ++ ) // loop to calculate the sum of differences
        sum += ( am - a[i] ) * ( am - a[i] ) ;

    sdev = sqrt( sum ) ; // take the square root of the sum

}
void stat :: mode()
{

    int i , max = 0 , j , count , loc = 0 ;

    for( i = 0 ; i < n - 1 ; i ++ ) // loop to iterate n - 1 elements
    {
        count = 0 ; // initialize the count to 0 to count each element

        for( j = i ; j <= n ; j ++ ) // loop to count the occurrence
        {
            if( a[i] == a[j] ) // if match occurs then add counter
                count ++ ;
        }

        if( max < count ) // if element appears more than previous max
        {                  // then replace the max
            max = count ;
            loc = i ;
        }
    }

    mod = a[loc] ; // store the value at location i to mod

}

void stat :: display()
{
    // displays the counted variables
    cout << "\nmean   :  " << men ;
    cout << "\nmedian :  " << med ;
    cout << "\nmode   :  " << mod ;
    cout << "\nstandard deviation :  " << sdev ;
}

void main()
{
    stat s ; // declare the variable of derived class

    clrscr() ;
    s.input() ; //call to input function of parent class
    s.mean() ; // call to mean function of derived class
    s.mode() ; // call to mode function of derived class
    s.stddev() ; // call to stddev function of derived class
    s.median() ; // call to median function of derived class
    s.display() ; //call to overridden display function of derived class
    getch() ;

}
```

## Q45

Develop a friend function to carryout multiplication between two conformable matrices stored in a single dimensional array variables as a private member of class ‘Onedim’. The result of multiplication needs to be stored in a two dimensional array variable as a private member of class ‘Twodim’. Incorporate suitable member functions both in class Onedim and class Twodim for reading this matrix and display of matrix.

One of the single dimensional array variables can hold matrix in column wise and other row wise. Also develop main program to reference the friend function.

Ans:

```cpp
#include<iostream.h>
#include<conio.h>

class Beta;
class Alpha
{
    int M,L,N;
    int A[100];
    int B[100];
public :

    void InputArray()
    {
        cin>>M>>L>>N;

        for(int i=1;i<=M*L;i++)
        cin>>A[i];
        cout<<endl;
        for( i=1;i<=L*N;i++)
        cin>>B[i];
    }
    friend void matmult(Alpha &obja,Beta &Objb);
};

class Beta
{
    int C[10][10];
    int M,N;

Beta Bobj;
Aobj.InputArray();
matmult(Aobj,Bobj);
Bobj.DisplayMatrix();
getche();
}
```

## Q46

Write a program to input in information of student's for eg: Student Roll Number, Student Name, Marks in Maths, Physics, Chemistry. Find the total marks for each student. In the student class make a function to sort students according to the total marks[ascending order]. If the total marks of two students are equal then it will decide the merit rank depending first on the marks obtained in Maths, then Physics. If total marks in all the three subjects and Maths and Physics are equal, it then means that chemistry is also equal. In that case, final decision is to be taken based on the roll number of the student. Also, the program is to be implemented in singly linked lists.

Ans:

```cpp
#include<iostream.h>
#include<conio.h>
#include<stdlib.h>
#include<ctype.h>
#include<string.h>

class student  //defining a class by the name student
{
    public: //All the functions or members below this declaration are public
    char name[10];
    int rollno,m1,m2,m3,t;
}; /* The semicolon after the class declaration is an important thing. Data
   constructs such as structures and classes end with a semicolon, while
   control constructs such as functions and loops do not. */

class node  //defining a class by the name node
{
    public: //All the members below this declaration are public
    student data;
    node *link; //link is pointer variable pointing to a node
}; //As explained above for the semicolon after the class declaration

class marklist
{
    node *head; //head is a pointer variable pointing to a node
    public: //All the functions below this declaration are public
    marklist();
    void input();
    void insert();
    void del();
    void sort();
    void push();
    void pop();
    void display();
};

marklist::marklist()  /* Example of a constructor, with the same name as the
class, which is used for initialization */
{
    head=NULL; /*Making the head point to the head of a linked list, by making
    its first link point to NULL */
}

void marklist::input()
{
    head = new node;
    node *ptr=head;
    node *back;
    char ch;
    do
    {
        cout<<"\nEnter roll no,name,marks of 3 subjects:\n";
        cin>>ptr->data.rollno>>ptr->data.name>>ptr->data.m1>>ptr->data.m2>>ptr->data.m3;
        ptr->data.m1+ptr->data.m2+ptr->data.m3;
        node *p=new node;
        ptr->link=p;
        back=new node;
        back=ptr;
        ptr=p;
        cout<<"\nEnter another (Y/N):";
        cin>>ch;
    }while(toupper(ch)!='N'); /*Process will repeat that is the user can keep
    on inputting values until the user inputs N as his choice */
    back->link=NULL;
    delete(ptr);
    display();
}

void marklist::display()
{
    node *ptr=head;
    cout<<"\n\nEntered information is :";
    cout<<"\nRollNo\tName\tFirst subject\tSecond subject\tThird subject\tTotal";
    do
    {
        cout<<"\n";
        cout<<"\n\t"<<ptr->data.rollno<<"\t"<<ptr->data.name<<"\t"<<ptr->data.m1<<"\t"<<ptr->data.m2<<"\t"<<ptr->data.m3<<"\t"<<ptr->data.t;
        ptr=ptr->link;
    }while(ptr!=NULL);
}
void marklist::insert()
{
    char name[10];
    int rollno,m1,m2,m3,t;
    node *ptr=head;
    node *p=new node;
    cout<<"\nEnter roll no,name,marks of 3 subjects:\n";
    cin>>rollno>>name>>m1>>m2>>m3;
    t=m1+m2+m3;
    strcpy(p->data.name,name);
    p->data.rollno=rollno;
    p->data.m1=m1;
    p->data.m2=m2;
    p->data.m3=m3;
    p->data.t=t;

    node *back=NULL;
    while((rollno>ptr->data.rollno)&&(ptr!=NULL))
    {
        back=ptr;
        ptr=ptr->link;
    }
    p->link=ptr;
    if(back==NULL)
        head=p;
    else
        back->link=p;
    display();
}
```
