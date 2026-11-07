
The elements at the bottom of the stack have been in the stack the longest. The top element of the stack is the last element added to the stack. Because the elements are added and removed from one end (that is, the top), it follows that the item that is added last will be removed first. For this reason, a stack is also called a **Last In First Out (LIFO)** data structure.

**Stack:** A data structure in which the elements are added and removed from one end only; a Last In First Out (LIFO) data structure.

Now that you know what a stack is, let us see what kinds of operations can be performed on a stack. Because new items can be added to the stack, we can perform the add operation, called **push**, to add an element onto the stack. Similarly, because the top item can be retrieved and/or removed from the stack, we can perform the operation **top** to retrieve the top element of the stack and the operation **pop** to remove the top element from the stack.

The **push**, **top**, and **pop** operations work as follows: Suppose there are boxes lying on the floor that need to be stacked on a table. Initially, all of the boxes are on the floor, and the stack is empty (see Figure 17-2).

![](img/b217c421655b51e7494cf3b89bb5432d_1230_0.png)

**FIGURE 17-2** Empty stack

First, we push box **A** onto the stack. After the push operation, the stack is as shown in Figure 17-3(a).

![](img/b217c421655b51e7494cf3b89bb5432d_1230_1.png)

**FIGURE 17-3** Stack operations

```cpp
virtual bool isFullStack() const = 0;
//Function to determine whether the stack is full.
//Postcondition: Returns true if the stack is full,
//               otherwise returns false.

virtual void push(const Type& newItem) = 0;
//Function to add newItem to the stack.
//Precondition: The stack exists and is not full.
//Postcondition: The stack is changed and newItem
//               is added to the top of the stack.

virtual Type top() const = 0;
//Function to return the top element of the stack.
//Precondition: The stack exists and is not empty.
//Postcondition: If the stack is empty, the program
//               terminates; otherwise, the top element
//               of the stack is returned.

virtual void pop() = 0;
//Function to remove the top element of the stack.
//Precondition: The stack exists and is not empty.
//Postcondition: The stack is changed and the top
//               element is removed from the stack.
};
```

Figure 17-4 shows the UML class diagram of the class stackADT.

![](img/b217c421655b51e7494cf3b89bb5432d_1232_0.png)

**FIGURE 17-4** UML class diagram of the class stackADT

We now consider the implementation of our abstract stack data structure. Because all of the elements of a stack are of the same type, a stack can be implemented as either an array or a linked structure. Both implementations are useful and are discussed in this chapter.

## Implementation of Stacks as Arrays

Because all of the elements of a stack are of the same type, you can use an array to implement a stack. The first element of the stack can be put in the first array slot, the second element of the stack in the second array slot, and so on. The top of the stack is the index of the last element added to the stack.

In this implementation of a stack, stack elements are stored in an array, and an array is a random access data structure; that is, you can directly access any element of the array. However, by definition, a stack is a data structure in which the elements are accessed (popped or pushed) at only one end—that is, a LIFO data structure. Thus, a stack element is accessed only through the top, not through the bottom or middle. This feature of a stack is extremely important and must be recognized in the beginning.

To keep track of the top position of the array, we can simply declare another variable called stackTop.

The following class stackType implements the functions of the abstract class stackADT. By using a pointer, we can dynamically allocate arrays, so we will leave it for the user to specify the size of the array (that is, the stack size). We assume that the default stack size is 100. Because the class stackType has a pointer member variable (the pointer to the array to store the stack elements), we must overload the assignment operator and include the copy constructor and destructor. Moreover, we give a generic definition of the stack. Depending on the specific application, we can pass the stack element type when we declare a stack object.

```cpp
template <class Type>
class stackType: public stackADT<Type>
{
public:
    const stackType<Type>& operator=(const stackType<Type>&);
        //Overload the assignment operator.

    void initializeStack();
        //Function to initialize the stack to an empty state.
        //Postcondition: stackTop = 0

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
        //              is added to the top of the stack.
        //

    Type top() const;
        //Function to return the top element of the stack.
        //Precondition: The stack exists and is not empty.
        //Postcondition: If the stack is empty, the program
        //              terminates; otherwise, the top element
        //              of the stack is returned.
        //

    void pop();
        //Function to remove the top element of the stack.
        //Precondition: The stack exists and is not empty.
        //Postcondition: The stack is changed and the top
        //              element is removed from the stack.
        //

    stackType(int stackSize = 100);
        //Constructor
        //Create an array of the size stackSize to hold
        //the stack elements. The default stack size is 100.
        //Postcondition: The variable list contains the base
        //              address of the array, stackTop = 0, and
        //              maxStackSize = stackSize.

    stackType(const stackType<Type>& otherStack);
        //Copy constructor

    ~stackType();
        //Destructor
        //Remove all the elements from the stack.
        //Postcondition: The array (list) holding the stack
        //              elements is deleted.

private:
    int maxStackSize;  //variable to store the maximum stack size
    int stackTop;      //variable to point to the top of the stack
    Type *list;        //pointer to the array that holds the
                       //stack elements

    void copyStack(const stackType<Type>& otherStack);
        //Function to make a copy of otherStack.
        //Postcondition: A copy of otherStack is created and
        //              assigned to this stack.
};
```

Figure 17-5 shows the UML class diagram of the class stackType.

![](img/b217c421655b51e7494cf3b89bb5432d_1235_0.png)

**FIGURE 17-5** UML class diagram of the class `stackType`

> Because C++ arrays begin with the index 0, we need to distinguish between the value of `stackTop` and the array position indicated by `stackTop`. If `stackTop` is 0, the stack is empty; if `stackTop` is nonzero, then the stack is nonempty and the top element of the stack is given by `stackTop`.
> 
> Note that the function `copyStack` is included as a *private* member. This is because we want to use this function only to implement the copy constructor and overload the assignment operator. To copy a stack into another stack, the program can use the assignment operator.

Figure 17-6 shows this data structure, wherein `stack` is an object of type `stackType`. Note that `stackTop` can range from 0 to `maxStackSize`. If `stackTop` is nonzero, then `stackTop - 1` is the index of the `stackTop` element of the stack. Suppose that `maxStackSize = 100`.
