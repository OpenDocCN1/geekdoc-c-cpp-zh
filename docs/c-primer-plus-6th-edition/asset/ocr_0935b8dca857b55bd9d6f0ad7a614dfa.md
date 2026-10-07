Abstract Data Types 553

data is always added or deleted from the top of the stack. For example, C++ programs use a stack to manage automatic variables.As new automatic variables are generated, they are added to the top of the stack.When they expire, they are removed from the stack. Let's look at the properties of a stack in a general, abstract way. First, a stack holds several items. (That property makes it a container, an even more general abstraction.) Next, a stack is characterized by the operations you can perform on it:

+   - You can create an empty stack.
- You can add an item to the top of a stack (that is, you can push an item).
- You may remove an item from the top (that is, you can pop an item).
- You can check whether the stack is full.
- You can check whether the stack is empty.

You can match this description with a class declaration in which the public member functions provide an interface that represents the stack operations.The private members take care of storing the stack data. The class concept is a nice touch to the ADT approach.
The private section has commit itself to how to handle the data. For example, you can use an ordinary array, a dynamically allocated array, or more data structures, such as a linked list. However the public interface should hide the representation. Instead, it should be expressed in general terms, such as creating a stack, pushing an item, and so on. Listing 10.10 shows one approach. It assumes that the bool type has been implemented. If it hasn't been implemented on your system, you can use int, 0, and 1 rather than bool, false, and true.

Listing 10.10 stack.h

```
// stack.h -- class definition for the stack ADT
#ifndef STACK_H
#define STACK_H_
```

```
class Stack
{
private:
    enum {MAX = 10};       // constant specific to class
    Item items[MAX];        // holds stack items
    int top;                // index for top stack item
public:
    Stack();
    bool isEmpty() const;
    bool isfull() const;
    // push() returns false if stack already is full, true otherwise
    bool push(Item item&); // add item to stack
```