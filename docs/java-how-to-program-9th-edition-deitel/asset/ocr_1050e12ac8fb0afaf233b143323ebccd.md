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

Fig. 26.10 | Producer with a run method that inserts the values 1 to 10 in buffer. (Part 2 of 2.)

Class Consumer (Fig. 26.11) also implements interface Runnable, allowing the Consumer to execute concurrently with the Producer. Lines 11–14 initialize Buffer reference sharedLocation with an object that implements the Buffer interface (created in main, Fig. 26.13) and passed to the constructor as the parameter shared. As we’ll see, this is the same UnsynchronizedBuffer object that’s used to initialize the Producer object—thus, the two threads share the same object. The Consumer thread in this program performs the tasks specified in method run (lines 17–39). Lines 21–35 iterate 10 times. Each iteration invokes Thread method sleep (line 26) to put the Consumer thread into the timed waiting state for up to 3 seconds. Next, line 27 uses the Buffer’s get method to retrieve the value in the shared buffer, then adds the value to variable sum. Line 28 displays the total of all the values consumed so far. When the loop completes, lines 37–38 display a line indicating the sum of the consumed values. Then method run terminates, which indicates that the Consumer completed its task. Once both threads enter the terminated state, the program ends.