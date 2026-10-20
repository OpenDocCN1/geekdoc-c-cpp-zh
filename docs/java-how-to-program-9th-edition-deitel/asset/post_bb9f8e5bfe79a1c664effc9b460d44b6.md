
then uses that Thread’s getName method to obtain its name. Line 38 increments writeIndex so that the next call to add will insert a value in the array’s next element. Lines 43–46 override method toString to create a String representation of the array’s contents.

## Class *ArrayWriter*

Class ArrayWriter (Fig. 26.6) implements the interface Runnable to define a task for inserting values in a SimpleArray object. The constructor (lines 10–14) takes two arguments—an integer value, which is the first value this task will insert in the SimpleArray object, and a reference to the SimpleArray object. Line 20 invokes method add on the SimpleArray object. The task completes after three consecutive integers beginning with startValue are added to the SimpleArray object.

```
// Fig. 26.6: ArrayWriter.java
// Adds integers to an array shared with other Runnables
import java.lang.Runnable;

public class ArrayWriter implements Runnable
{
    private final SimpleArray sharedSimpleArray;
    private final int startValue;

    public ArrayWriter( int value, SimpleArray array )
    {
        startValue = value;
        sharedSimpleArray = array;
    } // end constructor

    public void run()
    {
        for ( int i = startValue; i < startValue + 3; i++ )
        {
            sharedSimpleArray.add( i ); // add an element to the shared array
        } // end for
    } // end method run
} // end class ArrayWriter
```

**Fig. 26.6** | Adds integers to an array shared with other Runnables.

## Class *SharedArrayTest*

Class SharedArrayTest (Fig. 26.7) executes two ArrayWriter tasks that add values to a single SimpleArray object. Line 12 constructs a six-element SimpleArray object. Lines 15–16 create two new ArrayWriter tasks, one that places the values 1–3 in the SimpleArray object, and one that places the values 11–13. Lines 19–21 create an ExecutorService and execute the two ArrayWriters. Line 23 invokes the ExecutorService’s shutdown method to *prevent additional tasks from starting* and to enable the application to terminate when the currently executing tasks complete execution.

Recall that ExecutorService method shutdown returns immediately. Thus any code that appears *after* the call to ExecutorService method shutdown in line 23 *will continue executing as long as the main thread is still assigned to a processor*. We’d like to output the SimpleArray object to show you the results after the threads complete their tasks. So, we need the program to wait for the threads to complete before main outputs the SimpleArray object’s contents. Interface ExecutorService provides the awaitTermination method for this purpose. This method returns control to its caller either when all tasks executing in the ExecutorService complete or when the specified timeout elapses. If all tasks are completed before awaitTermination times out, this method returns true; otherwise it returns false. The two arguments to awaitTermination represent a timeout value and a unit of measure specified with a constant from class TimeUnit (in this case, TimeUnit.MINUTES).

```
// Fig 26.7: SharedArrayTest.java
// Executes two Runnables to add elements to a shared SimpleArray.
import java.util.concurrent.Executors;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.TimeUnit;

public class SharedArrayTest
{
    public static void main( String[] arg )
    {
        // construct the shared object
        SimpleArray sharedSimpleArray = new SimpleArray( 6 );

        // create two tasks to write to the shared SimpleArray
        ArrayWriter writer1 = new ArrayWriter( 1, sharedSimpleArray );
        ArrayWriter writer2 = new ArrayWriter( 11, sharedSimpleArray );

        // execute the tasks with an ExecutorService
        ExecutorService executor = Executors.newCachedThreadPool();
        executor.execute( writer1 );
        executor.execute( writer2 );

        executor.shutdown();

        try
        {
            // wait 1 minute for both writers to finish executing
            boolean tasksEnded = executor.awaitTermination(
                1, TimeUnit.MINUTES );

            if ( tasksEnded )
                System.out.println( sharedSimpleArray ); // print contents
            else
                System.out.println(
                    "Timed out while waiting for tasks to finish.");
        } // end try
        catch ( InterruptedException ex )
        {
            System.out.println(
                "Interrupted while waiting for tasks to finish.");
        } // end catch
    } // end main
} // end class SharedArrayTest
```

```
pool-1-thread-1 wrote 1 to element 0.
Next write index: 1
pool-1-thread-2 wrote 2 to element 1.
Next write index: 2
pool-1-thread-1 wrote 3 to element 2.
Next write index: 3
pool-1-thread-2 wrote 11 to element 0.
Next write index: 4
pool-1-thread-1 wrote 12 to element 4.
Next write index: 5
pool-1-thread-2 wrote 13 to element 5.
Next write index: 6
Contents of SimpleArray:
[11, 2, 0, 12, 13]
```

Fig. 26.7 | Executes two Runnables to insert values in a shared array. (Part 2 of 2.)

In this example, if both tasks complete before awaitTermination times out, line 32 displays the SimpleArray object's contents. Otherwise, lines 34–35 print a message indicating that the tasks did not finish executing before awaitTermination timed out.

The output in Fig. 26.7 demonstrates the problems (highlighted in the output) that can be caused by failure to synchronize access to shared data. The value 1 was written to element 0, then overwritten later by the value 11. Also, when writeIndex was incremented to 3, nothing was written to that element, as indicated by the 0 in that element of the printed array.

Recall that we added calls to Thread method sleep between operations on the shared data to emphasize the unpredictability of thread scheduling and increase the likelihood of producing erroneous output. Even if these operations were allowed to proceed at their normal pace, you could still see errors in the program’s output. However, modern processors can handle the simple operations of the SimpleArray method add so quickly that you might not see the errors caused by the two threads executing this method concurrently, even if you tested the program dozens of times. One of the challenges of multithreaded programming is spotting the errors—they may occur so infrequently that a broken program does not produce incorrect results during testing, creating the illusion that the program is correct.

## 26.4.2 Synchronized Data Sharing—Making Operations Atomic

The output errors of Fig. 26.7 can be attributed to the fact that the shared object, SimpleArray, is not thread safe—SimpleArray is susceptible to errors if it’s accessed concurrently by multiple threads. The problem lies in method add, which stores the value of writeIndex, places a new value in that element, then increments writeIndex. Such a method would present no problem in a single-threaded program. However, if one thread obtains the value of writeIndex, there’s no guarantee that another thread cannot come along and increment writeIndex before the first thread has a chance to place a value in the array. If this happens, the first thread will be writing to the array based on a stale value of writeIndex—a value that’s no longer valid. Another possibility is that one thread might obtain the value of writeIndex after another thread adds an element to the array but before writeIndex is incremented. In this case, the first thread would write to the array based on an invalid value for writeIndex.

SimpleArray is not thread safe because it allows any number of threads to read and modify shared data concurrently, which can cause errors. To make SimpleArray thread safe, we must ensure that no two threads can access it at the same time. We also must ensure that while one thread is in the process of storing writeIndex, adding a value to the array, and incrementing writeIndex, no other thread may read or change the value of writeIndex or modify the contents of the array at any point during these three operations. In other words, we want these three operations—storing writeIndex, writing to the array, incrementing writeIndex—to be an atomic operation, which cannot be divided into smaller suboperations. We can simulate atomicity by ensuring that only one thread carries out the three operations at a time. Any other threads that need to perform the operation must wait until the first thread has finished the add operation in its entirety.

Atomicity can be achieved using the synchronized keyword. By placing our three suboperations in a synchronized statement or synchronized method, we allow only one thread at a time to acquire the lock and perform the operations. When that thread has completed all of the operations in the synchronized block and releases the lock, another thread may acquire the lock and begin executing the operations. This ensures that a thread executing the operations will see the actual values of the shared data and that these values will not change unexpectedly in the middle of the operations as a result of another thread’s modifying them.

## Software Engineering Observation 26.2

Place all accesses to mutable data that may be shared by multiple threads inside synchronized statements or synchronized methods that synchronize on the same lock. When performing multiple operations on shared data, hold the lock for the entirety of the operation to ensure that the operation is effectively atomic.

## Class SimpleArray with Synchronization

Figure 26.8 displays class SimpleArray with the proper synchronization. Notice that it’s identical to the SimpleArray class of Fig. 26.5, except that add is now a synchronized method (line 20). So, only one thread at a time can execute this method. We reuse classes ArrayWriter (Fig. 26.6) and SharedArrayTest (Fig. 26.7) from the previous example.

```
// Fig. 26.8: SimpleArray.java
// Class that manages an integer array to be shared by multiple
// threads with synchronization.
import java.util.Arrays;
import java.util.Random;

public class SimpleArray
{
    private final int[] array; // the shared integer array
    private int writeIndex = 0; // index of next element to be written
    private final static Random generator = new Random();

Fig. 26.8 | Class that manages an integer array to be shared by multiple threads with synchronization. (Part 1 of 2.)
