to execute asynchronous compute-bound operations whenever possible. I go into the details doing this in Chapter 27, "Compute-Bound Asynchronous Operations."

However, there are some unusual occasions when you might want to explicitly create a thread dedicated to executing a particular compute-bound operation. Typically, you'd want to create a dedicated thread if you're going to execute code that requires the thread to be in a particular state that is not normal for a thread pool thread. For example, explicitly create your thread if any of the following is:

+   - You need the thread to run with a non-normal thread priority. All thread pools run at normal priority. Although you can change this, it is not recommended, and the priority change does not persist across thread pools.
- You need the thread to behave as a foreground thread, thereby preventing the application from dying until the thread has completed its task. For more information, see the "Foreground Threads vs. Background Threads" section later in this chapter. Thread pools are always background threads, and they may not complete their task if the CLR winds to terminate the process.
- The compute-bound task is extremely long-running. This way, I would not be taxing the thread pool's logic as it tries to figure out where to create an additional thread.
- You want to start a thread and possibly abort it prematurely by calling Thread.Abort (discussed in Chapter 22, "CLR Hosting and AppDomains").

To create a thread, you an instance of the System.Threading class, passing the name of a method into its constructor. Here is the prototype of Thread's constructor.

```
public sealed class Thread : CriticalFinalizerObject, ... {
    public Thread(ParameterizedThreadStart start);
    // Less commonly constructors are not shown here}
```

The start parameter identifies the method that the dedicated thread will execute, and this method must match the signature of the ParameterizedThreadStart delegate.4

```
delegate void ParameterizedThreadStart(Object obj);
```

Constructing a thread is a relatively lightweight operation because it does not actually create a physical operating system thread. To actually create the operating system thread and have it start executing the callback method, you must call Thread's Start method, passing it into the (state) that you passed as the callback method's argument.

> 4 For the record, the Thread also offers a constructor that takes a ThreadStart delegate that accepts no arguments and returns void. Personally, I recommend using this constructor and delegate because they are more limiting. If your method takes an Object and returns void, then you can invoke it by using a dedicated thread or invoke it using the thread pool (as shown in Chapter 27).

CHAPTER 26 Thread Basics 679