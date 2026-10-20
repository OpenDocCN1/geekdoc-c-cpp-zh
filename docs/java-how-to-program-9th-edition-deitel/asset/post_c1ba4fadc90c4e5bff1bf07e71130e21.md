
```java
// Fig. 26.3: PrintTask.java
// PrintTask class sleeps for a random time from 0 to 5 seconds
import java.util.Random;

public class PrintTask implements Runnable
{
    private final int sleepTime; // random sleep time for thread
    private final String taskName; // name of task
    private final static Random generator = new Random();

    // constructor
    public PrintTask( String name )
    {
        taskName = name; // set task name

        // pick random sleep time between 0 and 5 seconds
        sleepTime = generator.nextInt( 5000 ); // milliseconds
    } // end PrintTask constructor

    // method run contains the code that a thread will execute
    public void run()
    {
        try // put thread to sleep for sleepTime amount of time
        {
            System.out.printf( "%s going to sleep for %d milliseconds.\n",
                taskName, sleepTime );
            Thread.sleep( sleepTime ); // put thread to sleep
        } // end try
        catch ( InterruptedException exception )
        {
            System.out.printf( "%s %s\n", taskName,
                "terminated prematurely due to interruption" );
        } // end catch

        // print task name
        System.out.printf( "%s done sleeping\n", taskName );
    } // end method run
} // end class PrintTask
```

Fig. 26.3 | PrintTask class sleeps for a random time from 0 to 5 seconds.

When the thread awakens, it reenters the runnable state. When the PrintTask is assigned to a processor again, line 36 outputs a message indicating that the task is done sleeping, then method run terminates. The catch at lines 29–33 is required because method sleep might throw a checked exception of type InterruptedException if a sleeping thread’s interrupt method is called.

## Using the ExecutorService to Manage Threads that Execute PrintTasks

Figure 26.4 uses an ExecutorService object to manage threads that execute PrintTasks (as defined in Fig. 26.3). Lines 11–13 create and name three PrintTasks to execute. Line 18 uses Executors method newCachedThreadPool to obtain an ExecutorService that’s capable of creating new threads as they’re needed by the application. These threads are used by ExecutorService (threadExecutor) to execute the Runnables.

```java
// Fig. 26.4: TaskExecutor.java
// Using an ExecutorService to execute Runnables.
import java.util.concurrent.Executors;
import java.util.concurrent.ExecutorService;

public class TaskExecutor
{
    public static void main( String[] args )
    {
        // create and name each runnable
        PrintTask task1 = new PrintTask( "task1" );
        PrintTask task2 = new PrintTask( "task2" );
        PrintTask task3 = new PrintTask( "task3" );

        System.out.println( "Starting Executor" );

        // create ExecutorService to manage threads
        ExecutorService threadExecutor = Executors.newCachedThreadPool();

        // start threads and place in runnable state
        threadExecutor.execute( task1 ); // start task1
        threadExecutor.execute( task2 ); // start task2
        threadExecutor.execute( task3 ); // start task3

        // shut down worker threads when their tasks complete
        threadExecutor.shutdown();

        System.out.println( "Tasks started, main ends.\n" );
    } // end main
} // end class TaskExecutor
```

```text
Starting Executor
Tasks started, main ends.

task1 going to sleep for 4806 milliseconds.
task2 going to sleep for 2513 milliseconds.
task3 going to sleep for 1132 milliseconds.
task3 done sleeping
task2 done sleeping
task1 done sleeping
```

```text
Starting Executor
task1 going to sleep for 3161 milliseconds.
task3 going to sleep for 532 milliseconds.
task2 going to sleep for 3440 milliseconds.
Tasks started, main ends.

task3 done sleeping
task1 done sleeping
task2 done sleeping
```

## Monitors

A common way to perform synchronization is to use Java’s built-in monitors. Every object has a monitor and a monitor lock (or intrinsic lock). The monitor ensures that its object’s monitor lock is held by a maximum of only one thread at any time. Monitors and monitor locks can thus be used to enforce mutual exclusion. If an operation requires the executing thread to hold a lock while the operation is performed, a thread must acquire the lock before proceeding with the operation. Other threads attempting to perform an operation that requires the same lock will be blocked until the first thread releases the lock, at which point the blocked threads may attempt to acquire the lock and proceed with the operation.

To specify that a thread must hold a monitor lock to execute a block of code, the code should be placed in a synchronized statement. Such code is said to be guarded by the monitor lock; a thread must acquire the lock to execute the guarded statements. The monitor allows only one thread at a time to execute statements within synchronized statements that lock on the same object, as only one thread at a time can hold the monitor lock. The synchronized statements are declared using the synchronized keyword:

```java
synchronized ( object )
{
    statements
} // end synchronized statement
```

where object is the object whose monitor lock will be acquired; object is normally this if it’s the object in which the synchronized statement appears. If several synchronized statements are trying to execute on an object at the same time, only one of them may be active on the object—all the other threads attempting to enter a synchronized statement on the same object are placed in the blocked state.

When a synchronized statement finishes executing, the object’s monitor lock is released and one of the blocked threads attempting to enter a synchronized statement can be allowed to acquire the lock to proceed. Java also allows synchronized methods. Before executing, a non-static synchronized method must acquire the lock on the object that’s used to call the method. Similarly, a static synchronized method must acquire the lock on the class that’s used to call the method.

### 26.4.1 Unsynchronized Data Sharing

First, we illustrate the dangers of sharing an object across threads without proper synchronization. In this example, two Runnables maintain references to a single integer array. Each Runnable writes three values to the array, then terminates. This may seem harmless, but we’ll see that it can result in errors if the array is manipulated without synchronization.

### Class SimpleArray

A SimpleArray object (Fig. 26.5) will be shared across multiple threads. SimpleArray will enable those threads to place int values into array (declared at line 8). Line 9 initializes variable writeIndex, which will be used to determine the array element that should be written to next. The constructor (lines 13–16) creates an integer array of the desired size.

Method add (lines 19–40) allows new values to be inserted at the end of the array. Line 21 stores the current writeIndex value. Line 26 puts the thread that invokes add to sleep for a random interval from 0 to 499 milliseconds. This is done to make the problems associated with unsynchronized access to shared data more obvious.

```java
// Fig. 26.5: SimpleArray.java
// Class that manages an integer array to be shared by multiple threads.
import java.util.Arrays;
import java.util.Random;

public class SimpleArray // CAUTION: NOT THREAD SAFE!
{
   private final int[] array; // the shared integer array
   private int writeIndex = 0; // index of next element to be written
   private final static Random generator = new Random();

   // construct a SimpleArray of a given size
   public SimpleArray( int size )
   {
      array = new int[ size ];
   } // end constructor

   // add a value to the shared array
   public void add( int value )
   {
      int position = writeIndex; // store the write index

      try
      {
         // put thread to sleep for 0-499 milliseconds
         Thread.sleep( generator.nextInt( 500 ) );
      } // end try
      catch ( InterruptedException ex )
      {
         ex.printStackTrace();
      } // end catch

      // put value in the appropriate element
      array[ position ] = value;
      System.out.printf( "%s wrote %2d to element %d.\n",
         Thread.currentThread().getName(), value, position );

      ++writeIndex; // increment index of element to be written next
      System.out.printf( "Next write index: %d\n", writeIndex );
   } // end method add

   // used for outputting the contents of the shared integer array
   public String toString()
   {
      return "\nContents of SimpleArray:\n" + Arrays.toString( array );
   } // end method toString
} // end class SimpleArray
```

After the thread is done sleeping, line 34 inserts the value passed to `add` into the array at the element specified by position. Lines 35–36 output a message indicating the executing thread’s name, the value that was inserted in the array and where it was inserted. The expression `Thread.currentThread().getName()` (line 36) first obtains a reference to the currently executing Thread,
