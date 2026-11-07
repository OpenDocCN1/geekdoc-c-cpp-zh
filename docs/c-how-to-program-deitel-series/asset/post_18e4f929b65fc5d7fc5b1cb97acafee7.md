
```cpp
// Fig. 19.14: fig19_14.cpp
// A simple stack program.
#include <iostream>
#include "Stack.h" // Stack class definition
using namespace std;

int main()
{
   Stack< int > intStack; // create Stack of ints

   cout << "processing an integer Stack" << endl;

   // push integers onto intStack
   for ( int i = 0; i < 3; ++i )
   {
      intStack.push( i );
      intStack.printStack();
   } // end for

   int popInteger; // store int popped from stack

   // pop integers from intStack
   while ( !intStack.isStackEmpty() )
   {
      intStack.pop( popInteger );
      cout << popInteger << " popped from stack" << endl;
      intStack.printStack();
   } // end while

   Stack< double > doubleStack; // create Stack of doubles
   double value = 1.1;

   cout << "processing a double Stack" << endl;

   // push floating-point values onto doubleStack
   for ( int j = 0; j < 3; ++j )
   {
      doubleStack.push( value );
      doubleStack.printStack();
      value += 1.1;
   } // end for

   double popDouble; // store double popped from stack

   // pop floating-point values from doubleStack
   while ( !doubleStack.isStackEmpty() )
   {
      doubleStack.pop( popDouble );
      cout << popDouble << " popped from stack" << endl;
      doubleStack.printStack();
   } // end while
} // end main
```

Fig. 19.14 | A simple stack program. (Part 1 of 2.)

```cpp
processing an integer Stack
The list is: 0

The list is: 1 0

The list is: 2 1 0

2 popped from stack
The list is: 1 0

1 popped from stack
The list is: 0

0 popped from stack
The list is empty

processing a double Stack
The list is: 1.1

The list is: 2.2 1.1

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

**Fig. 19.14** | A simple stack program. (Part 2 of 2.)

## Implementing a Class Template Stack Class With Composition of a List Object

Another way to implement a Stack class template is by reusing the List class template through *composition*. Figure 19.15 is a new implementation of the Stack class template that contains a List<STACKTYPE> object called stackList (line 38). This version of the Stack class template uses class List from Fig. 19.5. To test this class, use the driver program in Fig. 19.14, but include the new header—Stackcomposition.h in line 4 of that file. The output of the program is identical for both versions of class Stack.

```cpp
// Fig. 19.15: Stackcomposition.h
// Stack class template with
// composed List object.
#ifndef STACKCOMPOSITION_H
#define STACKCOMPOSITION_H
```

Fig. 19.15 | Stack class template with a composed List object. (Part 1 of 2.)

- Queues are also used to support **print spooling**. For example, a single printer might be shared by all users of a network. Many users can send print jobs to the printer, even when the printer is already busy. These print jobs are placed in a queue until the printer becomes available. A program called a **spooler** manages the queue to ensure that, as each print job completes, the next print job is sent to the printer.
- Information packets also wait in queues in computer networks. Each time a packet arrives at a network node, it must be routed to the next node on the network along the path to the packet’s final destination. The routing node routes one packet at a time, so additional packets are enqueued until the router can route them.
- A file server in a computer network handles file access requests from many clients throughout the network. Servers have a limited capacity to service requests from clients. When that capacity is exceeded, client requests wait in queues.

## Implementing a Class Template Queue Class Based By Inheriting from List

The program of Figs. 19.16–19.17 creates a Queue class template (Fig. 19.16) through *private inheritance* (line 9) of the List class template from Fig. 19.5. The Queue has member functions enqueue (Fig. 19.16, lines 13–16), dequeue (lines 19–22), isQueueEmpty (lines 25–28) and printQueue (lines 31–34). These are essentially the insertAtBack, removeFromFront, isEmpty and print functions of the List class template. Of course, the List class template contains other member functions that we do *not* want to make accessible through the public interface to the Queue class. So when we indicate that the Queue class template is to inherit the List class template, we specify *private inheritance*. This makes all the List class template’s member functions private in the Queue class template. When we implement the Queue’s member functions, we have each of these call the appropriate member function of the list class—enqueue calls insertAtBack (line 15), dequeue calls removeFromFront (line 21), isQueueEmpty calls isEmpty (line 27) and printQueue calls print (line 33). As with the Stack example in Fig. 19.13, this *delegation requires explicit use of the this pointer* in isQueueEmpty and printQueue to avoid compilation errors.

```cpp
// Fig. 19.16: Queue.h
// Queue class-template definition.
#ifndef QUEUE_H
#define QUEUE_H

#include "List.h" // List class definition

template <typename QUEUETYPE >
class Queue : private List< QUEUETYPE >
{
public:
   // enqueue calls List member function insertAtBack
   void enqueue( const QUEUETYPE &data )
   {
      insertAtBack( data );
   } // end function enqueue
```

Fig. 19.16 | Queue class-template definition. (Part 1 of 2.)

are greater than the value in its parent node. Figure 19.19 illustrates a binary search tree with 9 values. Note that the shape of the binary search tree that corresponds to a set of data can vary, depending on the order in which the values are inserted into the tree.

![](img/b42ba5cd262b1358d16610173f975e4d_839_0.png)

## Implementing the Binary Search Tree Program

The program of Figs. 19.20–19.22 creates a binary search tree and traverses it (i.e., walks through all its nodes) three ways—using recursive inorder, preorder and postorder traversals. We explain these traversal algorithms shortly.

### Testing the Tree Class Template

We begin our discussion with the driver program (Fig. 19.20), then continue with the implementations of classes TreeNode (Fig. 19.21) and Tree (Fig. 19.22). Function main (Fig. 19.20) begins by instantiating integer tree intTree of type Tree< int > (line 10). The program prompts for 10 integers, each of which is entered in the binary tree by calling insertNode (line 19). The program then performs preorder, inorder and postorder traversals (these are explained shortly) of intTree (lines 23, 26 and 29, respectively). The program then instantiates floating-point tree doubleTree of type Tree< double > (line 31). The program prompts for 10 double values, each of which is inserted in the binary tree by calling insertNode (line 41). The program then performs preorder, inorder and postorder traversals of doubleTree (lines 45, 48 and 51, respectively).

```cpp
// Fig. 19.20: fig19_20.cpp
// Creating and traversing a binary tree.
#include <iostream>
#include <iomanip>
#include "Tree.h" // Tree class definition
using namespace std;

int main()
{
    Tree< int > intTree; // create Tree of int values

    cout << "Enter 10 integer values:\n";

// insert 10 integers to intTree
for ( int i = 1; i <= 10; ++i )
{
   int intValue = 0;
   cin >> intValue;
   intTree.insertNode( intValue );
} // end for

cout << "\nPreorder traversal\n";
intTree.preOrderTraversal();

cout << "\nInorder traversal\n";
intTree.inOrderTraversal();

cout << "\nPostorder traversal\n";
intTree.postOrderTraversal();

Tree< double > doubleTree; // create Tree of double values

cout << fixed << setprecision( 1 )
   << "\n\nEnter 10 double values:\n";

// insert 10 doubles to doubleTree
for ( int j = 0; j < 10; ++j )
{
   double doubleValue = 0.0;
   cin >> doubleValue;
   doubleTree.insertNode( doubleValue );
} // end for

cout << "\nPreorder traversal\n";
doubleTree.preOrderTraversal();

cout << "\nInorder traversal\n";
doubleTree.inOrderTraversal();

cout << "\nPostorder traversal\n";
doubleTree.postOrderTraversal();
cout << endl;
} // end main
```

Fig. 19.20 | Creating and traversing a binary tree. (Part 1 of 3.)

```cpp
Enter 10 integer values:
50 25 75 12 33 67 88 6 13 68

Preorder traversal
50 25 12 6 13 33 75 67 68 88
Inorder traversal
6 12 13 25 33 50 67 68 75 88
Postorder traversal
6 13 12 33 25 68 67 88 75 50

Enter 10 double values:
39.2 16.5 82.7 3.3 65.2 90.8 1.1 4.4 89.5 92.5
```

Fig. 19.20 | Creating and traversing a binary tree (Part 2 of 3)
