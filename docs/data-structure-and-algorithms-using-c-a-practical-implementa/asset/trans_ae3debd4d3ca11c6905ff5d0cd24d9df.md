

```
**************** M E N U ****************
e. ENQUEUE
d. Dequeue
m. isEmpty
u. isFull
c. Clear
f. Get Front
r. Get Rear
p. Print
q. Quit
Enter Choice : P
12
34
56
**************** M E N U ****************
e. ENQUEUE
d. Dequeue
m. isEmpty
u. isFull
c. Clear
f. Get Front
r. Get Rear
p. Print
q. Quit
Enter Choice : D

12 deleted from circular queue
**************** M E N U ****************
e. ENQUEUE
d. Dequeue
m. isEmpty
u. isFull
c. Clear
f. Get Front
r. Get Rear
p. Print
q. Quit
Enter Choice : P
56
****** M E N U ******
e. ENQUEUE
d. Dequeue
m. isEmpty
u. isFull
c. Clear
f. Get Front
g. Get Rear
p. Print
q. Quit
Enter Choice : U
Circular Queue is not Full

****** M E N U ******
e. ENQUEUE
d. Dequeue
m. isEmpty
u. isFull
c. Clear
f. Get Front
g. Get Rear
p. Print
q. Quit
Enter Choice : M
Circular Queue is not empty

****** M E N U ******
e. ENQUEUE
d. Dequeue
m. isEmpty
u. isFull
c. Clear
f. Get Front
g. Get Rear
p. Print
q. Quit
Enter Choice : E
Enter the number to insert 34

****** M E N U ******
e. ENQUEUE
d. Dequeue
m. isEmpty
u. isFull
c. Clear
f. Get Front
g. Get Rear
p. Print
q. Quit
Enter Choice : E
Enter the number to insert 77

****** M E N U ******
e. ENQUEUE
d. Dequeue
m. isEmpty
u. isFull
c. Clear
f. Get Front
g. Get Rear
p. Print
q. Quit
Enter Choice : P
56 34 77
**************** MENU ****************
a. ENQUEUE
d. DEQUEUE
m. isEmpty
u. isFull
c. Clear
f. Get Front
b. Get Rear
t. Traverse
s. Count
q. Quit
Enter Choice : C
**************** MENU ****************
a. ENQUEUE
d. DEQUEUE
m. isEmpty
u. isFull
c. Clear
f. Get Front
b. Get Rear
t. Traverse
s. Count
q. Quit
Enter Choice : D
**************** MENU ****************
a. ENQUEUE
d. DEQUEUE
m. isEmpty
u. isFull
c. Clear
f. Get Front
b. Get Rear
t. Traverse
s. Count
q. Quit
Enter Choice : Q
Process exited after 203.3 seconds with return value 0
Press any key to continue . . .
```

## 3. 循环队列插入、删除、搜索和遍历操作程序

```cpp
#include<iostream>
using namespace std;
//structure of class cqueue
class cqueue
{
	private:
		int front,rear,cnt,queue[10];
	public:
		cqueue(); //constructor
		void enqueue(); //prototype of enqueue()
		int dequeue(); //prototype of dequeue()
		int count(); //count the number of elements in queue
		void traverse(); //traverse the queue elements
		bool search(int); //search an element in circular queue
};
```

```cpp
cqueue :: cqueue()
{
	front=-1; //assign -1 to front and rear for empty queue
	rear=-1;
	cnt=0; //set 0 to count
}
```

```cpp
//method to insert an element into the queue
void cqueue :: enqueue()
{
	//condition for overflow
	if(front == 0 && rear==9 || front == rear+1)
	{
		cout<<endl<<"OVERFLOW";
	}
	else
	{
		if(rear==-1) //condition for queue does not having any element
		{
			front=0; //set the front and rear to 0
			rear=0;
		}
		else
		if(rear==9 && front!=0) //condition for rear at last but queue having empty space
		{
			rear=0;
		}
		else
		{ //increase the rear for insertion
			rear++;
		}
		//insert an element into the queue
		cout<<endl<<"Enter an element to insert into queue";
		cin>>queue[rear];
	}
}
```

```cpp
//method to delete an element from queue
void cqueue :: dequeue()
{
	if(front==-1) //condition for underflow
	{
		cout<<endl<<"UNDERFLOW";
	}
	else
	{
		//print the element to delete
		cout<<endl<<queue[front]<<" deleted from queue";
		//set the front
		if(front==rear) //queue having single element
		{
			front=-1;
			rear=-1;
		}
		else
		{
			if(front==9) //condition for front is at last
				front=0;
			else
				front=front+1; //increase the front
		}
	}
}
```

```cpp
//method to traverse the queue
void cqueue :: traverse()
{
	int i;
	if(front==-1) //condition for empty queue
	{
		cout<<endl<<"EMPTY QUEUE";
	}
	else
	{
		if(front > rear) //condition for front is greater than rear
		{
			for(i=front;i<=9;i++) //print the elements from front to last
				cout<<queue[i]<< " ";
			for(i=0;i<=rear;i++) //print the elements from 0 to rear
				cout<<queue[i]<< " ";
		}
		else
		{
			for(i=front;i<=rear;i++) //print the elements from front to rear
				cout<<queue[i]<< " ";
		}
	}
}
```

```cpp
//method to count the number of elements in queue
int cqueue :: count()
{
	int i;
	cnt=0;
	if(rear==-1) //condition for queue does not having element
		return cnt;//return cnt as 0
	else
	if(front > rear) //condition having front greater than rear
	{
		for(i=front;i<=9;i++) //count number of elements from front to last
			cnt++;
		for(i=0;i<=rear;i++) //count the elements from 0 to rear
			cnt++;
	}
	else
		for(i=front;i<=rear;i++) //count the elements from front to rear
			cnt++;
	return cnt; //return count
}
```

```cpp
//method to search an element in queue
bool cqueue :: search(int n)
{
	int i;
	if(rear==-1) //if queue does not having any element then return false
		return false;
	if(front > rear) //condition having front greater than rear
	{
		for(i=front;i<=9;i++)//search number of elements from front to last
			if(n==queue[i])
				return true;
		for(i=0;i<=rear;i++)//search the elements from 0 to rear
			if(n==queue[i])
				return true;
	}
	else
		for(i=front;i<=rear;i++)//search the elements from front to rear
			if(n==queue[i])
				return true;
	return false;
}
//driver program
```

```cpp
int main()
{
	int opt,n;
	cqueue obj;
	cout<<endl<<"***********************************************\n";
	cout<<endl<<"CIRCULAR QUEUE OPERATIONS";
	cout<<endl<<"***********************************************\n";
	//loop to operate the operations with queue till user wants
	while(1)
	{
		//display the menu
		cout<<endl<<"1. INSERT 2. DELETE 3. COUNT 4. SEARCH 5. TRAVERSE 0. EXIT";
		cout<<endl<<"Enter your choice";
		cin>>opt; //read the choice
		if(opt==1) //Condition for insert operation
			obj.enqueue();
		else
		if(opt==2) //condition for delete operation
			obj.dequeue();
		else
		if(opt==3) //condition for count operation
			cout<<endl<<"Circular queue having "<<obj.count()<<" number of elements";
		else
		if(opt==4) //condition for search operation
		{
			cout<<endl<<"Enter an element to search";
			cin>>n;
			if(obj.search(n))
				cout<<endl<<n<<" is inside the queue";
			else
				cout<<endl<<n<<" is not inside the queue";
		}
		else
		if(opt==5) //condition for traverse operation
			obj.traverse();
		else
		if(opt==0) //condition for terminate the loop
			break;
		else //invalid option
			cout<<endl<<"Invalid choice";
	}
}
```

## 输出

```
****************************************
CIRCULAR QUEUE OPERATIONS
****************************************
1. INSERT 2. DELETE 3. COUNT 4. SEARCH 5. TRAVERSE 0. EXIT
Enter your choice 1
Enter an element to insert into queue 23
1. INSERT 2. DELETE 3. COUNT 4. SEARCH 5. TRAVERSE 0. EXIT
Enter your choice 1
Enter an element to insert into queue 24
1. INSERT 2. DELETE 3. COUNT 4. SEARCH 5. TRAVERSE 0. EXIT
Enter your choice 1
Enter an element to insert into queue 5
1. INSERT 2. DELETE 3. COUNT 4. SEARCH 5. TRAVERSE 0. EXIT
Enter your choice 1
Enter an element to insert into queue 65
1. INSERT 2. DELETE 3. COUNT 4. SEARCH 5. TRAVERSE 0. EXIT
Enter your choice 1
Enter an element to insert into queue 76
1. INSERT 2. DELETE 3. COUNT 4. SEARCH 5. TRAVERSE 0. EXIT
Enter your choice 1
Enter an element to insert into queue 87
1. INSERT 2. DELETE 3. COUNT 4. SEARCH 5. TRAVERSE 0. EXIT
Enter your choice 1
Enter an element to insert into queue 5
1. INSERT 2. DELETE 3. COUNT 4. SEARCH 5. TRAVERSE 0. EXIT
Enter your choice 1
Enter an element to insert into queue 3
1. INSERT 2. DELETE 3. COUNT 4. SEARCH 5. TRAVERSE 0. EXIT
Enter your choice 1
Enter an element to insert into queue 76
1. INSERT 2. DELETE 3. COUNT 4. SEARCH 5. TRAVERSE 0. EXIT
Enter your choice 1
Enter an element to insert into queue 43
1. INSERT 2. DELETE 3. COUNT 4. SEARCH 5. TRAVERSE 0. EXIT
Enter your choice 1
OVERFLOW
1. INSERT 2. DELETE 3. COUNT 4. SEARCH 5. TRAVERSE 0. EXIT
Enter your choice 5
23 34 5 65 76 87 5 3 76 43
```

