

the circular buffer is full and the Producer must wait. Variable writeIndex (line 8) indicates the next location in which a value can be placed by a Producer. Variable readIndex (line 9) indicates the position from which the next value can be read by a Consumer.

## CircularBuffer Method set

CircularBuffer method set (lines 12–30) performs the same tasks as in Fig. 26.16, with a few modifications. The loop at lines 16–20 determines whether the Producer must wait (i.e., all buffer cells are full). If so, line 18 indicates that the Producer is waiting to perform its task. Then line 19 invokes method wait, causing the Producer thread to release the CircularBuffer’s lock and wait until there’s space for a new value to be written into the buffer. When execution continues at line 22 after the while loop, the value written by the Producer is placed in the circular buffer at location writeIndex. Then line 25 updates writeIndex for the next call to CircularBuffer method set. This line is the key to the buffer’s circularity. When writeIndex is incremented past the end of the buffer, the line sets it to 0. Line 27 increments occupiedCells, because there’s now one more value in the buffer that the Consumer can read. Next, line 28 invokes method displayState (lines 56–85) to update the output with the value produced, the number of occupied buffer cells, the contents of the buffer cells and the current writeIndex and readIndex. Line 29 invokes method notifyAll to transition waiting threads to the runnable state, so that a waiting Consumer thread (if there is one) can now try again to read a value from the buffer.

## CircularBuffer Method get

CircularBuffer method get (lines 33–53) also performs the same tasks as it did in Fig. 26.16, with a few minor modifications. The loop at lines 37–41 determines whether the Consumer must wait (i.e., all buffer cells are empty). If the Consumer must wait, line 39 updates the output to indicate that the Consumer is waiting to perform its task. Then line 40 invokes method wait, causing the current thread to release the lock on the CircularBuffer and wait until data is available to read. When execution eventually continues at line 43 after a notifyAll call from the Producer, readValue is assigned the value at location readIndex in the circular buffer. Then line 46 updates readIndex for the next call to CircularBuffer method get. This line and line 25 implement the circularity of the buffer. Line 48 decrements occupiedCells, because there’s now one more position in the buffer in which the Producer thread can place a value. Line 49 invokes method displayState to update the output with the consumed value, the number of occupied buffer cells, the contents of the buffer cells and the current writeIndex and readIndex. Line 50 invokes method notifyAll to allow any Producer threads waiting to write into the CircularBuffer object to attempt to write again. Then line 52 returns the consumed value to the caller.

## CircularBuffer Method displayState

Method displayState (lines 56–85) outputs the application’s state. Lines 62–63 output the values of the buffer cells. Line 63 uses method printf with a "%2d" format specifier to print the contents of each buffer with a leading space if it’s a single digit. Lines 70–82 output the current writeIndex and readIndex with the letters W and R, respectively.

## Testing Class CircularBuffer

Class CircularBufferTest (Fig. 26.19) contains the main method that launches the application. Line 11 creates the ExecutorService, and line 14 creates a CircularBuffer object and assigns its reference to `CircularBuffer` variable `sharedLocation`. Line 17 invokes the `CircularBuffer`’s `displayState` method to show the initial state of the buffer. Lines 20–21 execute the Producer and Consumer tasks. Line 23 calls method `shutdown` to end the application when the threads complete the Producer and Consumer tasks.

Each time the Producer writes a value or the Consumer reads a value, the program outputs a message indicating the action performed (a read or a write), the contents of buffer, and the location of `writeIndex` and `readIndex`. In the output of Fig. 26.19, the Producer first writes the value 1. The buffer then contains the value 1 in the first cell and the value −1 (the default value that we use for output purposes) in the other two cells. The write index is updated to the second cell, while the read index stays at the first cell. Next, the Consumer reads 1. The buffer contains the same values, but the read index has been updated to the second cell. The Consumer then tries to read again, but the buffer is empty and the Consumer is forced to wait. Only once in this execution of the program was it necessary for either thread to wait.

```java
// Fig. 26.19: CircularBufferTest.java
// Producer and Consumer threads manipulating a circular buffer.
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class CircularBufferTest
{
    public static void main( String[] args )
    {
        // create new thread pool with two threads
        ExecutorService application = Executors.newCachedThreadPool();

        // create CircularBuffer to store ints
        CircularBuffer sharedLocation = new CircularBuffer();

        // display the initial state of the CircularBuffer
        sharedLocation.displayState( "Initial State" );

        // execute the Producer and Consumer tasks
        application.execute( new Producer( sharedLocation ) );
        application.execute( new Consumer( sharedLocation ) );

        application.shutdown();
    } // end main
} // end class CircularBufferTest
```

```text
Initial State (buffer cells occupied: 0)
buffer cells:   -1   -1   -1
                ---  ---  ---
                  WR

Producer writes 1 (buffer cells occupied: 1)
buffer cells:    1   -1   -1
                ---  ---  ---
                 R    W
```

**Fig. 26.19** | Producer and Consumer threads manipulating a circular buffer. (Part 1 of 3.)

```
Consumer reads 1 (buffer cells occupied: 0)
buffer cells:    1   -1   -1
            ---  ---  ---
                 WR

Buffer is empty. Consumer waits.
Producer writes 2 (buffer cells occupied: 1)
buffer cells:    1    2   -1
            ---  ---  ---
                 R   W

Consumer reads 2 (buffer cells occupied: 0)
buffer cells:    1    2   -1
            ---  ---  ---
                     WR

Producer writes 3 (buffer cells occupied: 1)
buffer cells:    1    2    3
            ---  ---  ---
            W          R

Consumer reads 3 (buffer cells occupied: 0)
buffer cells:    1    2    3
            ---  ---  ---
            WR

Producer writes 4 (buffer cells occupied: 1)
buffer cells:    4    2    3
            ---  ---  ---
            R   W

Producer writes 5 (buffer cells occupied: 2)
buffer cells:    4    5    3
            ---  ---  ---
            R        W

Consumer reads 4 (buffer cells occupied: 1)
buffer cells:    4    5    3
            ---  ---  ---
                 R   W

Producer writes 6 (buffer cells occupied: 2)
buffer cells:    4    5    6
            ---  ---  ---
            W   R

Producer writes 7 (buffer cells occupied: 3)
buffer cells:    7    5    6
            ---  ---  ---
                 WR

Consumer reads 5 (buffer cells occupied: 2)
buffer cells:    7    5    6
            ---  ---  ---
                 W   R

Producer writes 8 (buffer cells occupied: 3)
buffer cells:    7    8    6
            ---  ---  ---
                     WR
```

```
Consumer reads 6 (buffer cells occupied: 2)
buffer cells:    7    8    6
            ---  ---  ---
               R     W

Consumer reads 7 (buffer cells occupied: 1)
buffer cells:    7    8    6
            ---  ---  ---
                  R   W

Producer writes 9 (buffer cells occupied: 2)
buffer cells:    7    8    9
            ---  ---  ---
               W   R

Consumer reads 8 (buffer cells occupied: 1)
buffer cells:    7    8    9
            ---  ---  ---
               W     R

Consumer reads 9 (buffer cells occupied: 0)
buffer cells:    7    8    9
            ---  ---  ---
               WR

Producer writes 10 (buffer cells occupied: 1)
buffer cells:   10    8    9
            ---  ---  ---
               R   W

Producer done producing
Terminating Producer
Consumer reads 10 (buffer cells occupied: 0)
buffer cells:   10    8    9
            ---  ---  ---
                  WR

Consumer read values totaling: 55
Terminating Consumer
```

Fig. 26.19 | Producer and Consumer threads manipulating a circular buffer. (Part 3 of 3.)

## 26.9 Producer/Consumer Relationship: The Lock and Condition Interfaces

Though the synchronized keyword provides for most basic thread-synchronization needs, Java provides other tools to assist in developing concurrent programs. In this section, we discuss the Lock and Condition interfaces. These interfaces give you more precise control over thread synchronization, but are more complicated to use.

## Interface Lock and Class ReentrantLock

Any object can contain a reference to an object that implements the Lock interface (of package java.util.concurrent.locks). A thread calls the Lock’s lock method (analogous to entering a synchronized block) to acquire the lock. Once a Lock has been obtained by one thread, the Lock object will not allow another thread to obtain the Lock until the first thread releases the Lock (by calling the Lock’s unlock method—analogous to ex-

