
![](img/b217c421655b51e7494cf3b89bb5432d_1258_0.png)

FIGURE 17-15 Stack before the pop operation

Figure 17-16 shows the pop operation.

![](img/b217c421655b51e7494cf3b89bb5432d_1258_1.png)

FIGURE 17-16 Pop operation

The statement

```cpp
temp = stackTop;
```

makes temp point to the top of the stack. See Figure 17-16(a). Next, the statement

```cpp
stackTop = stackTop->link;
```

makes the second element of the stack become the top element of the stack. See Figure 17-16(b).

Finally, the statement

```cpp
delete temp;
```

deallocates the memory pointed to by **temp**. See Figure 17-16(c).

The definition of the function pop is as follows:

```cpp
template <class Type>
void linkedStackType<Type>::pop()
{
        nodeType<Type> *temp;    //pointer to deallocate memory

        if (stackTop != nullptr)
        {
                temp = stackTop;        //set temp to point to the top node

                stackTop = stackTop->link;        //advance stackTop to the
                                                  //next node

                delete temp;        //delete the top node
        }
        else
                cout << "Cannot remove from an empty stack." << endl;
}//end pop
```

## Copy Stack

The function **copyStack** makes an identical copy of a stack. Its definition is similar to the definition of **copyList** for linked lists, given in Chapter 16. The definition of the function **copyStack** is as follows:

```cpp
template <class Type>
void linkedStackType<Type>::copyStack
                    (const linkedStackType<Type>& otherStack)
{
        nodeType<Type> *newNode, *current, *last;

        if (stackTop != nullptr) //if stack is nonempty, make it empty
                initializeStack();

        if (otherStack.stackTop == nullptr)
                stackTop = nullptr;
        else
        {
                current = otherStack.stackTop;  //set current to point
                                                //to the stack to be copied

                //copy the stackTop element of the stack
                stackTop = new nodeType<Type>;  //create the node

                stackTop->info = current->info; //copy the info
                stackTop->link = nullptr;    //set the link field of the
                                              //node to nullptr
                last = stackTop;              //set last to point to the node
                current = current->link;      //set current to point to
                                              //the next node

                //copy the remaining stack
                while (current != nullptr)
                {
                    newNode = new nodeType<Type>;
                    newNode->info = current->info;
                    newNode->link = nullptr;
                    last->link = newNode;
                    last = newNode;
                    current = current->link;
                }//end while
        }//end else
}//end copyStack
```

### Constructors and Destructors

We have already discussed the default constructor. To complete the implementation of the stack operations, next we give the definitions of the functions to implement the copy constructor and the destructor and to overload the assignment operator. (These functions are similar to those discussed for linked lists in Chapter 16.)

```cpp
//copy constructor
template <class Type>
linkedStackType<Type>::linkedStackType
                         (const linkedStackType<Type>& otherStack)
{
    stackTop = nullptr;
    copyStack(otherStack);
}//end copy constructor

//destructor
template <class Type>
linkedStackType<Type>::~linkedStackType()
{
    initializeStack();
}//end destructor
```

### Overloading the Assignment Operator (=)

The definition of the function to overload the assignment operator for the class `linkedStackType` is as follows:

```cpp
template <class Type>
const linkedStackType<Type>& linkedStackType<Type>::operator=
                         (const linkedStackType<Type>& otherStack)
{
    if (this != &otherStack) //avoid self-copy
        copyStack(otherStack);

    return *this;
}//end operator=
```

The definition of a stack and the functions to implement the stack operations discussed previously are generic. Also, as in the case of an array representation of a stack, in the linked representation of a stack, we must put the definition of the stack and the functions to implement the stack operations together in a (header) file. A client’s program can include this header file via the include statement.

Example 17-3 illustrates how a linkedStack object is used in a program.

### EXAMPLE 17-3

We assume that the definition of the class `linkedStackType` and the functions to implement the stack operations are included in the header file `"linkedStack.h"`.

```cpp
//This program tests various operations of a linked stack
#include <iostream>
#include "linkedStack.h"

using namespace std;

void testCopy(linkedStackType<int> OStack);

int main()
{
    linkedStackType<int> stack;
    linkedStackType<int> otherStack;
    linkedStackType<int> newStack;

        //Add elements into stack
    stack.push(28);
    stack.push(94);
    stack.push(37);

        //Use the assignment operator to copy the elements
        //of stack into newStack
    newStack = stack;

    cout << "After the assignment operator, newStack: "
         << endl;

        //Output the elements of newStack
    while (!newStack.isEmptyStack())
    {
        cout << newStack.top() << endl;
        newStack.pop();
    }

//Use the assignment operator to copy the elements
//of stack into otherStack
otherStack = stack;

cout << "Testing the copy constructor." << endl;

testCopy(otherStack);

cout << "After the copy constructor, otherStack: " << endl;

while (!otherStack.isEmptyStack())
{
    cout << otherStack.top() << endl;
    otherStack.pop();
}
return 0;
}

//Function to test the copy constructor
void testCopy(linkedStackType<int> OStack)
{
    cout << "Stack in the function testCopy:" << endl;

    while (!OStack.isEmptyStack())
    {
        cout << OStack.top() << endl;
        OStack.pop();
    }
}
```

### Sample Run:

```text
After the assignment operator, newStack:
37
94
28
Testing the copy constructor.
Stack in the function testCopy:
37
94
28
After the copy constructor, otherStack:
37
94
28
```

## Stack as Derived from the `class unorderedLinkedList`

If we compare the push function of the stack with the insertFirst function discussed for general lists in Chapter 16, we see that the algorithms to implement these operations are similar. A comparison of other functions—such as initializeStack and initializeList, isEmptyList and isEmptyStack, and so on—suggests that the class linkedStackType can be derived from the class linkedListType. Moreover, the functions pop and isFullStack can be implemented as in the previous section. Note that the class linkedListType is an abstract and does not implement all of the operations. However, the class unorderedLinkedListType is derived from the class linkedListType and provides the definitions of the abstract functions of the class linkedListType. Therefore, we can derive the class linkedStackType from the class unorderedLinkedListType. Next, we define the class linkedStackType that is derived from the class unorderedLinkedList. The definitions of the functions to implement the stack operations are also given.

```cpp
#include <iostream>
#include "unorderedLinkedList.h"

using namespace std;

template <class Type>
class linkedStackType: public unorderedLinkedList<Type>
{
public:
    void initializeStack();
    bool isEmptyStack() const;
    void push(const Type& newItem);
    Type top() const;
    void pop();
};

template <class Type>
void linkedStackType<Type>::initializeStack()
{
    unorderedLinkedList<Type>::initializeList();
}

template <class Type>
bool linkedStackType<Type>::isEmptyStack() const
{
    return unorderedLinkedList<Type>::isEmptyList();
}

template <class Type>
bool linkedStackType<Type>::isFullStack() const
{
    return false;
}

template <class Type>
void linkedStackType<Type>::push(const Type& newElement)
{
    unorderedLinkedList<Type>::insertFirst(newElement);
}

template <class Type>
Type linkedStackType<Type>::top() const
{
    return unorderedLinkedList<Type>::front();
}

template <class Type>
void linkedStackType<Type>::pop()
{
    nodeType<Type> *temp;

    temp = first;
    first = first->link;
    delete temp;
}
```

## Application of Stacks: Postfix Expressions Calculator

The usual notation for writing arithmetic expressions (the notation we learned in elementary school) is called **infix notation**, in which the operator is written between the operands. For example, in the expression $a + b$, the operator + is between the operands $a$ and $b$. In infix notation, the operators have precedence. That is, we must evaluate expressions from left to right, and multiplication and division have higher precedence than do addition and subtraction. If we want to evaluate the expression in a different order, we must include parentheses. For example, in the expression $a + b * c$, we first evaluate * using the operands $b$ and $c$, and then we evaluate + using the operand $a$ and the result of $b * c$.

In the early 1920s, the Polish mathematician Jan Lukasiewicz discovered that if operators were written before the operands (**prefix** or **Polish notation**; for example, $+\ a\ b$), the parentheses could be omitted. In the late 1950s, the Australian philosopher and early computer scientist Charles L. Hamblin proposed a scheme in which operators follow the operands (postfix operators), resulting in the **Reverse Polish** notation. This has the advantage that the operators appear in the order required for computation.

For example, the expression

$a + b * c$

in a postfix expression is

$a\ b\ c\ *\ +$

The following example shows various infix expressions and their equivalent postfix expressions.
