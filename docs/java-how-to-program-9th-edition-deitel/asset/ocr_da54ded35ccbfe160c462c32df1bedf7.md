need the program to wait for the threads to complete before main outputs the SimpleArray object’s contents. Interface ExecutorService provides the awaitTermination method for this purpose. This method returns control to its caller either when all tasks executing in the ExecutorService complete or when the specified timeout elapses. If all tasks are completed before awaitTermination times out, this method returns true; otherwise it returns false. The two arguments to awaitTermination represent a timeout value and a unit of measure specified with a constant from class TimeUnit (in this case, TimeUnit.MINUTES).

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