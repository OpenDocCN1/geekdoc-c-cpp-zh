
![](img/b217c421655b51e7494cf3b89bb5432d_1236_0.png)

图17-6 栈的示例

注意，指针`list`包含数组（存放栈元素）的基地址——即第一个数组分量的地址。接下来，我们讨论如何实现类`stackType`的成员函数。

### 初始化栈

让我们考虑`initializeStack`操作。由于`stackTop`的值指示栈是否为空，因此只需将`stackTop`设为0即可初始化栈（见图17-7）。

![](img/b217c421655b51e7494cf3b89bb5432d_1236_1.png)

图17-7 空栈

函数`initializeStack`的定义如下：

```cpp
template <class Type>
void stackType<Type>::initializeStack()
{
    stackTop = 0;
}//end initializeStack
```

### 空栈

我们已经看到，`stackTop`的值指示栈是否为空。如果`stackTop`为0，则栈为空；否则，栈不为空。函数`isEmptyStack`的定义如下：

```cpp
template <class Type>
bool stackType<Type>::isEmptyStack() const
{
    return (stackTop == 0);
}//end isEmptyStack
```

### 满栈

接下来，考虑操作`isFullStack`。由此可知，如果`stackTop`等于`maxStackSize`，则栈为满。函数`isFullStack`的定义如下：

```cpp
template <class Type>
bool stackType<Type>::isFullStack() const
{
    return (stackTop == maxStackSize);
}//end isFullStack
```

### 入栈

向栈中添加（或压入）一个元素是一个两步过程。回顾一下，`stackTop`的值指示栈中元素的数量，而`stackTop - 1`给出栈顶元素的位置。因此，入栈操作如下：

- 1. 将`newItem`存入`stackTop`所指示的数组分量中。
- 2. 递增`stackTop`。

图17-8和图17-9说明了入栈操作。

假设在入栈操作之前，栈如图17-8所示。

![](img/b217c421655b51e7494cf3b89bb5432d_1238_0.png)

图17-8 压入y之前的栈

假设**newItem**为**'y'**。入栈操作之后，栈如图17-9所示。

![](img/b217c421655b51e7494cf3b89bb5432d_1238_1.png)

图17-9 压入y之后的栈

![](img/b217c421655b51e7494cf3b89bb5432d_1238_2.png)

使用前面的算法，函数`push`的定义如下：

```cpp
template <class Type>
void stackType<Type>::push(const Type& newItem)
{
    if (!isFullStack())
    {
        list[stackTop] = newItem;    // add newItem to the
                                      // top of the stack
        stackTop++;                   // increment stackTop
    }
    else
        cout << "Cannot add to a full stack." << endl;
}//end push
```

如果试图向满栈添加新元素，所产生的情况称为**溢出**。溢出错误检查可以通过不同方式处理。一种方式如前面所示。或者，我们可以在调用函数`push`之前检查是否溢出，如下所示（假设`stack`是`stackType`类型的对象）。

```cpp
if (!stack.isFullStack())
    stack.push(newItem);
```

### 返回栈顶元素

操作`top`返回栈顶元素。其定义如下：

```cpp
template <class Type>
Type stackType<Type>::top() const
{
    assert(stackTop != 0);        //if stack is empty,
                                   //terminate the program

    return list[stackTop - 1];     //return the element of the
                                   //stack indicated by
                                   //stackTop - 1
}//end top
```

### 出栈

要从栈中删除（或弹出）一个元素，只需将`stackTop`递减1。

图17-10和图17-11说明了出栈操作。

假设在出栈操作之前，栈如图17-10所示。

![](img/b217c421655b51e7494cf3b89bb5432d_1240_0.png)

图17-10 弹出D之前的栈

出栈操作之后，栈如图17-11所示。

![](img/b217c421655b51e7494cf3b89bb5432d_1240_1.png)

图17-11 弹出D之后的栈

![](img/b217c421655b51e7494cf3b89bb5432d_1240_2.png)

函数pop的定义如下：

```cpp
template <class Type>
void stackType<Type>::pop()
{
    if (!isEmptyStack())
        stackTop--;                    //decrement stackTop
    else
        cout << "Cannot remove from an empty stack." << endl;
}//end pop
```

如果试图从空栈中删除元素，所产生的情况称为下溢。下溢错误检查可以通过不同方式处理。一种方式如函数pop的定义所示。或者，我们可以在调用函数pop之前检查是否下溢，如下所示（假设stack是stackType类型的对象）。

```cpp
if (!stack.isEmptyStack())
    stack.pop();
```

### 复制栈

函数copyStack制作栈的副本。要复制的栈作为参数传递给函数copyStack。实际上，我们将使用该函数实现复制构造函数并重载赋值运算符。该函数的定义如下：

```cpp
template <class Type>
void stackType<Type>::copyStack(const stackType<Type>& otherStack)
{
    delete [] list;
    maxStackSize = otherStack.maxStackSize;
    stackTop = otherStack.stackTop;

    list = new Type[maxStackSize];

        //copy otherStack into this stack
    for (int j = 0; j < stackTop; j++)
        list[j] = otherStack.list[j];
} //end copyStack
```

### 构造函数和析构函数

用于实现构造函数和析构函数的函数很直接。带参数的构造函数将栈大小设置为用户指定的大小，将stackTop设置为0，并创建一个合适的数组来存放栈元素。如果用户未指定用于存放栈元素的数组大小，则构造函数使用默认值100来创建大小为100的数组。析构函数只是释放数组（即栈）所占用的内存，并将stackTop设置为0。构造函数和析构函数的定义如下：

```cpp
template <class Type>
stackType<Type>::stackType(int stackSize)
{
    if (stackSize <= 0)
    {
        cout << "Size of the array to hold the stack must "
             << "be positive." << endl;
        cout << "Creating an array of size 100." << endl;
        maxStackSize = 100;
    }
    else
        maxStackSize = stackSize;    //set the stack size to
                                     //the value specified by
                                     //the parameter stackSize

    stackTop = 0;                    //set stackTop to 0
    list = new Type[maxStackSize];   //create the array to
                                     //hold the stack elements
}//end constructor

template <class Type>
stackType<Type>::~stackType() //destructor
{
    delete [] list; //deallocate the memory occupied
                    //by the array
}//end destructor
```

### 复制构造函数

当栈对象作为（值）参数传递给函数时，会调用复制构造函数。它将实参的成员变量的值复制到形参的对应成员变量中。其定义如下：

```cpp
template <class Type>
stackType<Type>::stackType(const stackType<Type>& otherStack)
{
    list = nullptr;

    copyStack(otherStack);
}//end copy constructor
```

### 重载赋值运算符（=）

回顾一下，对于具有指针成员变量的类，必须显式重载赋值运算符。为类stackType重载赋值运算符的函数定义如下：

```cpp
template <class Type>
const stackType<Type> & stackType<Type>::operator=
                         (const stackType<Type>& otherStack)
```
