+   12. In the solution to the bank simulation problem, can the event list be a queue? Can the event list be a list or sorted list?

+   13. Consider the stack-based search of the flight map in the HPAir problem of Chapter 6. You can replace the stack that searchS uses with a queue. That is, you can replace every call to push with a call to enqueue, every call to pop with a call to dequeue, and every call to peek with a call to peekFront. Trace the resulting algorithm when you fly from P to Z in the flight map in Figure 6-6. Indicate the contents of the queue after every operation on it.

+   14. As Chapter 6 pointed out, you can define ADT operations in a mathematically formal way by using axioms. Consider the following axioms for the ADT queue, where aqueue is an arbitrary queue and item is an arbitrary queue item:

```
(new Queue()).isEmpty() = true
(new Queue()).dequeue() = false
(new Queue()).peekFront() = error
(new Queue()).enqueue(item).dequeue() = new Queue()
(new Queue()).enqueue(item).peekFront() = item
(aQueue.enqueue(item)).isEmpty() = false
(aQueue.enqueue(item)).dequeue() = true
```

If aQueue is not empty,

```
(aQueue.enqueue(item)).dequeue() = (aQueue.dequeue()).enqueue(item)
```

and

```
(aQueue.enqueue(item)).peekFront() = aQueue.peekFront()
```

+   a. Note the recursive nature of the definition of peekFront. What is the base case? What is the recursive step? What is the significance of the isEmpty test? Why is the queue operation peekFront recursive in nature while the stack operation peek for the ADT stack is not?

+   b. The representation of a stack as a sequence of push operations without any pop operations is called a canonical form. (See Exercise 15 in Chapter 6.) Is there a canonical form for the ADT queue? That is, can you represent a queue as a sequence of enqueue operations without any dequeue operations? Prove your answer.

# PROGRAMMING PROBLEMS

+   1. Using the class queue in the Standard Template Library, define and test the class OurQueue that is derived from QueueInterface, as given in Listing 13-1. The class queue has the following methods that you can use to define the methods for OurQueue:

```
queue(); // Default constructor
bool empty() const; // Tests whether the queue is empty
void push(const ItemType& newEntry); // Adds newEntry to the back of the queue
void pop(); // Removes the front of the queue
ItemType& front(); // Returns a reference to the front of the queue
```

To access queue, use the following include statement:

```
#include <queue>;
```