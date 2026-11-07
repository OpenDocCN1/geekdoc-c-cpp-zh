
![](img/d0be7fc6d804b63484835c6c8bc67a07_1215_0.png)

## CHAPTER 17

## STACKS AND QUEUES

IN THIS CHAPTER, YOU WILL:

- 1. Learn about stacks
- 2. Examine various stack operations
- 3. Learn how to implement a stack as an array
- 4. Learn how to implement a stack as a linked list
- 5. Learn about infix, prefix, and postfix expressions, and how to use a stack to evaluate postfix expressions
- 6. Learn how to use a stack to remove recursion
- 7. Learn about queues
- 8. Examine various queue operations
- 9. Learn how to implement a queue as an array
- 10. Learn how to implement a queue as a linked list
- 11. Discover how to use queues to solve simulation problems

This chapter discusses two very useful data structures: stacks and queues. Both stacks and queues have numerous applications in computer science.

### Stacks

Suppose that you have a program with several functions. To be specific, suppose that you have functions A, B, C, and D in your program. Now suppose that function A calls function B, function B calls function C, and function C calls function D. When function D terminates, control goes back to function C; when function C terminates, control goes back to function B; and when function B terminates, control goes back to function A. During program execution, how do you think the computer keeps track of the function calls? What about recursive functions? How does the computer keep track of the recursive calls? In Chapter 16, we designed a recursive function to print a linked list backward. What if you want to write a nonrecursive algorithm to print a linked list backward?

This section discusses the data structure called the **stack**, which the computer uses to implement function calls. You can also use stacks to convert recursive algorithms into nonrecursive algorithms, especially recursive algorithms that are not tail recursive. Stacks have numerous applications in computer science. After developing the tools necessary to implement a stack, we will examine some applications of stacks.

A stack is a list of homogeneous elements in which the addition and deletion of elements occur only at one end, called the **top** of the stack. For example, in a cafeteria, the second tray in a stack of trays can be removed only if the first tray has been removed. For another example, to get to your favorite computer science book, which is underneath your math and history books, you must first remove the math and history books. After removing these books, the computer science book becomes the top book—that is, the top element of the stack. Figure 17-1 shows some examples of stacks.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1216_0.png)

**FIGURE 17-1** Various types of stacks

The elements at the bottom of the stack have been in the stack the longest. The top element of the stack is the last element added to the stack. Because the elements are added and removed from one end (that is, the top), it follows that the item that is added last will be removed first. For this reason, a stack is also called a **Last In First Out (LIFO)** data structure.

**Stack:** A data structure in which the elements are added and removed from one end only; a **Last In First Out (LIFO)** data structure.

Now that you know what a stack is, let us see what kinds of operations can be performed on a stack. Because new items can be added to the stack, we can perform the add operation, called **push**, to add an element onto the stack. Similarly, because the top item can be retrieved and/or removed from the stack, we can perform the operation **top** to retrieve the top element of the stack and the operation **pop** to remove the top element from the stack.

The **push**, **top**, and **pop** operations work as follows: Suppose there are boxes lying on the floor that need to be stacked on a table. Initially, all of the boxes are on the floor, and the stack is empty (see Figure 17-2).

![](img/d0be7fc6d804b63484835c6c8bc67a07_1217_0.png)

**FIGURE 17-2** Empty stack

First, we push box A onto the stack. After the push operation, the stack is shown in Figure 17-3(a).

![](img/d0be7fc6d804b63484835c6c8bc67a07_1217_1.png)

**FIGURE 17-3** Stack operations

We then push box B onto the stack. After this push operation, the stack is as shown in Figure 17-3(b). Next, we push box C onto the stack. After this push operation, the stack is as shown in Figure 17-3(c). Next, we look, that is, peek, at the top element of the stack. After this operation, the stack is unchanged and shown in Figure 17-3(d). We then push box D onto the stack. After this push operation, the stack is as shown in Figure 17-3(e). Next, we pop the stack. After this pop operation, the stack is as shown in Figure 17-3(f).

An element can be removed from the stack only if there is something in the stack, and an element can be added to the stack only if there is room. The two operations that immediately follow from push, top, and pop are **isFullStack** (checks whether the stack is full) and **isEmptyStack** (checks whether the stack is empty). Because a stack keeps changing as we add and remove elements, the stack must be empty before we first start using it. Thus, we need another operation, called **initializeStack**, which initializes the stack to an empty state. Therefore, to successfully implement a stack, we need at least these six operations, which are described in the next section. We might also need other operations on a stack, depending on the specific implementation.

### Stack Operations

- **initializeStack**: Initializes the stack to an empty state.
- **isEmptyStack**: Determines whether the stack is empty. If the stack is empty, it returns the value true; otherwise, it returns the value false.
- **isFullStack**: Determines whether the stack is full. If the stack is full, it returns the value true; otherwise, it returns the value false.
- **push**: Adds a new element to the top of the stack. The input to this operation consists of the stack and the new element. Prior to this operation, the stack must exist and must not be full.
- **top**: Returns the top element of the stack. Prior to this operation, the stack must exist and must not be empty.
- **pop**: Removes the top element of the stack. Prior to this operation, the stack must exist and must not be empty.

The following abstract class StackADT defines these operations as an ADT:

```cpp
template <class Type>
class StackADT
{
public:
    virtual void initializeStack() = 0;
        //Method to initialize the stack to an empty state.
        //Postcondition: Stack is empty.

    virtual bool isEmptyStack() const = 0;
        //Function to determine whether the stack is empty.
        //Postcondition: Returns true if the stack is empty,
        //              otherwise returns false.

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

Figure 17-4 shows the UML class diagram of the class `StackADT`.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1219_0.png)

**FIGURE 17-4** UML class diagram of the class `StackADT`

We now consider the implementation of our abstract stack data structure. Because all of the elements of a stack are of the same type, a stack can be implemented as either an array or a linked structure. Both implementations are useful and are discussed in this chapter.
