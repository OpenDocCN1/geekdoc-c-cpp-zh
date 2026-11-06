
begin from the front of the list. Searching for someone whose name begins with a letter near the end of the alphabet might begin from the back of the list.

In a circular, doubly linked list (Fig. 20.12), the forward pointer of the last node points to the first node, and the backward pointer of the first node points to the last node, thus closing the “circle.”

![](img/023f159fdd47d944d48e08843cea732d_860_0.png)

Fig. 20.12 | Circular, doubly linked list.

## 20.5 Stacks

Chapter 14, Templates, explained the notion of a stack class template with an underlying array implementation. In this section, we use an underlying pointer-based linked-list implementation. We also discuss stacks in Chapter 22, Standard Template Library (STL).

A stack data structure allows nodes to be added to the stack and removed from the stack only at the top. For this reason, a stack is referred to as a last-in, first-out (LIFO) data structure. One way to implement a stack is as a constrained version of a linked list. In such an implementation, the link member in the last node of the stack is set to null (zero) to indicate the bottom of the stack.

The primary member functions used to manipulate a stack are push and pop. Function push inserts a new node at the top of the stack. Function pop removes a node from the top of the stack, stores the popped value in a reference variable that is passed to the calling function and returns true if the pop operation was successful (false otherwise).

Stacks have many interesting applications. For example, when a function call is made, the called function must know how to return to its caller, so the return address is pushed onto a stack. If a series of function calls occurs, the successive return values are pushed onto the stack in last-in, first-out order, so that each function can return to its caller. Stacks support recursive function calls in the same manner as conventional nonrecursive calls. Section 6.11 discusses the function call stack in detail.

Stacks provide the memory for, and store the values of, automatic variables on each invocation of a function. When the function returns to its caller or throws an exception, the destructor (if any) for each local object is called, the space for that function’s automatic variables is popped off the stack and those variables are no longer known to the program.

Stacks are used by compilers in the process of evaluating expressions and generating machine-language code. The exercises explore several applications of stacks, including using them to develop your own complete working compiler.

We’ll take advantage of the close relationship between lists and stacks to implement a stack class primarily by reusing a list class. First, we implement the stack class through private inheritance of the list class. Then we implement an identically performing stack class through composition of the list class as a private member of a stack class. Of course, all of the data structures in this chapter, including these two stack classes, are implemented as templates to encourage further reusability.

The program of Figs. 20.13–20.14 creates a Stack class template (Fig. 20.13) primarily through private inheritance (line 9) of the List class template of Fig. 20.4. We want the Stack to have member functions push (lines 13–16), pop (lines 19–22), isStackEmpty (lines 25–28) and printStack (lines 31–34). Note that these are essentially the insertAtFront, removeFromFront, isEmpty and print functions of the List class template. Of course, the List class template contains other member functions (i.e., insertAtBack and removeFromBack) that would not make accessible through the public interface to the Stack class. So when we indicate that the Stack class template is to inherit from the List class template, we specify private inheritance. This makes all the List class template’s member functions private in the Stack class template. When we implement the Stack’s member functions, we then have each of these call the appropriate member function of the List class—push calls insertAtFront (line 15), pop calls removeFromFront (line 21), isStackEmpty calls isEmpty (line 27) and printStack calls print (line 33)—this is referred to as delegation.

```cpp
// Fig. 20.13: Stack.h
// Template Stack class definition derived from class List.
#ifndef STACK_H
#define STACK_H

#include "List.h" // List class definition

template< typename STACKTYPE >
class Stack : private List< STACKTYPE >
{
public:
   // push calls the List function insertAtFront
   void push( const STACKTYPE &data )
   {
      insertAtFront( data );
   } // end function push

   // pop calls the List function removeFromFront
   bool pop( STACKTYPE &data )
   {
      return removeFromFront( data );
   } // end function pop

   // isStackEmpty calls the List function isEmpty
   bool isStackEmpty() const
   {
      return this->isEmpty();
   } // end function isStackEmpty
```

Fig. 20.13  |  Stack class-template definition. (Part 1 of 2.)

```text
The list is: 3.3 2.2 1.1
3.3 popped from stack
The list is: 2.2 1.1
2.2 popped from stack
The list is: 1.1
1.1 popped from stack
The list is empty
All nodes destroyed
All nodes destroyed
```

Fig. 20.14 | A simple stack program. (Part 3 of 3.)

Another way to implement a Stack class template is by reusing the List class template through composition. Figure 20.15 is a new implementation of the Stack class template that contains a List< STACKTYPE > object called stackList (line 38). This version of the Stack class template uses class List from Fig. 20.4. To test this class, use the driver program in Fig. 20.14, but include the new header file—Stackcomposition.h in line 6 of that file. The output of the program is identical for both versions of class Stack.

```cpp
// Fig. 20.15: Stackcomposition.h
// Template Stack class definition with composed List object.
#ifndef STACKCOMPOSITION_H
#define STACKCOMPOSITION_H

#include "List.h" // List class definition

template< typename STACKTYPE >
class Stack
{
public:
   // no constructor; List constructor does initialization

   // push calls stackList object's insertAtFront member function
   void push( const STACKTYPE &data )
   {
      stackList.insertAtFront( data );
   } // end function push

   // pop calls stackList object's removeFromFront member function
   bool pop( STACKTYPE &data )
   {
      return stackList.removeFromFront( data );
   } // end function pop

   // isStackEmpty calls stackList object's isEmpty member function
   bool isStackEmpty() const
   {
      return stackList.isEmpty();
   } // end function isEmpty

   // printStack calls stackList object's print member function
   void printStack() const
   {
      stackList.print();
   } // end function printStack

private:
   List< STACKTYPE > stackList; // composed List object
}; // end class Stack
#endif
```

Fig. 20.15 | Stack class template with a composed List object. (Part 1 of 2.)

Fig. 20.15 | Stack class template with a composed List object. (Part 2 of 2.)

## 20.6 Queues

A queue is similar to a supermarket checkout line—the first person in line is serviced first, and other customers enter the line at the end and wait to be served. Queue nodes are removed only from the head of the queue and are inserted only at the tail of the queue. For this reason, a queue is referred to as a first-in, first-out (FIFO) data structure. The insert and remove operations are known as enqueue and dequeue.

Queues have many applications in computer systems. Computers that have a single processor can service only one user at a time. Entries for the other users are placed in a queue. Each entry gradually advances to the front of the queue as users receive service. The entry at the front of the queue is the next to receive service.

Queues are also used to support print spooling. For example, a single printer might be shared by all users of a network. Many users can send print jobs to the printer, even when the printer is already busy. These print jobs are placed in a queue until the printer becomes available. A program called a spooler manages the queue to ensure that, as each print job completes, the next print job is sent to the printer.

Information packets also wait in queues in computer networks. Each time a packet arrives at a network node, it must be routed to the next node on the network along the path to the packet's final destination. The routing node routes one packet at a time, so additional packets are enqueued until the router can route them.

A file server in a computer network handles file access requests from many clients throughout the network. Servers have a limited capacity to service requests from clients. When that capacity is exceeded, client requests wait in queues.

The program of Figs. 20.16–20.17 creates a Queue class template (Fig. 20.16) through private inheritance (line 9) of the List class template (Fig. 20.4). The Queue has member functions enqueue (lines 13–16), dequeue (lines 19–22), isEmptyQueue (lines 25–28) and printQueue (lines 31–34). These are essentially the insertAtBack, removeFront, isEmpty and print functions of the List class template. Of course, the List class template contains other member functions that we do not want to make accessible through the public interface to the Queue class. So when we indicate that the Queue class template is to inherit the List class template, we specify private inheritance. This makes all the List class template's member functions private in the Queue class template. When
