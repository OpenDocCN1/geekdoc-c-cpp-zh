
// To examine whether the stack is empty.
int stacks::isEmpty ()
{
    if (top==-1)
    return 1;
    else
    return 0;
}

Despite executing the push and pop operation, we are not aware of the elements that are available in the stack. To accomplish this objective, the function display () has been created. This function displays all the elements in the stack. It starts from the top and goes towards the bottom of the stack. In order to ensure that top is not shifted from the current position, a new variable with the name 'i' has been used and the value of top is assigned to this variable.

// Program to display the element(s) of the stack.
void stacks::display ()
{
    for (int i=top; i>=0; i--)
    cout<<stack[i]<<" ";
    cout<<endl;
}

On various occasions, we would need to determine the number of elements in the stack at any particular point in time. To accomplish this objective, we have created the count_elements () function.

## 5.4.1.1 Counting the number of elements

To count the number of elements in a stack, we have started from the top and moved towards the base. During this looping, variable cnt that counts the element of stack is incremented by 1. Finally, when all the elements are exhausted value of 'cnt' variable is returned to the caller function.

//function to count the number of element(s) in the stack;
int stacks::count_elements()
{
//initialize the t with top and cnt with 0.
int cnt=0,t=top;
// Continue till stack is not empty.
while(t>=0)

## Stack

Initially, the dynamic stack will be empty. To highlight this condition, we have initialized the top with the NULL. Since, all the stacks will be created from the empty condition, therefore; we have initialized it with the help of constructor.

Once the items are inserted (push) into the stack, top will move towards the new position. Insertion of the stack is illustrated in the following figure 5.3. Initially, the stack is empty; therefore top will be pointing to the NULL. When 10 is inserted, top will point to the new position. Similarly, when 20 is inserted the new position of top is demonstrated in the figure 5.3 (c).

![](img/9b7c80a1312a664ae505ba138aa3306b_149_0.png)

```
```cpp
stack::stack()
{

top=NULL;

}
void stack::push(int element)
{

    if(top==NULL)
    {

        top=new stacknode;
        top->data=element;
        top->next=NULL;

    }
    else
```
```
```
{
    stacknode *temp;
    temp=new stacknode;
    temp->data=element;
    temp->next=top;
    top=temp;
}
}
```

To display the current items in a dynamic stack, we use the current pointer, which accepts the address of the top and facilitates in retaining the value of top. In our program, temporary variable has been represented with the name current. To traverse the entire list of stack, while loop is used that executes till all the elements are not accessed.

```
void stack::display()
{
    stacknode *current;
    current=top;   // storing the address of top to the current
    cout<<" Elements in the stack are: "<<endl;
    while(current!=NULL)
    {
        cout<<current->data<<"     "; //display the data
        current=current->next;   // move to the next node, towards the base
    }
    cout<<endl;
}
```

To pop the items from the stack, we have used the pop function. This function will be used to remove the elements from the stack. Before taking out (pop) any element, stack is first examined for the availability of any. In case if no item is available in the stack, in that case message for the stack empty is displayed and the failure status is returned from the function. In case, if one or more item(s) are available in the stack, the item that is removed is returned. Same will be received by the caller for the future use. A function that describes the pop operation has been described as follows.

```
int stack::pop()// function to pop the element of the dynamic stack
{
    if(top==NULL)
    {
```
```
cout<<"Stack is empty "<<endl;
return 0;
}

stacknode* temp=top;
int el=temp->data;
top=top->next;
delete temp;
return el;
}
```

Similarly, we can create the size () function for the dynamic stack that count the number of elements currently in the stack. To accomplish this task, we have started from the top and moved towards the base. During this traversal, variable representing the ‘count’ is incremented by one. Function to represent the size of a dynamic stack is depicted below:

```
// function to determine the size (number of count) of the dynamic stack
int stack::size()
{
int count=0;
if(top==NULL)
{
cout<<"No element in the stack "<<endl;
return count;
}
stacknode *current;
current=top;  // storing the address of top to the current
while(current!=NULL)
{
count++;
}
return count;
}
```

Sequence of calling the stack function is depicted in the main function. Calling of the functions sequence is entirely governed by the specific operation to be accomplished. However, first it will start with the push, since, first few elements need to be inserted before removing the element from the stack.

```
stacks()
{
    top=-1;
}
int push(t);
t pop();
int isEmpty();
void display();
int count_elements();
};
// function to count the number of elements
template<class t>
int stacks<t>::count_elements()
{
int cnt=0,t1=top;
while(t1>=0)
{
cnt++;
t1--;
}
return cnt;
}
template<class t>
int stacks<t>::push(int element)
{
if(top==(size-1))
{
cout<<"overflow element not entered\n";
return 0;
}
else
{
stack[++top]=element;
}
return 1;
```

```
}
template<class t>
    t stacks<t>::pop()
    {
        t a=stack[top];
        if(top==-1)
        {
            cout<<"underflow:\n";
        }
        else
        {
            a=stack[top--];
        }
        return a;
    }
//function to display the item in the stack.
    template<class t>
    void stacks<t>::display()
    {
        for(int i=top;i>=0;i--)
        cout<<stack[i]<<" ";
        cout<<endl;
    }
    template<class t>
    int stacks<t>::isEmpty()
    {
        if(top==-1)
        return 1;
        else
        return 0;
    }
// Completion of all function and starting of main function
int main()
{
int n,n1;
```
```
stacks<int> s1;
clrscr();
if(s1.isEmpty())
cout<<"Stack is empty"<<endl;
else
cout<<"Stack is not empty";
s1.push(10);
s1.push(5);
//s1.push(7);
s1.push(14);
cout<<"Total    number    of    elements    in    stack    are:"<<s1.count_elements()<<endl;
s1.push(90);
//s1.push(299);
cout<<" Element(s) in the stack are:"<<endl;
s1.display();
n=s1.pop();
cout<<" Element pop is "<<n<<endl;
getch();
return 0;
}
```

## 5.5.2 Dynamic stack using template

```
#include<iostream.h>
#include<conio.h>
//using namespace std;
const int size=5;
template <class t>
class stacks
{
    t stack[size];
    int top;
    public:
        stacks()
        {
```
```
top=-1;
}
int push(t);
t pop();
int isempty();
void display();
int count_elements();
};
template<class t>
int stacks<t>::count_elements()
{
int cnt=0,t1=top;
while(t1>=0)
{
cnt++;
t1--;
}
return cnt;
}
template<class t>
int stacks<t>::push(int element)
{
if(top==(size-1))
{
cout<<"overflow element not entered\n";
return 0;
}
else
{
stack[++top]=element;
}
return 1;
}
template<class t>
t stacks<t>::pop()
```

## Stack

```
```cpp
{
    t a=stack[top];
    if(top==-1)
    {
        cout<<"underflow:\n";
    }
    else
    {
        a=stack[top--];
    }
    return a;
}
template<class t>
void stacks<t>::display()
{
    for(int i=top;i>=0;i--)
        cout<<stack[i]<<" ";
    cout<<endl;
}
template<class t>
int stacks<t>::isempty()
{
    if(top==-1)
        return 1;
    else
        return 0;
}
int main()
{
int n,n1;
stacks<int> s1;
clrscr();
if(s1.isempty())
cout<<"stack is empty"<<endl;
else
```
```
cout<<"stack is not empty";
s1.push(10);
s1.push(5);
//s1.push(7);
//s1.push(14);
cout<<"total    number    of    elements    in    stack    are:"<<s1.count_elements()<<endl;
s1.push(90);
//s1.push(299);
cout<<" element(s) in the stack are:"<<endl;
s1.display();
n=s1.pop();
cout<<" element pop is "<<n<<endl;
n=s1.pop();
cout<<" element pop is "<<n<<endl;
n=s1.pop();
cout<<" element pop is "<<n<<endl;
if(s1.isempty())
cout<<"stack under flow"<<endl;
else
{
n=s1.pop();
cout<<" element pop is "<<n<<endl;
}
getch();
return 0;
}
```

## 5.6 APPLICATION OF STACK

Stack is applied in variety of applications. In majority of applications, usage of stack is either explicit or implicit. For instance, in non-recursive traversal of a tree this data structure is explicitly used. In the recursion, it is implicitly used by the program. Stack is widely utilized in the application such as parenthesis matching, infix to postfix conversion, evaluation of complex expression etc. Applications utilizing stack have been discussed in the upcoming sub-section.
