.NET Framework 4 adds another level of abstraction to the notion of running work in a parallel manner. This is realized by the Task Parallel Library (TPL), exposed through additions to the System.Threading namespace. This new library has its own notion of task schedulers, which employ interesting techniques to make sure multiple cores are leveraged in an optimized manner. We discuss some of this as well, focusing on the Task<T> class and explaining how this new scheduling infrastructures does something known as work stealing.

# Where It All Starts: The Thread Class

The closest you can get to a “raw thread” is using the Thread class, which lives in the System.Threading namespace that will be the topic of this chapter. By “raw thread” we mean a native (as all of them ultimately are) thread that can run managed code but isn’t subject to lots of additional management by the CLR or any library. In particular, no techniques such as pooling or specialized scheduling are employed.

# Creating Threads

Use of the Thread class is pretty simple. We start by looking at the instance members defined on the Thread class, so we need to create an instance first. All a thread object needs to know about is what code it has to run. As you should infer by now, the idea of delegating execution of code is where delegates enter the picture. It shouldn’t come as a surprise that the constructors of Thread take in delegate-typed objects:

```
public Thread(ParameterizedThreadStart start);
public Thread(ThreadStart start);
```

Overloads exist that can control the maximum stack size the newly created thread can use, but we omit this detail from our discussion. From the two constructors, we can pick one with the most convenient delegate type. Let’s start by looking at the second one, which is the simpler of the two:

```
public delegate void ThreadStart();
```

In fact, this is nothing but the Action delegate (which was introduced at a later point, hence the apparent duplication): It takes no parameters and doesn’t return anything.

# SINGLE-METHOD INTERFACES AND JAVA'S RUNNABLE

As mentioned earlier in this book, the frequent occurrence of single-method interfaces in lots of frameworks is exactly what warrants the introduction of a concept like delegates. Other frameworks, such as Java, have traditionally gone with a more pure object-oriented approach, where the act of passing a single piece of code around involves implementing an interface.