
// To examine whether the stack is empty.
int stacks::isEmpty ()
{
    if (top==-1)
    return 1;
    else
    return 0;
}

尽管执行了压入和弹出操作，我们并不知道栈中可用的元素。为了实现这一目标，创建了 display () 函数。该函数显示栈中的所有元素。它从栈顶开始向栈底遍历。为了确保 top 不偏离当前位置，使用了一个名为 'i' 的新变量，并将 top 的值赋给该变量。

// Program to display the element(s) of the stack.
void stacks::display ()
{
    for (int i=top; i>=0; i--)
    cout<<stack[i]<<" ";
    cout<<endl;
}

在很多情况下，我们需要确定在任意特定时刻栈中元素的数量。为了实现这一目标，我们创建了 count_elements () 函数。

## 5.4.1.1 统计元素个数

要统计栈中元素的数量，我们从栈顶开始向栈底移动。在此循环过程中，用于计数栈元素的变量 cnt 每次加 1。最后，当所有元素都遍历完毕后，将 'cnt' 变量的值返回给调用函数。

//function to count the number of element(s) in the stack;
int stacks::count_elements()
{
//initialize the t with top and cnt with 0.
int cnt=0,t=top;
// Continue till stack is not empty.
while(t>=0)

## 栈

最初，动态栈为空。为了突出这种情况，我们用 NULL 初始化了 top。由于所有栈都是从空状态开始创建的，因此我们借助构造函数对其进行了初始化。

一旦将元素插入（压入）栈中，top 将移动到新位置。栈的插入操作如图 5.3 所示。最初，栈为空，因此 top 指向 NULL。当插入 10 时，top 将指向新位置。类似地，当插入 20 时，top 的新位置如图 5.3 (c) 所示。

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
{
    stacknode *temp;
    temp=new stacknode;
    temp->data=element;
    temp->next=top;
    top=temp;
}
}
```

为了显示动态栈中的当前元素，我们使用 current 指针，它接收 top 的地址并有助于保留 top 的值。在我们的程序中，临时变量用名称 current 表示。为了遍历整个栈列表，使用 while 循环，该循环一直执行直到所有元素都被访问。

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

为了从栈中弹出元素，我们使用了 pop 函数。该函数用于从栈中移除元素。在取出（弹出）任何元素之前，首先要检查栈中是否有可用元素。如果栈中没有可用元素，则显示栈为空的提示信息，并且函数返回失败状态。如果栈中有一个或多个元素，则返回被移除的元素。调用者将收到该返回值以供后续使用。描述 pop 操作的函数如下所示。

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

类似地，我们可以为动态栈创建 size () 函数，用于统计当前栈中元素的数量。为了完成此任务，我们从栈顶开始向栈底移动。在此遍历过程中，表示“计数”的变量每次增加 1。表示动态栈大小的函数如下所示：

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

调用栈函数的顺序在主函数中展示。函数调用的顺序完全由要执行的具体操作决定。但是，首先将从 push 开始，因为在从栈中移除元素之前，需要先插入前几个元素。

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

## 5.5.2 使用模板的动态栈

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

## 栈

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

## 5.6 栈的应用

栈应用于各种场景。在大多数应用中，栈的用法要么是显式的，要么是隐式的。例如，在树的非递归遍历中，这种数据结构被显式使用。在递归中，它被程序隐式使用。栈广泛用于括号匹配、中缀转后缀、复杂表达式求值等应用。使用栈的应用将在接下来的小节中讨论。

