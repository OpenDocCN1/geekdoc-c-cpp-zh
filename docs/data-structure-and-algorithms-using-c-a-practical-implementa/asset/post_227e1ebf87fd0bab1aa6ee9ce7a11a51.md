
```cpp
front = front + 1;
}
void display()
{
    int i;
    if (front == -1)
    cout<<"\n EMPTY QUEUE";
    else
    {
    cout<<"\n THE QUEUE ELEMENTS ARE";
    for(i = front ; i <= rear; i++)
    cout<<"\t"<<q[i];
    }
}
int main()
{
    int opt;
    cout<<"\n Enter the size of the QUEUE";
    cin>>size;
    q = (int *)malloc(size * sizeof(int));
    while(1)
    {
    cout<<"\n Enter the choice";
    cout<<"\n 1. INSERT 2. DELETE 3. DISPLAY 0. EXIT";
    cin>>opt;
    if(opt == 1)
    {
    cout<<"\n Enter the number to insert";
    cin>>opt;
    insert(opt);
    }
    else
    {
    if(opt == 2)
    Delete();
    else
    if(opt == 3)
    display();
    else
    if(opt == 0)
    exit(0);
    else
    cout<<"\n INVALID CHOICE";
    }
    }
}
```

## Output

```
Enter the size of the QUEUE
4
Enter the choice
1. INSERT 2. DELETE 3. DISPLAY 0. EXIT
1
Enter the number to insert
23
Enter the choice
1. INSERT 2. DELETE 3. DISPLAY 0. EXIT
1
Enter the number to insert
43
Enter the choice
1. INSERT 2. DELETE 3. DISPLAY 0. EXIT
1
Enter the number to insert
65
Enter the choice
1. INSERT 2. DELETE 3. DISPLAY 0. EXIT
1
Enter the number to insert
?77
Enter the choice
1. INSERT 2. DELETE 3. DISPLAY 0. EXIT
1
Enter the number to insert
88
QUEUE OVERFLOW
Enter the choice
1. INSERT 2. DELETE 3. DISPLAY 0. EXIT
3
THE QUEUE ELEMENTS ARE 23 43 65 ?77
Enter the choice
1. INSERT 2. DELETE 3. DISPLAY 0. EXIT
2
Element deleted : 23
Enter the choice
1. INSERT 2. DELETE 3. DISPLAY 0. EXIT
2
Element deleted : 43
Enter the choice
1. INSERT 2. DELETE 3. DISPLAY 0. EXIT
2
Element deleted : 65
Enter the choice
1. INSERT 2. DELETE 3. DISPLAY 0. EXIT
2
Element deleted : ?77
Enter the choice
1. INSERT 2. DELETE 3. DISPLAY 0. EXIT
2
Underflow
Enter the choice
1. INSERT 2. DELETE 3. DISPLAY 0. EXIT
0
Process exited after 22.92 seconds with return value 0
Press any key to continue . . .
```

## 2. CIRCULAR QUEUE OPERATIONS

```cpp
#include<iostream>
#include<iomanip>
using namespace std;
/body of class
class CircularQueue
{
    private : //declare data members
        int front,rear,size,cq;
    public:
        CircularQueue(int); //constructor
        //method declarations
        void Enqueue(int);
        void Dequeue();
        void Print();
        bool isEmpty();
        bool isFull();
        void Clear();
        int getRear();
        int getFront();
};
//body of constructor
CircularQueue :: CircularQueue(int n)
{
    size= n;
    front=-1; //initialize front
    rear=-1; //initialize rear
    cq = new int[size]; //allocate memory for circular queue
}
//method will return the value of rear
int CircularQueue :: getRear()
{
    return rear;
}
//method will return the value of front
int CircularQueue :: getFront()
{
    return front;
}
//method will clear the elements of queue
void CircularQueue :: Clear()
{
    front=-1; //set front to -1
    rear=-1; //set rear to -1
}
//method will return true if circular queue is full
bool CircularQueue :: isFull()
{
    //condition for circular queue is full
    if(front==0 && rear == size-1 || front == rear+1)
    return true;
    else
    return false;
}
//method will return true if the circular queue is empty
bool CircularQueue :: isEmpty()
{
    if(front==-1) //condition for empty
    return true;
    else
    return false;
}
//method will print the elements of circular queue
void CircularQueue :: Print()
{
    int i;
    if(isEmpty()) //check for empty queue
    printf("\n CIRCULAR QUEUE IS EMPTY");
    else
    if (front > rear) //print the elements when front > rear
    {
        for(i = front; i <= size-1; i++)
        cout<<cq[i]<<setw(5);
        for(i = 0; i <= rear; i++)
        cout<<cq[i]<<setw(5);
    }
    else //print the elements from front to rear
    for(i = front; i <= rear; i++)
    cout<<cq[i]<<setw(5);
}
//method will insert an element into circular queue
void CircularQueue :: Enqueue(int n)
{
    if (isFull()) //condition for overflow
    {
    printf("\n Overflow");
    return;
    }
    if (rear == -1) /* Insert first element */
    {
        front = 0;
        rear = 0;
    }
    else
        if (rear == size-1) //if rear is at last then assign it to first
        rear = 0;
        else
            rear++; //increment the value of rear
    //assign the number into circular queue
    cq[rear] = n ;
}
//method to delete the elements from queue
void CircularQueue :: Dequeue()
{
    int ch;
    if (isEmpty()) //condition for underflow
    {
        printf("\nUnderflow");
        return ;
    }
    //print the element which is to be delete
    cout<<endl<<cq[front]<<" deleted from circular queue";
    if (front == rear) //condition for queue having single element
    {
        Clear();
    }
    else
    if ( front == size-1)
    front = 0;
    else
        front++;
}
//driver program
int main()
{
    int op,n;
    char ch;
    cout<<endl<<"Enter the size of circular queue";
    cin>>n; //ask user about the size of circular queue
    CircularQueue obj(n); //declare an object

    //infinite loop to control the program
    while(1)
    {
    cout<<endl<<"********** M E N U **********";
    cout<<endl<<"e. ENQUEUE";
    cout<<endl<<"d. Dequeue";
    cout<<endl<<"m. isEmpty";
    cout<<endl<<"u. isFull";
    cout<<endl<<"c. Clear";
    cout<<endl<<"f. Get Front";
    cout<<endl<<"r. Get Rear";
    cout<<endl<<"p. Print";
    cout<<endl<<"n. Quit";
    cout<<endl<<"Enter Choice : ";
    cin>>ch;

    //condition for enqueue()
    if(ch=='e' || ch=='E')
    {
    cout<<endl<<"Enter the number to insert";
    cin>>opt;

    obj.Enqueue(opt);
    }
    else //condition for dequeue()
    if(ch=='d' || ch=='D')
    {
    obj.Dequeue();
    }
    else //condition for call to isEmpty()
    if(ch=='m' || ch=='M')
    {
    if(obj.isEmpty())
    cout<<endl<<"Circular Queue is EMPTY";
    else
    cout<<endl<<"Circular Queue is not empty" ;
    }
    else //condition to call isFull()
    if(ch=='u' || ch=='U')
    {
    if(obj.isFull())
    cout<<endl<<"Circular Queue is FULL";
    else
    cout<<endl<<"Circular Queue is not Full" ;
    }
    else //condition to call clear()
    if(ch=='c' || ch=='C')
    obj.Clear();
    else
    if(ch=='F' || ch=='f') //condition to call getFront()
    cout<<endl<<"Front = "<<obj.getFront();
    else
    if(ch=='R' || ch=='r') //condition to call getRear()
    cout<<endl<<"Rear = "<<obj.getRear();
    else //condition to call Print()
    obj.Print();
    else //condition to terminate the program
    if(ch=='q' || ch=='Q')
    exit(0);
    else
    cout<<endl<<"Invalid Choice";
    }
}
```

## OUTPUT

```
Enter the size of circular queue
3
**********************************
****** M E N U ******
1. Enqueue
2. Dequeue
3. isEmpty
4. isFull
5. Clear
6. Get Front
7. Get Rear
8. Print
9. Quit
Enter Choice : P
CIRCULAR QUEUE IS EMPTY
**********************************
****** M E N U ******
1. Enqueue
2. Dequeue
3. isEmpty
4. isFull
5. Clear
6. Get Front
7. Get Rear
8. Print
9. Quit
Enter Choice : R
Rear = -1
**********************************
****** M E N U ******
1. Enqueue
2. Dequeue
3. isEmpty
4. isFull
5. Clear
6. Get Front
7. Get Rear
8. Print
9. Quit
Enter Choice : F
Front = -1
**********************************
****** M E N U ******
1. Enqueue
2. Dequeue
3. isEmpty
4. isFull
5. Clear
6. Get Front
7. Get Rear
8. Print
9. Quit
Enter Choice : U
Circular Queue is not Full
**********************************
****** M E N U ******
1. Enqueue
2. Dequeue
3. isEmpty
4. isFull
5. Clear
6. Get Front
7. Get Rear
8. Print
9. Quit
Enter Choice : M
Circular Queue is EMPTY
********** M E N U **********
e. ENQUEUE
d. Dequeue
m. isEmpty
u. isFull
c. Clear
f. Get Front
r. Get Rear
p. Print
q. Quit
Enter Choice : E
Enter the number to insert
12
********** M E N U **********
e. ENQUEUE
d. Dequeue
m. isEmpty
u. isFull
c. Clear
f. Get Front
r. Get Rear
p. Print
q. Quit
Enter Choice : E
Enter the number to insert
34
********** M E N U **********
e. ENQUEUE
d. Dequeue
m. isEmpty
u. isFull
c. Clear
f. Get Front
r. Get Rear
p. Print
q. Quit
Enter Choice : E
Enter the number to insert
56
********** M E N U **********
e. ENQUEUE
d. Dequeue
m. isEmpty
u. isFull
c. Clear
f. Get Front
r. Get Rear
p. Print
q. Quit
Enter Choice : E
Enter the number to insert
2
Overflow
```
