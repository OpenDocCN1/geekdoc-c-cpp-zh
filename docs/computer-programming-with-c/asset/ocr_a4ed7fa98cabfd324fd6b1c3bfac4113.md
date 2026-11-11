# Program 2

```
```cpp
#include<iostream.h>
void main()
{
int a;
a=10;
cout<<"Enter a number"<<endl;
cin>>a;
delete a;
cout<<"The value of variable ‘a’ is"<<a<<endl;
}
```
```

# Program 3

Modify the following function to traverse a linked list starting from head in reverse direction. Assume pointer head is globally defined.

```
```cpp
void traverse()
{
Node *temp;
temp=head;
cout<<"The elements of the linked list are as below:"<<endl;
    while(temp!=NULL)
    {
    cout<<temp->data<<endl;
    temp= temp -> next;
    }
}
```
```

# Program 4

Given below is the function that can be used to insert elements into a singly linked list starting from head. Assuming that head is a globally defined pointer, modify the following code to insert elements in ascending order.

```
```cpp
void insert(int x)
{
    if(head ==NULL)
    {
/*Node to be inserted is the first node*/
        head=new Node;
        head->data=x;
        head->next=NULL;
        }
        else
        {
```
```