
![](img/c654620410a83b786d7196f7d03d0886_165_0.png)

Now more of the usage graphs are showing activity and the CPU usage is up from 25% to 50% as our program is now using more processors.

## Making lots of Threads

From the displays above you can see that if we create an additional thread we can use more of the power the computer gives us. In fact, we can create many more threads than this:

```
for (int i = 0; i < 100; i = i + 1)
{
    Thread t1 = new Thread(busyLoopMethod);
    t1.Start();
}
```

This loop will create 100 threads, all running the busyLoop method. Now our computer is really busy:

![](img/c654620410a83b786d7196f7d03d0886_165_1.png)

All the processors are now maxed out, and the CPU usage is up to 100%. If you run this code you might actually find that the machine becomes slightly less responsive, and that all the cooling fans come on full blast.

## Programmer's Point: Too Many Threads Will Slow Everything Down

Note that nothing has stopped your program from starting a large number of threads running. This is potentially dangerous. If you run too many threads at once you will slow everything down. This is actually the basis of a type of attack on your computer, called a Denial of Service attack. This makes your computer unusable by starting a huge number of threads which tie up the processor. Fortunately Windows boosts the priority of threads that deal with user input so you can usually get control and stop such wayward behaviour.

## 5.6.5 Threads and Synchronisation

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

- 1. Thread 1 fetches the value of the count variable so that it can add 1 to it.
- 2. Before the addition can be performed, Thread 1 is stopped and Thread 20 is allowed to run.
- 3. Thread 20 fetches the value of count, adds one to it and stores it back in memory.
- 4. Sometime later Thread 1 gets control again, adds 1 to the value it fetched before it was stopped and stores the result back in memory.

Because of the way that Thread 1 was interrupted during its calculation, it has overwritten the changes that Thread 20 made. As the threads run they are all loading, incrementing and storing the value of count and overwriting changes that they have made.

What we need is a way of stopping the threads from interrupting each other. The statement count = count + 1; must be allowed to complete without being interrupted. You can do this by using a feature called mutual exclusion or mutex. We can return to our train analogy here.

### Using Mutual Exclusion to Manage Data Sharing

Allowing two threads to share the same variable is a bit like allowing two trains to share the same piece of track. Both are dangerous. The single track problem was solved by using a single brass token which was held by the engine driver. When they entered the single track they were given the token. When the train left the single track section the driver handed the token back. Anyone wanting to enter the track had to wait for their turn with the token.

Mutual exclusion works in just the same way by using an instance of an object to play the role of the token.

```
static object sync = new object();
```

If you don't want to destroy a thread, but simply make it pause for a while, you can call the Suspend method on the thread:

```
t1.Suspend();
```

The thread is put to sleep until you call the Resume method on that thread.

```
t1.Resume();
```

### Finding the state of a thread

You can find out the state of a thread by using its ThreadState property. This is an enumerated value which has a number of possible values.

The most useful are:

| ThreadState.Running | the thread is running |
| ThreadState.Stopped | the thread has finished executing the thread method |
| ThreadState.Suspend | the thread has been suspended |
| ThreadState.WaitSleepJoin | the thread is executing a Sleep, waiting to join with another thread or waiting for a Monitor |

As an example, to display a message if thread t1 is running:

```
if ( t1.ThreadState == ThreadState.Running )
{
    Console.WriteLine("Thread Running");
}
```

## 5.6.7 Staying Sane with Threads

Threads are very useful. They let your program deal with tasks by firing off threads of execution. The best way to create a system that must support many users, for example a web server, is to create a multi-threaded application which starts up a thread to deal with each incoming request. This makes the code easier to manage and also means that your program can make the best use of the processing power available.

However, threads can also be a great source of frustration. We know that our programs sometimes produce errors when they run. This is mostly because we have done something wrong. When we get a problem we look at what has happened and then work out what the fault is. Up until now our programs have been single threaded and we have been able to put in the data which causes the problem. This will cause the program to fail, at which point we can begin to fix it.

Unfortunately when you add multi-threading to a solution this is no longer true. A program which works fine for 99.999% of the time may fail spectacularly, or just lock up completely, when a specific set of timing related events occur. A synchronization problem like the "Deadly Embrace" described above may only appear when two users both request a particular feature at exactly the same time.

When you have problems with a multi-threaded system the biggest difficulty is always making the fault occur so you can fix it. Often the only way to investigate the problem is to add lots of write statements so that the program makes a log that you can examine after it has failed. Of course, time spent writing the log output affects the timing of events in the program and can often cause a fault to move or, if you are very lucky, vanish completely.

You should protect any variables shared between threads of execution by using the Monitor class as described above. This will stop inadvertent data corruption. If variables sometimes get "out of step" then this is sure sign that you have several threads fighting over data items.

You should try to avoid any "Deadly Embrace" situations by making your threads either producers or consumers of data. If consumers are always waiting for producers
(and producers never wait for consumers) then you can be sure that you never get the situation where one thread waits for a thread that is waiting for it.

Finally you should design in the logging and debugging behaviour (you can always use conditional compilation to turn the logging off later) so that if you do have a problem it is easy to get some diagnostic information which will tell you what your program was doing at the time it went wrong.

## Programmer's Point: Put Threads into your Design

I think what I am really saying here is that any thread use should be designed into your program, and not tacked on afterwards. If you want to use threads the way that they are managed and how they communicate should be decided right at the start of your design and your whole system should be constructed with them in mind.

## 5.6.8 Threads and Processes

You can regard different threads as all living in the computer together in the same way that a number of trains can share a particular railway. The next step up is to have more than one railway. In programming terms this is a move from threads to processes.

Processes are different from threads, in that each process has its own memory space which is isolated from other processes.

When you are using a word processor and a web browser at the same time on your computer each of them is running on your computer as a different process. Your word processor may fire off several threads that run within it (perhaps one to perform spell checking), but nothing in the word processor program can ever directly access the variables in the browser.

In a C# program you can create a process and start it in a similar way to starting a thread. You can also use the Process class to start programs for you. This class is held in the System.Diagnostics namespace, so you can add a Using statement to make it easier to get hold of the class:

```
using System.Diagnostics;
```

To start a program on your system you can use the Start method on the Process class:

```
Process.Start("Notepad.exe");
```

The Start method is supplied with the name of the program that you want to start. The above line of C# would start the Notepad program.

You can also create Process instances that you can control from within your program in a similar manner to threads.

## 5.7 Structured Error Handling

By now I hope that you are starting to think very hard about how programs fail. You should also be thinking that when you build a system you should consider how you are going to manage the way that it will fail. This is actually a very important part of the design process. When something bad happens the program must deal with this in a managed way. The key to achieving this is to think about making your own custom exceptions for your system.

We have been on the receiving end of exceptions already. We have seen that if something bad happens whilst a file is being read, or a Parse method is given an invalid string, the system will throw an exception to indicate that it is unhappy. This means that potentially badly behaved code like this has to be enclosed in a Try...catch construction so that our program can respond sensibly. Now we are going to take a closer look at exceptions and see about creating our own exception types.
