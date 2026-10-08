Class QueueTest's main method (Fig. 19.17) creates a QueueInheritance object called queue. Lines 15–18 define four values that are enqueued and dequeued. The program enqueues (lines 21, 23, 25 and 27) a bool containing true, a char containing '$', an int containing 34567 and a string containing "hello". QueueTest uses LinkedListLibrary and namespace QueueInheritanceLibrary; the solution for QueueTest must have references to other class libraries.

```
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

        // use method Dequeue to remove items from queue
        object removedObject = null;
        // remove items from queue
        try {
            while (true) {
                removedObject = queue.Dequeue();
                Console.WriteLine($"{removedObject} dequeued");
                queue.Display();
            }
        } catch (EmptyListException emptyListException) {
}
```

Fig. 19.17 | Testing class QueueInheritance. (Part I of 2.)