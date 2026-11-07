
## Implementation of Stacks as Arrays

Because all of the elements of a stack are of the same type, you can use an array to implement a stack. The first element of the stack can be put in the first array slot, the second element of the stack in the second array slot, and so on. The top of the stack is the index of the last element added to the stack.

In this implementation of a stack, stack elements are stored in an array, and an array is a random access data structure; that is, you can directly access any element of the array. However, by definition, a stack is a data structure in which the elements are accessed (popped or pushed) at only one end—that is, a Last In First Out data structure. Thus, a stack element is accessed only through the top, not through the bottom or middle. This feature of a stack is extremely important and must be recognized in the beginning.

To keep track of the top position of the array, we can simply declare another variable called `stackTop`.

The following class, `stackType`, implements the functions of the abstract class `stackADT`. By using a pointer, we can dynamically allocate arrays, so we will leave it for the user to specify the size of the array (that is, the stack size). We assume that the default stack size is 100. Because the class `stackType` has a pointer member variable (the pointer to the array to store the stack elements), we must overload the assignment operator and include the copy constructor and destructor. Moreover, we give a generic definition of the stack. Depending on the specific application, we can pass the stack element type when we declare a stack object.

```cpp
template <class Type>
class stackType: public stackADT<Type>
{
public:
    const stackType<Type>& operator=(const stackType<Type>&);
        //Overload the assignment operator.

    void initializeStack();
        //Function to initialize the stack to an empty state.
        //Postcondition: stackTop = 0;

    bool isEmptyStack() const;
        //Function to determine whether the stack is empty.
        //Postcondition: Returns true if the stack is empty,
        //              otherwise returns false.

    bool isFullStack() const;
        //Function to determine whether the stack is full.
        //Postcondition: Returns true if the stack is full,
        //              otherwise returns false.

    void push(const Type& newItem);
        //Function to add newItem to the stack.
        //Precondition: The stack exists and is not full.
        //Postcondition: The stack is changed and newItem
        //                is added to the top of the stack.

    Type top() const;
        //Function to return the top element of the stack.
        //Precondition: The stack exists and is not empty.
        //Postcondition: If the stack is empty, the program
        //               terminates; otherwise, the top element
        //               of the stack is returned.

    void pop();
        //Function to remove the top element of the stack.
        //Precondition: The stack exists and is not empty.
        //Postcondition: The stack is changed and the top
        //               element is removed from the stack.

    stackType(int stackSize = 100);
        //Constructor
        //Create an array of the size stackSize to hold
        //the stack elements. The default stack size is 100.
        //Postcondition: The variable list contains the base
        //               address of the array, stackTop = 0, and
        //               maxStackSize = stackSize.

    stackType(const stackType<Type>& otherStack);
        //Copy constructor

    ~stackType();
        //Destructor
        //Remove all the elements from the stack.
        //Postcondition: The array (list) holding the stack
        //               elements is deleted.

private:
    int maxStackSize;   //variable to store the maximum stack size
    int stackTop;       //variable to point to the top of the stack
    Type *list;         //pointer to the array that holds the
                        //stack elements

    void copyStack(const stackType<Type>& otherStack);
        //Function to make a copy of otherStack.
        //Postcondition: A copy of otherStack is created and
        //               assigned to this stack.
};
```

Figure 18-5 shows the UML class diagram of the class `stackType`.

![](img/f97f778697507bb6fdd80c5991210cba_1131_0.png)

**FIGURE 18-5** UML class diagram of the class `stackType`

> **NOTE**
>
> Because C++ arrays begin with the index 0, we need to distinguish between the value of `stackTop` and the array position indicated by `stackTop`. If `stackTop` is 0, the stack is empty; if `stackTop` is nonzero, then the stack is nonempty and the top element of the stack is given by `stackTop - 1`.
>
> Notice that the function `copyStack` is included as a *private* member. This is because we want to use this function only to implement the copy constructor and overload the assignment operator. To copy a stack into another stack, the program can use the assignment operator.

Figure 18-6 shows this data structure, wherein `stack` is an object of type `stackType`. Note that `stackTop` can range from 0 to `maxStackSize`. If `stackTop` is nonzero, then `stackTop - 1` is the index of the top element of the stack. Suppose that `maxStackSize = 100`.

The definition of the function `initializeStack` is:

```cpp
template <class Type>
void stackType<Type>::initializeStack()
{
    stackTop = 0;
}//end initializeStack
```

### Empty Stack

We have seen that the value of `stackTop` indicates whether the stack is empty. If `stackTop` is 0, the stack is empty; otherwise, the stack is not empty. The definition of the function `isEmptyStack` is:

```cpp
template <class Type>
bool stackType<Type>::isEmptyStack() const
{
    return (stackTop == 0);
}//end isEmptyStack
```

### Full Stack

Next, we consider the operation `isFullStack`. It follows that the stack is full if `stackTop` is equal to `maxStackSize`. The definition of the function `isFullStack` is:

```cpp
template <class Type>
bool stackType<Type>::isFullStack() const
{
    return (stackTop == maxStackSize);
}//end isFullStack
```

### Push

Adding, or pushing, an element onto the stack is a two-step process. Recall that the value of `stackTop` indicates the number of elements in the stack, and `stackTop - 1` gives the position of the top element of the stack. Therefore, the push operation is as follows:

1. Store the `newItem` in the array component indicated by `stackTop`.
2. Increment `stackTop`.

Figures 18-8 and 18-9 illustrate the push operation.

Suppose that before the push operation, the stack is as shown in Figure 18-8.

![](img/f97f778697507bb6fdd80c5991210cba_1134_0.png)

**FIGURE 18-8** Stack before pushing *y*

Assume `newItem` is `'y'`. After the push operation, the stack is as shown in Figure 18-9.

![](img/f97f778697507bb6fdd80c5991210cba_1134_1.png)

**FIGURE 18-9** Stack after pushing *y*

Using the previous algorithm, the definition of the function `push` is:

```cpp
template <class Type>
void stackType<Type>::push(const Type& newItem)
{
    if (!isFullStack())
    {
        list[stackTop] = newItem;    //add newItem to the
                                     //top of the stack
        stackTop++;                   //increment stackTop
    }
    else
        cout << "Cannot add to a full stack." << endl;
}//end push
```

If we try to add a new item to a full stack, the resulting condition is called an **overflow**. Error checking for an overflow can be handled in different ways. One way is as shown previously. Or, we can check for an overflow before calling the function `push`, as shown next (assuming `stack` is an object of type `stackType`).

```cpp
if (!stack.isFullStack())
    stack.push(newItem);
```

### Return the Top Element

The operation `top` returns the top element of the stack. Its definition is:

```cpp
template <class Type>
Type stackType<Type>::top() const
{
    assert(stackTop != 0);          //if stack is empty,
                                     //terminate the program
    return list[stackTop - 1];      //return the element of the
                                     //stack indicated by
                                     //stackTop - 1
}//end top
```

### Pop

To remove, or pop, an element from the stack, we simply decrement `stackTop` by 1.

Figures 18-10 and 18-11 illustrate the pop operation.

Suppose that before the pop operation, the stack is as shown in Figure 18-10.
