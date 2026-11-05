# 5.6.5 Threads and Synchronisation

You might be wondering why all the threads don't fight over the value of count that is being used as the loop counter. This is because the variable is local to the busyLoop method:

```
static private void busyLoop()
{
    long count;
    for (count = 0; count < 100000000000; count = count+1)
    {
    }
}
```

The count variable is declared within the body of the method. This means that each method has its own copy of this local variable. If you are still thinking about trains as trains, it is as if the data for each thread is held in tracks that are pulled along behind the train. We could make a tiny change to this code and make the count variable a member of the class:

```
static long count;
static private void busyLoop()
{
    for (count = 0; count < 100000000000; count = count + 1)
    {
    }
}
```

The method looks very similar, but now every thread running busyLoop is sharing the same count variable. This is potentially disastrous. It is now very hard to predict how long this multi-threaded program will take to finish. Consider the following sequence of actions:

+   1. Thread 1 fetches the value of the count variable so that it can add 1 to it.
+   2. Before the addition can be performed, Thread 1 is stopped and Thread 20 is allowed to run.
+   3. Thread 20 fetches the value of count, adds one to it and stores it back in memory.
+   4. Sometime later Thread 1 gets control again, adds 1 to the value it fetched before it was stopped and stores the result back in memory.

Because of the way that Thread 1 was interrupted during its calculation, it has overwritten the changes that Thread 20 made. As the threads run they are all loading, incrementing and storing the value of count and overwriting changes that they have made.

What we need is a way of stopping the threads from interrupting each other. The statement count = count + 1; must be allowed to complete without being interrupted. You can do this by using a feature called mutual exclusion or mutex. We can return to our train analogy here.

# Using Mutual Exclusion to Manage Data Sharing

Allowing two threads to share the same variable is a bit like allowing two trains to share the same piece of track. Both are dangerous. The single track problem was solved by using a single brass token which was held by the engine driver. When they entered the single track they were given the token. When the train left the single track section the driver handed the token back. Anyone wanting to enter the track had to wait for their turn with the token.

Mutual exclusion works in just the same way by using an instance of an object to play the role of the token.

```
static object sync = new object();
```