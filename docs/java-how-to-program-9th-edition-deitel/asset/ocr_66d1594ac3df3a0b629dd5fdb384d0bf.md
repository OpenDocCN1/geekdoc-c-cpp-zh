Line 46 sets occupied to false to indicate that buffer is now empty (i.e., a Consumer cannot read the value, but a Producer can place another value in buffer), line 48 calls method displayState to indicate that the consumer is reading and line 50 invokes method notifyAll. If any threads are in the waiting state for the lock on this SynchronizedBuffer object, they enter the runnable state and can now attempt to reacquire the lock. Method notifyAll returns immediately, then method get returns the value of buffer to its caller. When method get returns, the lock on the SynchronizedBuffer object is implicitly released.

# Error-Prevention Tip 26.3

Always invoke method wait in a loop that tests the condition the task is waiting on. It's possible that a thread will reenter the runnable state (via a timed wait or another thread calling notifyAll) before the condition is satisfied. Testing the condition again ensures that the thread will not erroneously execute if it was notified early.

# Testing Class SynchronizedBuffer

Class SharedBufferTest2 (Fig. 26.17) is similar to class SharedBufferTest (Fig. 26.13). SharedBufferTest2 contains method main (lines 8–24), which launches the application. Line 11 creates an ExecutorService to run the Producer and Consumer tasks. Line 14 creates a SynchronizedBuffer object and assigns its reference to Buffer variable sharedLocation. This object stores the data that will be shared between the Producer and Consumer. Lines 16–17 display the column heads for the output. Lines 20–21 execute a Producer and a Consumer. Finally, line 23 calls method shutdown to end the application when the Producer and Consumer complete their tasks. When method main ends (line 24), the main thread of execution terminates.

```
1  // Fig. 26.17: SharedBufferTest2.java
2  // Two threads correctly manipulating a synchronized buffer.
3  import java.util.concurrent.ExecutorService;
4  import java.util.concurrent.Executors;
5  
6  public class SharedBufferTest2
7  {
8      public static void main( String[] args )
9      {
10         // create a newCachedThreadPool
11         ExecutorService application = Executors.newCachedThreadPool();
12         
13         // create SynchronizedBuffer to store ints
14         Buffer sharedLocation = new SynchronizedBuffer();
15         
16         System.out.printf( "%-40s%s\t%s\n%-40s\n\n", "Operation",
17                            "Buffer", "Occupied", "------------", "------------\t------------" );
18         
19         // execute the Producer and Consumer tasks
20         application.execute( new Producer( sharedLocation ) );
21         application.execute( new Consumer( sharedLocation ) );
22
```