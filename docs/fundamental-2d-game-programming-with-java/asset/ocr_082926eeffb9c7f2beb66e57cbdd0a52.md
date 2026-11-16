```
System.out.println( "Threadpool Shutdown :" ) );
} catch( InterruptedException e ) {
// at this point, just give up...
e.printStackTrace();
System.exit( -1 );
}
}
}
protected void sleep( int ms ) {
try {
Thread.sleep( ms );
} catch( InterruptedException ex ) { }
public static void main( String[] args ) {
new BlockingQueueExample().runTest();
}
}
```

# USING A STATE MACHINE

One way to use the new BlockingHardware class in a game loop is with a state machine. This state machine idea will also be used in Chapter 13, “Sound,” so if it doesn’t make sense, there are more examples coming. A state machine is a simple way to perform certain actions based on received events. A classic state machine example is a door, with open, closed, and locked states. The unlocked state is the same as closed, so it is excluded. Events could be (for example) a key event and a hand event. If a hand event is used on a closed door, it would transition to open. A hand event on an open door would close it. A key event on a closed door would lock it. A key event on a locked door would return it to the closed state. A hand event on an locked door or a key event on an open door would do nothing. See Figure 12.2.

| | Hand | Key |
|---|---|---|
| Open(0) | (1) | X |
| Closed(1) | (0) | (2) |
| Locked(2) | X | (1) |

Figure 12.2 Door State Machine. © 2014 Timothy Wright.