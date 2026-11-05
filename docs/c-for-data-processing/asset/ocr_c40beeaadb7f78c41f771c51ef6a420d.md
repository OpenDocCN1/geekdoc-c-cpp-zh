single track, a computer can run more than one thread in a single block of program code.

A computer can support multiple threads in two ways. The first is by rapidly switching between active threads, giving each thread the chance to run for a limited time before moving on to run another. When a thread is not running it is waiting for its turn to run. As far as the thread is concerned it is running continuously, but in reality a thread may only be active for a small fraction of a second now and then.

The second way to support multiple threads is to actually have more than one processor. The first computers had only one processor and so were forced to use "time slicing" to support multiple threads. Newer machines now have "dual core" or even "quad core" processors which can actually run multiple threads simultaneously.

# 5.6.2 Why do we have threads?

Threads make it possible for your computer to do something useful while one program is held up. Your system can play music and download files while your program waits for you to press the next key. A modern computer can perform many millions of instructions per second; it makes sense to share this ability amongst several tasks.

The programs that you have been writing and running have all executed as threads in your computer. This is how your program can be active at the same time as other programs you may wish to use alongside it. You have not been aware of this because the operating system (usually Windows) does a very good job of sharing out the processing power.

Threads provide another level of "abstraction", in that if we wish to do more than one thing at the same time it is very useful just to send a thread off to perform the task, rather than interleave the second task with the first. If I wrote a word processor we might find it useful to create threads to perform time consuming tasks like printing or spell checking. These could be performed "in the background" while the user continues to work on the document.

Threads are also how Windows forms respond to events. You have seen that a "click" event from a Button component can be made to run an event handler code. The Windows system actually creates a new thread of execution which runs the event handler code.

# Programmer's Point: Threads can be dangerous

In the same way that letting two trains share the same railway track can sometimes lead to problems, programs that use threads can also fail in spectacular and confusing ways. It is possible for systems to fail only when a certain sequence of events causes two previously well behaved threads to "fight" over a shared item of data. Bugs caused by threading are amongst the hardest ones to track down and fix because you have to make the problem happen before you can fix it, and the circumstances that cause the fault may only occur every now and then. I'm going to give some tips on how to make sure that your programs don't fall foul of threading related bugs, and I suggest that you follow these carefully.

# 5.6.3 Threads and Processors

Consider the following method:

```
static private void busyLoop()
{
    long count;
    for (count = 0; count < 1000000000000; count = count+1)
    {
    }
}
```