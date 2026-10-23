
```
int Q::dequeue()
{
    int a;
    if((rear== -1)||(front== -1))
    {
        cout<<"underflow:\n";
        return 0;
    }
    else
    {
        a=queue[front];
        front++;
        if(front>rear)//after removal if queue is empty
        {
            front=rear=-1;
        }
    }
    return a;
}
```

## 6.2.1.3 统计元素数量

要统计队列中的元素数量，我们必须从队首开始。由于 `front` 可能位于第 0 个索引，也可能在部分元素被移除（出队）后远离该位置。计数应一直进行到队尾元素为止，因为它表示元素的最后一个位置（索引）。

```
// Program to count the number of elements in the queue
int Q::count()
{
int f,r, c=0;
f=front,r=rear;// initialize f with front and rear
while(f++<=r) //execute the loop till last element is not reached
{
c++;  //count the elements
}
return c;   // return the count
}
```

## 6.2.1.4 查找队列中的第一个元素

我们可以在不改变第一个索引的情况下确定队列中的第一个元素。一旦队列中的元素被显示出来，它将再次显示所有元素，包括 `FirstElement()` 函数返回的第一个元素。该函数的代码如下例所示：

```
// Program : Write the program to determine the first element in a
queue without changing the first index.

int firstelement()
{
if(first==0)
{
cout<<" queue is empty";
return 0;
}
int x=queue[first];      // Store the first element of the stack
return x;   // return the first element
}
```

## 6.2.2 主函数

前面各小节中定义的函数都能实现各自的目标。要调用它们，我们可以使用主函数，调用方式如下例所示。

```
int main()
{
clrscr();
Q q1;
q1.enqueue(90);
q1.enqueue(5);
q1.enqueue(78);
q1.enqueue(35);
q1.enqueue(10);
q1.enqueue(14);
cout<<" Total number of elements "<<q1.count()<<endl;
q1.display();
cout<<"Dequeue item: "<<q1.dequeue()<<endl;
cout<<"Dequeue item: "<<q1.dequeue()<<endl;
```
```
cout<<" Total number of elements "<<q1.count()<<endl;
q1.display();
if(q1.isEmpty())
    cout<<"Queue is empty"<<endl;
else
cout<<"Not empty"<<endl;
getch();
return 0;
}
```

## 6.2.3 队列的局限性

队列因执行出队操作而有一个主要局限。出队时，`front` 会向 `rear` 移动。因此，从第 0 个索引到 `front` 之间不再有元素。虽然空间仍然存在，但用户无法利用这些空间，因为 `front` 已经越过了第 0 个索引。为了克服这一局限，可以将元素从当前位置移动到第 0 个索引及其之后的位置。因此，`front` 和 `rear` 的值也需要相应改变。

![](img/9b7c80a1312a664ae505ba138aa3306b_175_0.png)

对于较小规模的列表，移动操作可能是更好的选择；但对于规模很大的队列，移动元素将代价高昂，并且需要大量资源来移动元素。

```
// To shift the Element after dequeue
void Q::shiftElements()
{
int f=front,t=-1;
while(f<=rear)
{
queue[++t]=queue[f++]; // initialize the front member in the 0th index
}
front=0;
rear=t;
cout<<endl<<"Items shifted in the Q"<<endl;
```

## 6.3 动态队列

动态队列克服了静态队列的局限。动态队列可以扩展到任意程度，唯一限制是硬件限制。在动态队列中，无需测试队满条件，因为它由硬件容量决定。不过，与之前一样，仍需要测试队空条件。

动态队列的结构通过以下类定义。下面的程序给出了各个函数及其功能。

```
//Structure of queue node
class qnode
{
public:
int info;
qnode *next;
};
class queue            //class for queue
{
//defining the front and rear pointer
qnode *front,*rear;
public:
//constructor for queue
queue();
//function to enqueue in dynamic queue
void enqueue(int);
//function to deque in the queue
int dequeue();
//To display the items in the queue
void display();
};
```

如果队列为空，则表示队列中没有元素。因此，不能移除任何元素，并返回不成功标志（0）。

第二种情况下，从队首移除元素。元素出队后，队列将为空。为了反映这一变化，需要将 `front` 和 `rear` 初始化为 NULL。

第三种情况下，当队列中元素多于一个时，`front` 必须移动到下一个可用位置。需要删除数据项以及存储在 `temp` 中的前一个 `front` 指针，以释放原先由 `front` 指针占用的空间。

```
// Function to dequeue the element from the queue
int queue::dequeue()
{
int x=front->info;
if(front==NULL)
{
cout<<"Queue is empty"<<endl;
}
else
{
qnode *temp=front;
if(front==rear)
{
front=NULL;
rear=NULL;
delete temp;
return x;
}
front=front->next;
}
return x;
}
```

入队操作会插入元素，而出队操作则从队列中移除元素。在入队和出队操作之后，大多数情况下队列中仍会剩余一些元素。为了观察这一变化，可以使用 `display` 函数。该函数显示当前动态队列中的元素。

要显示元素，我们从 `front` 开始，持续访问节点，直到到达队列末尾。队列末尾位置由 `rear` 表示。

```
void queue::display()
{
    qnode *current;
    if(front==NULL)
    {
    cout<<"queue is empty"<<endl;
    return;
    }
    current=front;
    while(current!=rear)
    {
    cout<<current->info<<endl;
    current=current->next;
    }
    cout<<current->info<<endl;
}
```

`isEmpty()` 是本程序中另一个具有重要作用的函数。它可以同时支持入队和出队。在入队期间，它可用来检查队列是否为空，并据此启动下一步操作。

该函数在调用 `dequeue` 函数时也起着重要作用。我们可以将 `isEmpty()` 作为条件包含到其他函数中。如果队列为空，则无法执行出队操作。`isEmpty()` 函数在下面的程序中定义。

```
int queue::isEmpty()
{
    int flag=0;
    if(front==NULL)
    {
    flag=1;
    }
    return flag;
}
```

上述所有函数都可以从主函数中调用。需要传递的顺序和参数已在主函数中给出。下面的主函数展示了这一点。

```
// Main function to call other queue function
void main()
{
    clrscr();
    queue q1;
    q1.enqueue(40);
    q1.enqueue(27);
    if(q1.isEmpty())
    {
        cout<<"Q is empty"<<endl;
    }
    //q1.enqueue(12);
    //q1.enqueue(64);
    q1.display();
    int j;
    j=q1.dequeue();
    cout<<" element deleted "<<j<<endl;
    q1.display();
    j=q1.dequeue();
    cout<<" element deleted "<<j<<endl;
    if(q1.isEmpty())
    {
        cout<<"Q is empty"<<endl;
    }
    q1.display();
    j=q1.dequeue();
    cout<<" element deleted "<<j<<endl;
    q1.display();
    getch();
}
```

## 6.4 使用模板的队列

动态队列在数据结构中有着广泛的应用。动态队列主要用于树的遍历，尤其是广度优先遍历。同时，我们还可以享受队列大小不受限制的灵活性。前面一节中给出的队列存在一个局限：对于不同的数据类型，程序需要相应修改。例如，前面讨论的程序使用了整数数据类型；如果必须使用字符数据类型，则需要适当修改程序。

为了解决这类问题并使程序适用于任何数据类型，我们可以使用模板。下面的程序演示了队列模板 `t` 的使用：

```
#include<conio.h>
#include<iostream.h>
//Structure of queue node
template<class t>
class qnode
{
public:
t info;
qnode<t> *next;
};
//class for queue
template<class t>
class queue
{
//defining the front and rear pointer
qnode<t> *front,*rear;
public:
//constructor for queue
queue();
//function to enqueue in dynamic queue
void enqueue(t);
//function to deque in the queue
 t dequeue();
//To display the items in the queue
void display();
//To check for queue empty or not
int isEmpty();
};
template<class t>
queue<t>::queue()
{
```
