Notice that the read returns immediately in ASYNC mode. If you select any of the other modes then it only returns when a character is received. In this case you don't need the if statement to test for a result. However, if the device you are connecting to never sends a character, the loop hangs forever.

# Using Events

There is a tendency among IoT programmers to use interrupts too often. They are useful when you need to deal with a low-priority event that occurs very rarely. For something that is important and very, you usually need to use a polling loop to keep up. You still need to know how to use events to work with the serial port and there are some tricky things you have to get right.

There are two event sources that you can control:

+   * int eventAfter(int len)
* int eventAfter(int len,MicroBitSerialMode)

which trigger an event if there are the specified number of characters in the receive buffer, in addition there are another two:

+   * int eventOn(ManagedString delimiters)
* int eventOn(ManagedString delimiters,MicroBitSerialMode)

which trigger an event if any of the specified delimiters are present in the receive buffer.

There are two things to notice when using these events. The first is that, at the moment, the framework does not allocate buffers until you have actually used the serial device. What this means is that you can set up a program that looks reasonable but never fires an event because the receive buffer is never created. The second problem is that these events only fire once.

Both events have an ID of:

```
MICROBIT_ID_SERIAL
```

and respective values:

```
MICROBIT_SERIAL_EVT_HEAD_MATCH
MICROBIT_SERIAL_EVT_DELIM_MATCH
```

Notice that you can the usual modes but SPINWAIT will return an error and SLEEP will pause the fiber and wait for the event.