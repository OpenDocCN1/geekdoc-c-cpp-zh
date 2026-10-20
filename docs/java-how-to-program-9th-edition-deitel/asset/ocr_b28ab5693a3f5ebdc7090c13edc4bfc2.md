boxing to insert Integer objects into the queue. Lines 27–32 use an infinite loop to dequeue the objects in first-in, first-out order. When the queue is empty, method dequeue throws an EmptyListException, and the program displays the exception’s stack trace.

```
// Fig. 22.14: QueueTest.java
// Class QueueTest.
import com.deitel.ch22.Queue;
import com.deitel.ch22.EmptyListException;

public class QueueTest
{
    public static void main( String[] args )
    {
        Queue< Integer > queue = new Queue< Integer >();

        // use enqueue method
        queue.enqueue( -1 );
        queue.print();
        queue.enqueue( 0 );
        queue.print();
        queue.enqueue( 1 );
        queue.print();
        queue.enqueue( 5 );
        queue.print();

        // remove objects from queue
        try
        {
            int removedItem;

            while ( true )
            {
                removedItem = queue.dequeue(); // use dequeue method
                System.out.printf( "%n%d dequeued%n", removedItem );
                queue.print();
            } // end while
        } // end try
        catch ( EmptyListException emptyListException )
        {
            emptyListException.printStackTrace();
        } // end catch
    } // end main
} // end class QueueTest
```

The queue is: -1
The queue is: -1 0
The queue is: -1 0 1
The queue is: -1 0 1 5

-1 dequeued
The queue is: 0 1 5

Fig. 22.14 | Queue processing program. (Part I of 2.)