
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

图 26.3 | PrintTask 类随机睡眠 0 到 5 秒。

当线程苏醒时，它会重新进入可运行状态。当 PrintTask 再次被分配给处理器时，第 36 行输出一条消息，指示该任务已完成睡眠，随后 run 方法终止。第 29–33 行的 catch 是必需的，因为如果睡眠线程的 interrupt 方法被调用，sleep 方法可能会抛出类型为 InterruptedException 的受检异常。

## 使用 ExecutorService 管理执行 PrintTask 的线程

图 26.4 使用一个 ExecutorService 对象来管理执行 PrintTask 的线程（如图 26.3 所定义）。第 11–13 行创建并命名三个要执行的 PrintTask。第 18 行使用 Executors 的 newCachedThreadPool 方法获取一个 ExecutorService，它能够在应用程序需要时创建新线程。这些线程由 ExecutorService（threadExecutor）用于执行 Runnable。

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

## 监视器

执行同步的常见方式是使用 Java 内置的监视器（monitor）。每个对象都有一个监视器和一个监视器锁（monitor lock，或称内部锁）。监视器确保其对象的监视器锁在任何时刻最多只能被一个线程持有。因此，监视器和监视器锁可用来强制实现互斥。如果某个操作要求执行线程在操作期间持有锁，那么线程必须先获取锁才能继续操作。其他试图执行需要同一把锁的操作的线程将被阻塞，直到第一个线程释放锁，此时被阻塞的线程才可以尝试获取锁并继续操作。

为了指定线程必须持有监视器锁才能执行一段代码，这段代码应放在 synchronized 语句中。这样的代码称为受监视器锁保护（guarded）；线程必须获取该锁才能执行受保护的语句。监视器同一时刻只允许一个线程执行在同一个对象上锁定的 synchronized 语句，因为同一时刻只能有一个线程持有监视器锁。synchronized 语句使用 synchronized 关键字声明：

```java
synchronized ( object )
{
    statements
} // end synchronized statement
```

其中 object 是要获取其监视器锁的对象；如果 synchronized 语句出现在某个对象中，那么 object 通常就是 this。如果有多个 synchronized 语句同时试图在某个对象上执行，则只有一个语句可以在该对象上处于活动状态——其他所有试图进入同一对象上的 synchronized 语句的线程都将进入阻塞状态。

当 synchronized 语句执行完毕时，该对象的监视器锁会被释放，一个试图进入 synchronized 语句的被阻塞线程可以被允许获取该锁以继续执行。Java 还允许 synchronized 方法。在执行之前，非静态 synchronized 方法必须获取调用该方法的对象上的锁。类似地，静态 synchronized 方法必须获取调用该方法的类上的锁。

### 26.4.1 非同步数据共享

首先，我们说明在缺乏正确同步的情况下跨线程共享对象的危险性。在这个例子中，两个 Runnable 持有一个整数数组的引用。每个 Runnable 向数组写入三个值，然后终止。这看起来似乎无害，但我们将看到，如果在没有同步的情况下操作该数组，可能会导致错误。

### SimpleArray 类

SimpleArray 对象（图 26.5）将在多个线程之间共享。SimpleArray 将使这些线程能够将 int 值放入 array（在第 8 行声明）中。第 9 行初始化变量 writeIndex，它将用于确定下一个要写入的数组元素。构造函数（第 13–16 行）创建一个所需大小的整数数组。

方法 add（第 19–40 行）允许将新值插入到数组末尾。第 21 行存储当前的 writeIndex 值。第 26 行让调用 add 的线程随机睡眠 0 到 499 毫秒。这样做是为了使与未同步访问共享数据相关的问题更加明显。

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

线程睡眠结束后，第 34 行将传递给 `add` 的值插入数组中由 position 指定的元素位置。第 35–36 行输出一条消息，指示执行线程的名称、插入数组中的值以及插入的位置。表达式 `Thread.currentThread().getName()`（第 36 行）首先获取当前执行线程的引用，
