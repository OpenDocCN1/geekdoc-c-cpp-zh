
Programming Tip: When an exception can occur within a loop, you must decide whether to place a try block within the body of the loop—in which case an exception will be caught each time the loop cycles (as in the first example)—or place the entire loop within a try block—in which case the exception would be caught only once (as in the second example). Neither choice is better than the other, but if you make the wrong choice, the client likely will not get the necessary information.

Note: Sometimes a catch block will intentionally terminate program execution. When the block does not do so, but rather completes its execution, any statements that appear after the last catch block execute next.

## C3.5 Programmer-Defined Exception Classes

You may find that the C++ Standard Library has an exception class already defined that suits the exception needs of your program. You may also want to define your own exception class. Usually, the C++ exception class exception, or one of its derived classes, is the base class for programmer-defined exception classes. Adhering to this practice provides a standardized interface for working with exceptions. If you follow this practice, you will need to use the std namespace.

An exception class typically consists of a constructor that has a string parameter. For example, you can define the class TargetNotFoundException as

```
#include <stdexcept>
#include <string>
using namespace std;

class TargetNotFoundException: public exception
{
public :
   TargetNotFoundException(const string& message = "")
      : exception("Target not found: " + message.c_str())
   { // end constructor
   }; // end class TargetNotFoundException
```

The constructor provides a way for a throw statement to identify the condition that caused the exception. For example, the statement

```
throw TargetNotFoundException(target + " not found in a box");
```

invokes the constructor of TargetNotFoundException. The message given to the constructor is returned by the method what that is inherited from the class exception. Thus, a catch block, such as the following one, can access the message:

```
catch(TargetNotFoundException except)
{
   cout << except.what() << endl;
}
```

If target has the value "glasses" when this block executes, the output is

Target not found: glasses not found in a box!

While the string message is helpful, sometimes we want to return additional information to the client to help resolve the problem. We could add a private data field to our exception class to store additional error details. A second parameter in the constructor to receive an initial value for those details, as well as a public accessor method so that the client can retrieve them, are also needed. When a method throws this exception, it would call the constructor and send it the extra data and the message as its two arguments.

## Programming Tip: Using exceptions

To throw an exception in a function:

- Determine what errors, preconditions, postconditions, and unusual conditions you must check and where they should be checked, so your function can correctly perform its task.
- Detect the error, precondition, postcondition, or unusual condition. Usually this is done with an if statement.
- If an error condition has occurred, throw an exception using the throw statement. As an argument to the exception class constructor, pass a string description of the reason for the error.
- Add a throw clause to the function header indicating the exceptions thrown by the function.
- Derive a custom exception class to better identify the conditions that caused the error. Although doing so is optional, it is desirable.

To handle an exception or use a function that could throw an exception

- Place the statement that might throw an exception in a try block. The fewer statements in the try block the better. Do not use new to create an object in a try block.
- After the try block, place catch blocks for each type of exception that can be thrown by the statements in the try block. Place the catch blocks in order from the most specific exception classes to the more general exception classes.

## Implementations of the ADT Stack

## Chapter 7

- Contents
- 7.1 An Array-Based Implementation 242
- 7.2 A Link-Based implementation 245
- 7.3 Implementations That Use Exceptions 249

- Summary 251
- Exercises 251
- Programming Problems 252

- Prerequisites
- Chapter 3 Array-Based Implementations
- C++ Interlude 2 Pointers, Polymorphism, and Memory Allocation
- Chapter 4 Link-Based Implementations
- Chapter 6 Stacks
- C++ Interlude 3 Exceptions

This chapter implements the ADT stack using the techniques we described in Chapters 3 and 4 for the ADT bag. We first will use an array and then a chain of linked nodes to store the stack's entries. You should be happy to discover the simplicity and efficiency of these implementations. We then will modify these implementations to use exceptions as a way for a method to signal an unusual occurrence, such as an attempt to get an entry from an empty stack.

## 7.1 An Array-Based Implementation

Figure 7-1a shows a sketch of an array that contains the entries in a stack. Where in the array should the top entry be? Since entries are added or removed at the top of the stack, we can avoid shifting the current entries if we anchor the bottom of the stack at index 0 and track the location of the stack's top using an index top. Then if the array is and items[top] is the top entry, items and top can be the private data members of our class of stacks. Figure 7-1b illustrates these details. Notice that the top of the stack in this figure is at index 2. We can either add a new entry at index[3] and then increment top or remove the top entry in index[2] by decrementing top to 1.

Our class will have a default constructor to initialize the private data members items and top. However, since we plan to store a stack's entries in statically allocated memory, the compiler-generated destructor and copy constructor will be sufficient. If, on the other hand, we were to use a dynamically allocated array, we would have to define a destructor and a copy constructor.

Listing 7-1 shows the header file for an array-based implementation of the ADT stack. Comments describing the methods are in Listing 6-1 of Chapter 6.

### FIGURE 7-1 Using an array to store a stack's entries: (a) a preliminary sketch; (b) implementation details

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_268_0.png)

### LISTING 7-1 The header file for an array-based stack

```
/* ADT stack: Array-based implementation.
   File ArrayStack.h */
#ifndef _ARRAY_STACK
#define _ARRAY_STACK
#include "StackInterface.h"
const int MAX_STACK = maximum-size-of-stack;
template<class ItemType>
class ArrayStack : public StackInterface<ItemType>
{
private:
   ItemType items[MAX_STACK]; // Array of stack items
   int top; // Index to top of stack
public:
    ArrayStack(); // Default constructor
    bool isEmpty() const;
    bool push(const ItemType& newEntry);
    bool pop();
    ItemType peek() const;
}; // end ArrayStack

#include "ArrayStack.cpp"
#endif
```

The implementations of the methods that the previous header file declares are given in Listing 7-2. These definitions are straightforward, but notice that the method peek uses assert to enforce its precondition that the stack contain at least one entry. Later in this chapter, we will revise peek to throw an exception if the client calls it when the stack is empty.

### LISTING 7-2 The implementation file for an array-based stack

/* @file ArrayStack.cpp */

#include <cassert> // For assert
#include "ArrayStack.h" // Header file

template<class ItemType>
ArrayStack<ItemType>::ArrayStack() : top(-1)
{ } // end default constructor

// Copy constructor and destructor are supplied by the compiler

template<class ItemType>
bool ArrayStack<ItemType>::isEmpty() const
{
   return top < 0;
} // end isEmpty

template<class ItemType>
bool ArrayStack<ItemType>::push(const ItemType& newEntry)
{
   bool result = false;
   if (top < MAX_STACK - 1) // Does stack have room for newEntry?
   {
      top++;
      items[top] = newEntry;
      result = true;
   } // end if

   return result;
} // end push

template<class ItemType>
bool ArrayStack<ItemType>::pop()

(continues)
