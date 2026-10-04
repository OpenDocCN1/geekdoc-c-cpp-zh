```
Console.WriteLine("ComputeBoundOp: state={0}", state);
Thread.Sleep(1000); // Simulates other work (1 second)
```

// When this method returns, the thread goes back
// to the pool and waits for another task

}

When I compile and run this, I get the following output.

Main thread: queuing an asynchronous operation
Main thread: doing other work...
In ComputeBoundOp: state=5

And, sometimes when I run this code, I get this output.

Main thread: queuing an asynchronous operation
In ComputeBoundOp: state=5
Main thread: doing other work...

The difference in the order of the lines in the output is attributed to the fact that the two methods are running asynchronously with respect to one another. The Windows scheduler determines when to thread each file, or it may them both simultaneously if the application is running on a multi-CPU machine.

> Note If the callback method throws an exception that is unhandled, the CLR terminates the process (which hosts its own policy). Unhandled exceptions are discussed in Chapter 20, "Exceptions and State Management."

> Note For Windows Store apps, the System.Threading.ThreadPool class is not publicly exposed. However, it is used indirectly when you use types in the System.Threading.Tasks namespace (see the "Tasks" Section later in this chapter).

# Execution Contexts

Every thread has an execution context data structure associated with it. The execution context includes things as security settings (compressed stack, Thread's Principal property, and Windows identity), host settings (see System.Threading.HostExecutionContextManager), and logical call data (see System.Runtime.Messaging.CallContext.Logical-SetData and Logical-GetData methods). When a thread executes code, some operations are affected by the values of the thread's execution context. This is certain for the security settings. whenever a thread uses another (helper) thread to perform tasks, the issuing thread's execution context should flow (be copied) to the helper thread. This ensures that any operations performed by helper thread(s) are executing with the same security settings and host settings. It also