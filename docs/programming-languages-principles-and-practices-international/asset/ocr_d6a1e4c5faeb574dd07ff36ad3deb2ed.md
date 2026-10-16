```
#ifndef QUEUE_H
#define QUEUE_H

namespace MyQueue
{ struct Queuere p;
  typedef Queuere p * Queue;
  // struct no longer needed in C++
  Queue createq();
  Queue enqueue(Queue q, void* elem);
  void* frontq(Queue q);
  Queue dequeue(Queue q);
  bool emptyq(Queue q);
}

#endif
```

Figure 11.8 The queue.h header file in C++ using a namespace

Inside the queue.cpp file, the definitions of the queue functions must now use the scope resolution operator, for example:

```
struct MyQueue::Queuere p
{ void* data;
  Queue next;
};
```

Alternatively, one could reenter the MyQueue namespace by surrounding the implementation code in queue.cpp with the same namespace declaration as in the header. (Namespaces can be reentered whenever one wishes to add definitions or implementations to a namespace.)

A client of MyQueue has three options:

+   1. After the appropriate #include, the user can simply refer to the MyQueue definitions using the qualified name (i.e., with MyQueue:: before each name used from the MyQueue namespace).
+   2. Alternatively, the user can write a using declaration for each name used from the namespace and then use each such name without qualification.
+   3. Finally, the user can “unqualify” all the names in the namespace with a single using namespace declaration.

Consider Figure 11.9, which lists C++ client code for the above C++ queue code. This code exhibits all three of the above options to reference names in a namespace. A using declaration (option 2) is given on line 3, allowing the standard library function endl from iostream to be used without qualification. A using namespace declaration (option 3) is given on line 4, allowing all names in MyQueue to be