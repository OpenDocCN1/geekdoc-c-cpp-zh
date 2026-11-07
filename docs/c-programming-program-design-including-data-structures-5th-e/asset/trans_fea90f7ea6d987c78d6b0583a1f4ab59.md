
```cpp
Type top() const;
    //Function to return the top element of the stack.
    //Precondition: The stack exists and is not empty.
    //Postcondition: If the stack is empty, the program
    //               terminates; otherwise, the top
    //               element of the stack is returned.

void pop();
    //Function to remove the top element of the stack.
    //Precondition: The stack exists and is not empty.
    //Postcondition: The stack is changed and the top
    //               element is removed from the stack.

linkedStackType();
    //Default constructor
    //Postcondition: stackTop = NULL;

linkedStackType(const linkedStackType<Type>& otherStack);
    //Copy constructor

~linkedStackType();
    //Destructor
    //Postcondition: All the elements of the stack are
    //               removed from the stack.

private:
    nodeType<Type> *stackTop; //pointer to the stack

    void copyStack(const linkedStackType<Type>& otherStack);
        //Function to make a copy of otherStack.
        //Postcondition: A copy of otherStack is created and
        //               assigned to this stack.
};
```

> **注意** 在栈的这种链式实现中，用于存储栈元素的内存是动态分配的。从逻辑上讲，栈永远不会满。只有当内存空间耗尽时，栈才会满。因此，实际上，函数 isFullStack 不适用于栈的链式实现。然而，类 linkedStackType 必须提供函数 isFullStack 的定义，因为它在父抽象类 stackADT 中定义。

我们将类 linkedStackType 的 UML 类图留作练习。（参见本章末尾的练习26。）

## 示例 18-2

假设 stack 是 linkedStackType 类型的对象。图 18-12(a) 展示了一个空栈，图 18-12(b) 展示了一个非空栈。

![](img/f97f778697507bb6fdd80c5991210cba_1150_0.png)

**图 18-12** 空链式栈和非空链式栈

在图 18-12(b) 中，栈顶元素是 C；也就是说，最后入栈的元素是 C。

接下来，我们讨论实现链式栈操作的函数定义。

### 默认构造函数

我们考虑的第一个操作是默认构造函数。当声明栈对象时，默认构造函数将栈初始化为空状态。因此，该函数将 stackTop 设置为 NULL。该函数的定义如下：

```cpp
template <class Type>
linkedStackType<Type>::linkedStackType()
{
    stackTop = NULL;
}
```

### 空栈与满栈

操作 isEmptyStack 和 isFullStack 非常直接。如果 stackTop 为 NULL，则栈为空。此外，由于栈元素的内存是动态分配和释放的，栈永远不会满。（只有当内存耗尽时，栈才会满。）因此，函数 isFullStack 总是返回值 false。实现这些操作的函数定义如下：

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

回想一下，在栈的链式实现中，函数 isFullStack 并不适用，因为从逻辑上讲，栈永远不会满。然而，你必须提供它的定义，因为它作为抽象函数包含在父类 `class stackADT` 中。

### 初始化栈

操作 initializeStack 将栈重新初始化为空状态。由于栈可能包含一些元素，并且我们使用的是栈的链式实现，因此必须释放栈元素占用的内存，并将 stackTop 设置为 NULL。该函数的定义如下：

```cpp
template <class Type>
void linkedStackType<Type>::initializeStack()
{
    nodeType<Type> *temp; //pointer to delete the node

    while (stackTop != NULL) //while there are elements in
                             //the stack
    {
        temp = stackTop;     //set temp to point to the
                             //current node
        stackTop = stackTop->link; //advance stackTop to the
                                   //next node
        delete temp;         //deallocate memory occupied by temp
    }
} //end initializeStack
```

接下来，我们考虑 `push`、`top` 和 `pop` 操作。从图 18-12(b) 可以清楚地看出，在 `push` 的情况下，`newElement` 将被添加到 `stackTop` 所指向的链表的开头。在 `pop` 的情况下，将移除 `stackTop` 所指向的节点。在这两种情况下，指针 `stackTop` 的值都会被更新。操作 `top` 返回 `stackTop` 所指向节点的 info 字段。

### 入栈

考虑图 18-13 所示的栈。

创建一个节点，将该节点的地址存储到变量 newNode 中，并将 newElement 存储到 newNode 的 info 字段中。参见图 18-14(a)。

语句：

```cpp
newNode->link = stackTop;
```

将 newNode 插入到栈顶，如图 18-14(b) 所示。

最后，语句：

```cpp
stackTop = newNode;
```

更新 stackTop 的值，结果如图 18-14(c) 所示。

函数 push 的定义如下：

```cpp
template <class Type>
void linkedStackType<Type>::push(const Type& newElement)
{
    nodeType<Type> *newNode; //pointer to create the new node

    newNode = new nodeType<Type>; //create the node

    newNode->info = newElement; //store newElement in the node
    newNode->link = stackTop; //insert newNode before stackTop
    stackTop = newNode; //set stackTop to point to the
                        //top node
} //end push
```

在将元素压入栈之前，我们不需要检查栈是否已满，因为在这种实现中，从逻辑上讲，栈永远不会满。

### 返回栈顶元素

返回栈顶元素的操作非常直接。其定义如下：

```cpp
template <class Type>
Type linkedStackType<Type>::top() const
{
    assert(stackTop != NULL); //if stack is empty,
                              //terminate the program
    return stackTop->info;    //return the top element
}//end top
```

### 出栈

现在我们考虑 pop 操作，它移除栈顶元素。考虑图 18-15 所示的栈。

![](img/f97f778697507bb6fdd80c5991210cba_1154_0.png)

**图 18-15** pop 操作之前的栈

图 18-16 展示了 pop 操作。

![](img/f97f778697507bb6fdd80c5991210cba_1154_1.png)

**图 18-16** pop 操作

语句：

```cpp
temp = stackTop;
```

使 temp 指向栈顶。参见图 18-16(a)。接下来，语句：

```cpp
stackTop = stackTop->link;
```

使栈的第二个元素成为栈顶元素。参见图 18-16(b)。

最后，语句：

```cpp
delete temp;
```

释放 temp 所指向的内存。参见图 18-16(c)。

函数 pop 的定义如下：

```cpp
template <class Type>
void linkedStackType<Type>::pop()
{
    nodeType<Type> *temp;    //pointer to deallocate memory

    if (stackTop != NULL)
    {
        temp = stackTop;    //set temp to point to the top node

        stackTop = stackTop->link;    //advance stackTop to the
                                      //next node

        delete temp;    //delete the top node
    }
    else
        cout << "Cannot remove from an empty stack." << endl;
}//end pop
```

### 复制栈

函数 copyStack 生成栈的一个完全相同的副本。其定义类似于第17章中给出的链表 copyList 的定义。函数 copyStack 的定义如下：

```cpp
template <class Type>
void linkedStackType<Type>::copyStack
                         (const linkedStackType<Type>& otherStack)
{
    nodeType<Type> *newNode, *current, *last;

    if (stackTop != NULL) //if stack is nonempty, make it empty
        initializeStack();

    if (otherStack.stackTop == NULL)
        stackTop = NULL;
    else
    {
        current = otherStack.stackTop;  //set current to point
                                        //to the stack to be copied

        //copy the stackTop element of the stack
        stackTop = new nodeType<Type>;  //create the node

        stackTop->info = current->info; //copy the info
