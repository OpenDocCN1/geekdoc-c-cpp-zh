Producer and Consumer from the example in Section 26.5, except that line 28 is removed from class Producer and class Consumer. We implement the bounded buffer in class CircularBuffer (Fig. 26.18) as a circular buffer that uses a shared array of three elements. A circular buffer writes into and reads from the array elements in order, beginning at the first cell and moving toward the last. When a Producer or Consumer reaches the last element, it returns to the first and begins writing or reading, respectively, from there. In this version of the producer/consumer relationship, the Consumer consumes a value only when the array is not empty and the Producer produces a value only when the array is not full. The statements that created and started the thread objects in the main method of class SharedBufferTest2 (Fig. 26.17) now appear in class CircularBufferTest (Fig. 26.19).

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