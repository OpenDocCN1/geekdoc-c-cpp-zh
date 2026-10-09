occurs on the worker thread. One solution is to wrap the body of the task

delegate with a try/catch block. Exceptions thrown on and subsequently

ccaught by the worker thread will consequentty not present problems, as

a try block will work normally on the worker thread. This is not the case,

however, for unhandled exceptions—those that the worker thread does

not catch.

Generally (starting with version 2.07 of the CLR), unhandled excep-

tions on any thread are treated as fatal, trigger the operating system

error reporting dialog, and cause the application to terminate abnor-

mally. All exceptions on all threads must be caught, and if they are

not, the application is not allowed to continue to run. (For some

advanced techniques for dealing with unhandled exceptions, see the

upcoming Advanced Topic titled “Dealing with Unhandled Exceptions

on a Thread.”) Fortunately, this is not the case, however, for unhan-

dled exceptions in an asynchronously running task. Rather, the task

scheduler inserts a catchall exception handler around the delegate so

that if the task throws an otherwise unhandled exception, the catchall

handler will catch it and record the details of the exception in the task,

avoiding any trigger of the CLR automatically terminating the process.

As we saw in Listing 19.6, one technique for dealing with a faulted

task is to explicitly create a continuation task that is the fault handler for

that task; the task scheduler will automatically schedule the continuation

when it detects that the antecedent task threw an unhandled exception.

If no such handler is present, however, and Wait() (or an attempt to get

the Result) executes on a faulted task, an AggregateException will be

thrown (see Listing 19.7 and Output 19.4).

# **LISTING 19.7: Handling a Task’s Unhandled Exception**

```
using System;
using System.Threading.Tasks;

public class Program
{

```

> 7. In version 1.0 of the CLR, an unhandled exception on a worker thread terminated the
thread but not the application. As a result, it was possible for a buggy program to have
all its worker threads die, but the main thread would continue to run, even though the
program was no longer doing any work. This is a confusing situation for users to be in; it
is better to signal to the user that the application is in a bad state and terminate it before
it can do any more harm.

![](bbox=[0.0, 0.55, 0.1, 0.6])