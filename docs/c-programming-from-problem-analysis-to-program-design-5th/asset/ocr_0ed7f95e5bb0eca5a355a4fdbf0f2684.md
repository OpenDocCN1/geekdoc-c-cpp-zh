```
```cpp
stackTop->link = NULL;   //set the link field of the
                         //node to NULL
last = stackTop;         //set last to point to the node
current = current->link; //set current to point to
                         //the next node

                         //copy the remaining stack
while (current != NULL)
{
    newNode = new nodeType<Type>;

    newNode->info = current->info;
    newNode->link = NULL;
    last->link = newNode;
    last = newNode;
    current = current->link;
}//end while
}//end else
}//end copyStack
```
```

# Constructors and Destructors

We have already discussed the default constructor. To complete the implementation of the stack operations, next we give the definitions of the functions to implement the copy constructor and the destructor and to overload the assignment operator. (These functions are similar to those discussed for linked lists in Chapter 18.)

```
```cpp
//copy constructor
template <class Type>
linkedStackType<Type>::linkedStackType(
                         const linkedStackType<Type>& otherStack)
{
    stackTop = NULL;
    copyStack(otherStack);
}//end copy constructor
```
```

```
```cpp
//destructor
template <class Type>
linkedStackType<Type>::~linkedStackType()
{
    initializeStack();
}//end destructor
```
```

# Overloading the Assignment Operator (=)

The definition of the function to overload the assignment operator for the class linkedStackType is:

```
```cpp
template <class Type>
const linkedStackType<Type>& linkedStackType<Type>::operator=
                         (const linkedStackType<Type>& otherStack)
```
```