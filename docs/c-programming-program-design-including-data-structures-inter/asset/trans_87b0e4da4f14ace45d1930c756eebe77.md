
```cpp
infile.open("HighestGPAData.txt");              //Step 2

if (!infile)                                    //Step 3
{
    cout << "The input file does not"
         << "exist. Program terminates!"
         << endl;
    return 1;
}

cout << fixed << showpoint;                     //Step 4
cout << setprecision(2);                        //Step 4

infile >> GPA >> name;                          //Step 5

highestGPA = GPA;                               //Step 6

while (infile)                                  //Step 7
{
    if (GPA > highestGPA)                       //Step 7.1
    {
        stack.initializeStack();                //Step 7.1.1

        if (!stack.isFullStack())               //Step 7.1.2
            stack.push(name);

        highestGPA = GPA;                       //Step 7.1.3
    }
    else if (GPA == highestGPA)                 //Step 7.2
    {
        if (!stack.isFullStack())
            stack.push(name);
        else
        {
            cout << "Stack overflows."
                 << "Program terminates!"
                 << endl;
            return 1;                           //exit program
        }
    }

    infile >> GPA >> name;                      //Step 7.3
}

cout << "Highest GPA = " << highestGPA
     << endl;                                   //Step 8
cout << "The students holding the "
     << "highest GPA are:" << endl;

while (!stack.isEmptyStack())                   //Step 9
{
    cout << stack.top() << endl;
    stack.pop();
}
```

回顾一下，在栈的线性表示中，stackTop 的值表示栈中元素的数量，而 stackTop - 1 的值指向栈顶项。借助 stackTop，我们可以完成几件事：找到栈顶元素、检查栈是否为空，等等。

与线性表示类似，在链式表示中，stackTop 用于定位栈中的栈顶元素。不过，这里有一个细微差别。在前一种情况下，stackTop 给出数组的下标。在后一种情况下，stackTop 给出栈顶元素的地址（内存位置）。

下面的类实现了抽象类 stackADT 中的函数：

```cpp
//Definition of the node
template <class Type>
struct nodeType
{
    Type info;
    nodeType<Type> *link;
};

template <class Type>
class linkedStackType: public stackADT<Type>
{
public:
    const linkedStackType<Type>& operator=
                         (const linkedStackType<Type>&);
    //Overload the assignment operator.

    bool isEmptyStack() const;
    //Function to determine whether the stack is empty.
    //Postcondition: Returns true if the stack is empty;
    //               otherwise returns false.

    bool isFullStack() const;
    //Function to determine whether the stack is full.
    //Postcondition: Returns false.

    void initializeStack();
    //Function to initialize the stack to an empty state.
    //Postcondition: The stack elements are removed;
    //               stackTop = NULL;

    void push(const Type& newItem);
    //Function to add newItem to the stack.
    //Precondition: The stack exists and is not full.
    //Postcondition: The stack is changed and newItem
    //               is added to the top of the stack.

    Type top() const;
    //Function to return the top element of the stack
    //Precondition: The stack exists and is not empty.
    //Postcondition: If the stack is empty, the program
    //              terminates; otherwise, the top
    //              element of the stack is returned.
    void pop();
    //Function to remove the top element of the stack.
    //Precondition: The stack exists and is not empty.
    //Postcondition: The stack is changed and the top
    //              element is removed from the stack.

    linkedStackType();
    //Default constructor
    //Postcondition: stackTop = NULL;

    linkedStackType(const linkedStackType<Type>& otherStack);
    //Copy constructor

    ~linkedStackType();
    //Destructor
    //Postcondition: All the elements of the stack are
    //              removed from the stack.

private:
    nodeType<Type> *stackTop; //pointer to the stack

    void copyStack(const linkedStackType<Type>& otherStack);
    //Function to make a copy of otherStack.
    //Postcondition: A copy of otherStack is created and
    //              assigned to this stack.
};
```

在这种栈的链式实现中，用于存储栈元素的内存是动态分配的。从逻辑上说，栈永远不会满。只有当内存空间耗尽时，栈才会满。因此，实际上，函数 isFullStack 并不适用于栈的链式实现。然而，类 linkedStackType 必须提供函数 isFullStack 的定义，因为该函数是在父抽象类 stackADT 中定义的。

我们将类 linkedStackType 的 UML 类图留作练习。（参见本章末尾的习题 28。）

## 示例 17-2

假设 stack 是一个 linkedStackType 类型的对象。图 17-12(a) 展示了一个空栈，图 17-12(b) 展示了一个非空栈。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1192_0.png)

在图 17-12(b) 中，栈顶元素是 C；也就是说，最后被压入栈的元素是 C。

接下来，我们讨论实现链式栈操作的相关函数定义。

### 默认构造函数

我们考虑的第一个操作是默认构造函数。当声明一个栈对象时，默认构造函数会将栈初始化为空状态。因此，该函数将 stackTop 设置为 NULL。该函数的定义如下：

```cpp
template <class Type>
linkedStackType<Type>::linkedStackType()
{
    stackTop = NULL;
}
```

### 空栈与满栈

操作 isEmptyStack 和 isFullStack 非常直接。如果 stackTop 为 NULL，则栈为空。另外，由于栈元素的内存在动态分配和释放，栈永远不会满。（只有当内存耗尽时，栈才会满。）因此，函数 isFullStack 总是返回 false。实现这些操作的函数定义如下：

```cpp
template <class Type>
bool linkedStackType<Type>::isEmptyStack() const
{
    return (stackTop == NULL);
} //end isEmptyStack

template <class Type>
bool linkedStackType<Type>::isFullStack() const
{
    return false;
} //end isFullStack
```

回顾一下，在栈的链式实现中，函数 isFullStack 并不适用，因为从逻辑上说，栈永远不会满。然而，你必须提供它的定义，因为它作为抽象函数包含在父类 stackADT 中。

### 初始化栈

操作 initializeStack 会将栈重新初始化为空状态。由于栈中可能包含一些元素，而且我们使用的是栈的链式实现，因此必须释放栈元素占用的内存，并将 stackTop 设置为 NULL。该函数的定义如下：

```cpp
template <class Type>
void linkedStackType<Type>::initializeStack()
{
    nodeType<Type> *temp; //pointer to delete the node

    while (stackTop != NULL) //while there are elements in
                             //the stack
    {
        temp = stackTop;          //set temp to point to the
                                  //current node
        stackTop = stackTop->link; //advance stackTop to the
                                   //next node
        delete temp;              //deallocate memory occupied by temp
    }
} //end initializeStack
```

接下来，我们考虑 push、top 和 pop 操作。从图 17-12(b) 可以清楚地看出，newElement 将被添加（在 push 的情况下）到由 stackTop 指向的链表的开头。在 pop 的情况下，将由 stackTop 指向的节点删除。在这两种情况下，指针 stackTop 的值都会被更新。操作 top 返回 stackTop 所指向节点的 info。

### 入栈

考虑图 17-13 所示的栈。
