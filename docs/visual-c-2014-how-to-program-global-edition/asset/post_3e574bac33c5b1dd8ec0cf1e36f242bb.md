
# 19.5 Stacks

hello popped
The stack is: 34567 $ True

34567 popped
The stack is: $ True

$ popped
The stack is: $ True

True popped
Empty stack
at LinkedList.List.RemoveFrom() in C:\Users\PaulDeitel\nDocuments\examples\ch19\Fig19_04\LinkedList\nLinkedList\LinkedList.cs: line 81
at StackInheritanceLibrary.StackInheritance.Pop() in C:\Users\PaulDeitel\nDocuments\examples\ch19\Fig19_13\StackInheritance\nStackInheritanceLibrary.StackInheritance.cs: line 24
at StackInheritanceTest.Stack() in C:\Users\PaulDeitel\nDocuments\examples\ch19\Fig19_14\StackInheritance\nStackInheritanceTest.StackInheritanceTest.cs: line 35

Fig. 19.14 | Testing class That Contains a Reference to a List (Part 2 of 2)

### Stack Class That Contains a Reference to a List
Another way to implement a stack is by reusing a list through composition. ClassComposition (Fig. 15) uses a private object of class list (line 10). Composition enables us to hide the methods of class list that should not be in our public interface by providing public interface methods only to the required list methods. Each class implements stack method by delegating its work to an appropriate list method. StackComposition's methods call list methods AtFront, RemoveFrom, IsEmpty and Display. In this example, we do not show StackComposition, because the only differences in this example are that we change the name of the stack class from StackInheritance to StackComposition and update a using directive.

```cs
// Fig.19.15: StackComposition.class.cs
// StackComposition encapsulates functionality of class list.
using LinkedListList;

namespace StackCompositionLibrary
{
    // StackComposition encapsulates List's capabilities
    public class StackComposition
    {
        private List stack;

        public StackComposition()
        {
            stack = new List("stack");
```

Fig. 19.15 | StackComposition class encapsulates functionality of class list. (Part I of 2)

```cs
 // add object to stack
public void Push(object dataValue)
{
    stack.insertAtFront(dataValue);
}
```

```cs
 // remove object from stack
public object Pop()
{
    return stack.RemoveFromFront();
}
```

```cs
 // determine whether stack is empty
public bool IsEmpty()
{
    return stack.IsEmpty();
}
```

```cs
 // output stack contents
public void Display()
{
    stack.Display();
}
```

Fig. 19.15 | StackComposition class encapsulates functionality of class List. (Part 2 of 2.)

# 19.6 Queues

Another commonly used data structure is the queue. A queue is similar to a checkout line in a supermarket—the cashier services the person at the beginning of the first line. Other customers enter the line at the end and wait for service. Queue nodes are removed from the head (or front) of the queue and are inserted at the tail (or end). For this reason, a queue is a first-in, first-out (FIFO) data structure. The insert and remove operations are called enqueue and dequeue.

Queues have many uses in computer systems. Computers with a single processor can serve only one app at a time. Each requiring processor time is placed in a queue. The app at the front of the queue is the next to receive service. Each app gradually advances to the front before it receives service.

Queues are also used to print spooling. Each program, a single printer might be shared by all of users. Many users can send jobs to the printer, even when the printer is already busy. These print jobs are placed in a queue until the printer becomes available. A program called a spooler manages the queue to ensure that as each job completes, the next is sent to the printer.

Information packets also in queues in computer networks. Each packet arrives at a network node, it must be routed to the next node along the path to the packet's final destination. The routing node routes one packet at a time, so additional packets are enqueued until the router can route them.

A file server in a computer network handles file-access requests from many clients throughout the network. Servers have a limited capacity to service requests from clients. When that capacity is exceeded, client requests wait in queues.

### Queue That Inherits from List

The code in Fig 19.16 creates a queue class by inheriting from a list class. We want the QueueInheritance class (Fig. 19.6) to have methods Enqueue, Dequeue, IsEmpty and Display. Essentially, these are the methods InsertBack, RemoveFront, IsEmpty and Display of class List. Of course, the list contains other methods (as InsertFront and RemoveBack) we would rather make accessible through the public interface to the queue class. Remember that all methods in the public interface of the List are also public methods of the class QueueInheritance.

The implementation of each QueueInheritance method calls the appropriate List method—enqueue and dequeue calls RemoveFront. Calls also invoke the base-class versions that were inherited from List into QueueInheritance's public interface. Class QueueInheritance uses namespace LinkedList(Fig. 19.4); the class library for QueueInheritance must have a reference to the LinkedList class library. Just as we demonstrated with stacks, we could use composition to implement a queue that does not expose the unwanted methods of class List.

```cs
// Fig. 19.16: QueueInheritancelibrary.cs
// Implementing a queue by inheriting from class List.
using LinkedListList;

namespace QueueInheritance
{
    // QueueInheritance inherits List's capabilities
    public class QueueInheritance : List
    {
        // pass name "queue" to List constructor
        public QueueInheritance() : base("queue") { }

        // place dataValue at end of queue by inserting
        // dataValue at end of linked list
        public void Enqueue(object dataValue)
        {
            InsertBack(dataValue);
        }

        // remove item from front of queue by removing
        // item at front of linked list
        public object Dequeue()
        {
            return RemoveFront();
        }
    }
}
```

Fig. 19.16 | Implementing a queue by inheriting from class List.

Class QueueTest's main method (Fig. 19.17) creates a QueueInheritance object called queue. Lines 15–18 define four values that are enqueued and dequeued. The program enqueues (lines 21, 23, 25 and 27) a bool containing true, a char containing '$', an int containing 34567 and a string containing "hello". QueueTest uses LinkedListLibrary and namespace QueueInheritanceLibrary; the solution for QueueTest must have references to other class libraries.

```cs
// Fig. 19.17: QueueTest.cs
// Testing QueueInheritance.
using System;
using QueueInheritanceLibrary;
using LinkedListLibrary;
// demonstrate functionality of class QueueInheritance
class QueueTest
{
    static void Main()
    {
        QueueInheritance queue = new QueueInheritance();

        // create objects to store in the queue
        bool aBoolean = true;
        char aCharacter = '$';
        int aInteger = 34567;
        string aString = "hello";

        // use method to add items to queue
        queue.Enqueue(aBoolean);
        queue.Display();
        queue.Enqueue(aCharacter);
        queue.Display();
        queue.Enqueue(aInteger);
        queue.Display();
        queue.Enqueue(aString);
        queue.Display();

        // use method to remove items from queue
        object removedObject = null;
        // remove items from queue
        try {
            while (true) {
                removedObject = queue.Dequeue();
                Console.WriteLine($"{removedObject} dequeued");
                queue.Display();
            }
        } catch (EmptyListException emptyException) {
            // if exception occurs, write stack trace
            Console.Error.WriteLine(emptyException.StackTrace);
        }
    }
}
```

Fig. 19.17 | Testing class QueueInheritance. (Part I of 2.)

```cs
// if exception occurs, write stack trace
Console.Error.WriteLine(emptyException.StackTrace);
}
```

The queue is: True
The queue is: True $
The queue is: True $34567
The queue is: True $34567 hello
True dequeued
The queue is: $ 34567 hello
$ dequeued
The queue is: 34567 hello
34567 dequeued
The queue is: hello
hello dequeued
Empty queue
at LinkedList.List.RemoveFromFront() in C:\Users\PaulDeitel\nDocuments\examples\ch19\Fig19_04\LinkedList\nLinkedList\LinkedList.cs: line 81
at QueueInheritance.QueueInheritance.Dequeue() in C:\Users\PaulDeitel\nDocuments\examples\ch19\Fig19_16\QueueInheritance\nQueueInheritance.QueueInheritance.cs: line 24
at QueueTest.Main(String[] args) in C:\Users\PaulDeitel\nDocuments\examples\ch19\Fig19_17\QueueTest.QueueTest.cs: line 38

Fig. 19.17 | Testing class QueueInheritance. (Part 2 of 2.)

An infinite loop (lines 36-41) dequeues the elements from the queue in FIFO order. When there are no objects to dequeue, dequeue throws an Empty-ListException, and the program displays the exception's stack trace, which shows the program-execution stack at the time the exception occurred. The program uses method Display to output the contents of the queue after each operation.

# 19.7 Trees

Linked lists and stacks are linear data structures (i.e., sequences). A tree is a non-linear, two-dimensional data structure with special properties. Tree nodes can contain two or more links.

### Basic Terminology

With binary trees (Fig. 19.18), each tree connects two links (none, one or both which may be null). The root node is the first node in a tree. Each root node refers to a child. The left child is the first node in the left subtree, and the right child is the first node in the right subtree. The children of a special node are called siblings, A
