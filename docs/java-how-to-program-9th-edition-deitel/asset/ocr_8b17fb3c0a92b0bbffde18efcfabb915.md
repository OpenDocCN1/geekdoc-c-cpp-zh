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

# 26.9 Producer/Consumer Relationship: The Lock and Condition Interfaces

Though the synchronized keyword provides for most basic thread-synchronization needs, Java provides other tools to assist in developing concurrent programs. In this section, we discuss the Lock and Condition interfaces. These interfaces give you more precise control over thread synchronization, but are more complicated to use.

# Interface Lock and Class ReentrantLock

Any object can contain a reference to an object that implements the Lock interface (of package java.util.concurrent.locks). A thread calls the Lock’s lock method (analogous to entering a synchronized block) to acquire the lock. Once a Lock has been obtained by one thread, the Lock object will not allow another thread to obtain the Lock until the first thread releases the Lock (by calling the Lock’s unlock method—analogous to ex-