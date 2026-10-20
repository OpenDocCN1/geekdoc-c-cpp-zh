

```
23        application.shutdown();
24    } // end main
25 } // end class SharedBufferTest2
```

| 操作 | 缓冲区 | 已占用 |
| --------- | ------ | -------- |
| 消费者尝试读取。缓冲区为空。消费者等待。 | -1 | false |
| 生产者写入 1 | 1 | true |
| 消费者读取 1 | 1 | false |
| 消费者尝试读取。缓冲区为空。消费者等待。 | 1 | false |
| 生产者写入 2 | 2 | true |
| 消费者读取 2 | 2 | false |
| 生产者写入 3 | 3 | true |
| 消费者读取 3 | 3 | false |
| 生产者写入 4 | 4 | true |
| 生产者尝试写入。缓冲区已满。生产者等待。 | 4 | true |
| 消费者读取 4 | 4 | false |
| 生产者写入 5 | 5 | true |
| 消费者读取 5 | 5 | false |
| 生产者写入 6 | 6 | true |
| 生产者尝试写入。缓冲区已满。生产者等待。 | 6 | true |
| 消费者读取 6 | 6 | false |
| 生产者写入 7 | 7 | true |
| 生产者尝试写入。缓冲区已满。生产者等待。 | 7 | true |
| 消费者读取 7 | 7 | false |
| 生产者写入 8 | 8 | true |
| 消费者读取 8 | 8 | false |
| 消费者尝试读取。缓冲区为空。消费者等待。 | 8 | false |

```
Producer writes 9
9	true
Consumer reads 9
9	false
Consumer tries to read.
Buffer empty. Consumer waits.
9	false
Producer writes 10
10	true
Consumer reads 10
10	false
Producer done producing
Terminating Producer
Consumer read values totaling 55
Terminating Consumer
```

图 26.17 | 两个线程正确操作同步缓冲区的示例。（第 3 部分，共 3 部分。）

研究图 26.17 中的输出。观察到每个被生产出的整数都被恰好消费一次——没有值丢失，也没有值被消费超过一次。同步确保生产者在缓冲区为空时才生产一个值，而消费者仅在缓冲区已满时才消费。生产者总是先进行，消费者如果生产者自上次消费后尚未生产则等待，而生产者如果消费者尚未消费生产者最近生产的值则等待。多次执行此程序以确认每个被生产出的整数都被恰好消费一次。在示例输出中，注意高亮的行，指示生产者和消费者必须等待以执行各自任务的时刻。

## 26.8 生产者/消费者关系：有界缓冲区

第 26.7 节中的程序使用线程同步来保证两个线程正确地操作共享缓冲区。然而，应用程序可能无法达到最佳性能。如果两个线程以不同的速度运行，其中一个线程将花费更多（或大部分）时间等待。例如，在第 26.7 节的程序中，我们在两个线程之间共享一个整数变量。如果生产者线程的生产速度快于消费者能够消费的速度，那么生产者线程会等待消费者，因为缓冲区中没有其他位置可以放置下一个值。类似地，如果消费者消费值的速度快于生产者生产值的速度，消费者会等待直到生产者将下一个值放入共享缓冲区。即使我们有以相同相对速度运行的线程，在一段时间内它们也可能偶尔“不同步”，导致其中一个线程等待另一个线程。我们不能对并发线程的相对速度做出假设——与操作系统、网络、用户和其他组件的交互可能导致线程以不同且不断变化的速度运行。当这种情况发生时，线程会等待。当线程过度等待时，程序的效率会降低，交互式程序的响应性会下降，应用程序的延迟会更长。

生产者和消费者来自第 26.5 节的示例，只是从类 Producer 和类 Consumer 中移除了第 28 行。我们在类 CircularBuffer（图 26.18）中实现有界缓冲区，作为使用共享三元素数组的循环缓冲区。循环缓冲区按顺序写入和读取数组元素，从第一个单元开始向最后一个移动。当生产者或消费者到达最后一个元素时，它返回到第一个，并从那里开始分别写入或读取。在这种生产者/消费者关系版本中，消费者仅在数组不为空时才消费一个值，而生产者仅在数组未满时才生产一个值。类 SharedBufferTest2（图 26.17）主方法中创建和启动线程对象的语句现在出现在类 CircularBufferTest（图 26.19）中。

```
// Fig. 26.18: CircularBuffer.java
// Synchronizing access to a shared three-element bounded buffer.
public class CircularBuffer implements Buffer
{
    private final int[] buffer = { -1, -1, -1 }; // shared buffer

    private int occupiedCells = 0; // count number of buffers used
    private int writeIndex = 0; // index of next element to write to
    private int readIndex = 0; // index of next element to read

    // place value into buffer
    public synchronized void set( int value ) throws InterruptedException
    {
        // wait until buffer has space available, then write value;
        // while no empty locations, place thread in blocked state
        while ( occupiedCells == buffer.length )
        {
            System.out.printf( "Buffer is full. Producer waits.\n" );
            wait(); // wait until a buffer cell is free
        } // end while

        buffer[ writeIndex ] = value; // set new buffer value

        // update circular write index
        writeIndex = ( writeIndex + 1 ) % buffer.length;

        ++occupiedCells; // one more buffer cell is full
        displayState( "Producer writes " + value );
        notifyAll(); // notify threads waiting to read from buffer
    } // end method set

    // return value from buffer
    public synchronized int get() throws InterruptedException
    {
        // wait until buffer has data, then read value;
        // while no data to read, place thread in waiting state
        while ( occupiedCells == 0 )
        {
            System.out.printf( "Buffer is empty. Consumer waits.\n" );
```
```
40      wait(); // wait until a buffer cell is filled
41    } // end while
42
43      int readValue = buffer[ readIndex ]; // read value from buffer
44
45      // update circular read index
46      readIndex = ( readIndex + 1 ) % buffer.length;
47
48      --occupiedCells; // one fewer buffer cells are occupied
49      displayState( "Consumer reads " + readValue );
50      notifyAll(); // notify threads waiting to write to buffer
51
52      return readValue;
53    } // end method get
54
55    // display current operation and buffer state
56    public void displayState( String operation )
57    {
58      // output operation and number of occupied buffer cells
59      System.out.printf( "%s%s%d)\n%s", operation,
60        " (buffer cells occupied: ", occupiedCells, "buffer cells: " );
61
62      for ( int value : buffer )
63        System.out.printf( " %2d  ", value ); // output values in buffer
64
65      System.out.print( "\n          " );
66
67      for ( int i = 0; i < buffer.length; i++ )
68        System.out.print( "---- " );
69
70      System.out.print( "\n          " );
71
72      for ( int i = 0; i < buffer.length; i++ )
73      {
74        if ( i == writeIndex && i == readIndex )
75          System.out.print( "  WR " ); // both write and read index
76        else if ( i == writeIndex )
77          System.out.print( "  W   " ); // just write index
78        else if ( i == readIndex )
79          System.out.print( "   R  " ); // just read index
80        else
81          System.out.print( "      " ); // neither index
82      } // end for
83
84      System.out.println( "\n" );
85    } // end method displayState
86  } // end class CircularBuffer
```

图 26.18 | 同步访问共享三元素有界缓冲区。（第 2 部分，共 2 部分。）

第 5 行将数组 buffer 初始化为代表循环缓冲区的三元素 int 数组。变量 occupiedCells（第 7 行）计算 buffer 中包含待读取数据的元素数量。当 occupiedBuffers 为 0 时，循环缓冲区中没有数据，消费者必须等待——当 occupiedCells 为 3（循环缓冲区的大小）时，

