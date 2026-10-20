
```
13  // construct a SimpleArray of a given size
14  public SimpleArray( int size )
15  {
16      array = new int[ size ];
17  } // end constructor
18
19  // add a value to the shared array
20  public synchronized void add( int value )
21  {
22      int position = writeIndex; // store the write index
23
24      try
25      {
26          // put thread to sleep for 0-499 milliseconds
27          Thread.sleep( generator.nextInt( 500 ) );
28      } // end try
29      catch ( InterruptedException ex )
30      {
31          ex.printStackTrace();
32      } // end catch
33
34      // put value in the appropriate element
35      array[ position ] = value;
36      System.out.printf( "%s wrote %2d to element %d.\n",
37          Thread.currentThread().getName(), value, position );
38
39      ++writeIndex; // increment index of element to be written next
40      System.out.printf( "Next write index: %d\n", writeIndex );
41  } // end method add
42
43  // used for outputting the contents of the shared integer array
44  public String toString()
45  {
46      return "\nContents of SimpleArray:\n" + Arrays.toString( array );
47  } // end method toString
48  } // end class SimpleArray
```

```
pool-1-thread-1 wrote  1 to element 0.
Next write index: 1
pool-1-thread-2 wrote 11 to element 1.
Next write index: 2
pool-1-thread-2 wrote 12 to element 2.
Next write index: 3
pool-1-thread-2 wrote 13 to element 3.
Next write index: 4
pool-1-thread-1 wrote  2 to element 4.
Next write index: 5
pool-1-thread-1 wrote  3 to element 5.
Next write index: 6

Contents of SimpleArray:
1 11 12 13 2 3
```

Fig. 26.8 | 管理由多个线程通过同步共享的整数数组的类。 （第 2 部分，共 2 部分。）

从共享对象中。 生产者/消费者关系将识别待完成工作的任务与实际执行工作的任务分离开来。 打印 spooling 是常见生产者/消费者关系的一个例子。 虽然在你想从应用程序（即生产者）打印时打印机可能不可用，但你仍然可以“完成”打印任务，因为数据会暂时放在磁盘上，直到打印机可用。 同样，当打印机（即消费者）可用时，它不必等待当前用户想要打印。 spool 的打印作业可以在打印机可用时立即打印。 生产者/消费者关系的另一个例子是向 DVD 复制数据的应用程序，它将数据放入固定大小的缓冲区，DVD 驱动器在“刻录”数据到 DVD 时会清空该缓冲区。

在多线程生产者/消费者关系中，生产者线程生成数据并将其放入称为缓冲区的共享对象中。 消费者线程从缓冲区读取数据。 这种关系需要同步，以确保值被正确生产和消费。 所有由多个线程共享的可变数据（例如缓冲区中的数据）的操作都必须使用锁进行保护，以防止损坏，如第 26.4 节所述。 生产者和消费者线程共享的缓冲区数据上的操作也是状态相关的——操作只有在缓冲区处于正确状态时才应继续。 如果缓冲区处于非满状态，生产者可以生产；如果缓冲区处于非空状态，消费者可以消费。 访问缓冲区的任何操作都必须使用同步，以确保只有在缓冲区处于适当状态时才将数据写入缓冲区或从缓冲区读取。 如果尝试将下一个数据放入缓冲区的生产者确定它已满，则生产者线程必须等待直到有空间写入新值。 如果消费者线程发现缓冲区为空或发现先前的数据已被读取，则消费者也必须等待新数据可用。

考虑如果我们不同步对共享数据进行操作的多个线程的访问，会如何产生逻辑错误。 我们的下一个示例（图 26.9–图 26.13）在没有适当同步的情况下实现生产者/消费者关系。 生产者线程将数字 1 到 10 写入共享缓冲区——两个线程之间共享的单个内存位置（在本例中为图 26.12 第 6 行的单个 int 变量 buffer）。 消费者线程从共享缓冲区读取此数据并显示数据。 程序的输出显示生产者写入（生产）到共享缓冲区的值以及消费者从共享缓冲区读取（消费）的值。

生产者线程写入共享缓冲区的每个值必须由消费者线程恰好消费一次。 然而，本例中的线程未同步。 因此，如果生产者在消费者读取先前数据之前将新数据放入共享缓冲区，数据可能会丢失或损坏。 另外，如果消费者在生产者生产下一个值之前再次消费数据，数据也可能被错误地重复。 为了展示这些可能性，以下示例中的消费者线程保留其读取的所有值的总和。 生产者线程生产从 1 到 10 的值。 如果消费者读取每个生产的值一次且仅一次，总和将为 55。 然而，如果你多次执行此程序，你会看到总和并不总是 55（如图 26.13 中的输出所示）。 为了强调这一点，示例中的生产者和消费者线程在执行任务之间各自随机休眠长达三秒。 因此，我们不知道生产者线程何时会尝试写入新值，或消费者线程何时会尝试读取值。

```
private final static Random generator = new Random();
private final Buffer sharedLocation; // reference to shared object

// constructor
public Producer( Buffer shared )
{
    sharedLocation = shared;
} // end Producer constructor

// store values from 1 to 10 in sharedLocation
public void run()
{
    int sum = 0;

    for ( int count = 1; count <= 10; count++ )
    {
        try // sleep 0 to 3 seconds, then place value in Buffer
        {
            Thread.sleep( generator.nextInt( 3000 ) ); // random sleep
            sharedLocation.set( count ); // set value in buffer
            sum += count; // increment sum of values
            System.out.printf( "\t%2d\n", sum );
        } // end try
        // if lines 25 or 26 get interrupted, print stack trace
        catch ( InterruptedException exception )
        {
            exception.printStackTrace();
        } // end catch
    } // end for

    System.out.println(
        "Producer done producing\nTerminating Producer" );
} // end method run
} // end class Producer
```

Fig. 26.10 | 生产者，其 run 方法将值 1 到 10 插入缓冲区。 （第 2 部分，共 2 部分。）

类 Consumer（图 26.11）也实现了 Runnable 接口，允许 Consumer 与 Producer 并发执行。 行 11–14 使用在 main 中创建的对象（图 26.13）初始化 Buffer 引用 sharedLocation，该对象实现了 Buffer 接口并作为参数 shared 传递给构造函数。 正如我们将看到的，这与用于初始化 Producer 对象的 UnsynchronizedBuffer 对象相同——因此，两个线程共享同一个对象。 本程序中的 Consumer 线程执行方法 run（行 17–39）中指定的任务。 行 21–35 迭代 10 次。 每次迭代调用 Thread 方法 sleep（行 26）将 Consumer 线程置于定时等待状态长达 3 秒。 接下来，行 27 使用 Buffer 的 get 方法检索共享缓冲区中的值，然后将该值添加到变量 sum。 行 28 显示迄今为止消费的所有值的总和。 当循环完成后，行 37–38 显示已消费值的总和的行。 然后方法 run 终止，这表明 Consumer 已完成其任务。 一旦两个线程都进入终止状态，程序结束。
