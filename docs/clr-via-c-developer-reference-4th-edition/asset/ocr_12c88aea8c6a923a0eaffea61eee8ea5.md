It can also decide to fail an AppDomain creation, or it can decide to return a reference to an existing AppDomain instead. When a new AppDomain is created, the CLR creates a new AppDomainManagerderived object which can also modify configuration settings, how execution context is flowed between threads, and permissions granted to an assembly.

# Writing a Robust Host Application

A host can tell the CLR what actions to take when a failure occurs in managed code. Here are some examples (from least severe to most severe):

+   - The CLR can abort a thread if it is taking too long to execute and return a response. (I'll discuss this in the next section)
- The CLR can unload an AppDomain. This aborts all of the threads in the AppDomain and causes the problematic code to be unloaded.
- The CLR can be disabled. This stops any more managed code from executing in the process, but unmanaged code is still allowed to run.
- The CLR can exit the Windows process. This aborts all of the threads and unloads all of the AppDomains first so that cleanup operations occur, and then the process terminates.

The CLR can abort a thread or AppDomain gracefully or rudely. A graceful abort means that cleanup code executes. In other words, code in Finally blocks runs, and objects that have Finalize methods executed does not execute. In other words, code in Finally blocks may not run, and objects may not have their Finalize methods executed. A graceful abort cannot a thread that is in a catch or Finally block. Unfortunately, a thread that is in unmanaged code or in a constrained execution region (CER) cannot be aborted.

A host can set what is usually an escalation policy, which tells the CLR how to deal with managed code failures. For example, SQL Server tells the CLR what to do when an unhandled exception is thrown while is managed code. When a thread experiences an unhandled exception, the CLR first attempts to upgrade the exception to a graceful abort. If the thread does not abort in a specified time, the CLR attempts to upgrade the graceful thread to a rude abort.

I just described is what usually happens. However, if the thread experiencing the unhandled exception is in a critical region, the policy is different. A thread that is in a critical region is a thread that has entered a synchronization lock that must be released by the thread, for example, a thread that has called Monitor.Enter, Mutex.WaitOne, or one of ReaderLock.AcquireReaderLock or AcquireReaderWriter methods.Successfully waiting for an AutoResetEvent, or Semaphore cannot be aborted in a critical region because

> All of these locks internally call Thread's BeginCriticalRegion and EndCriticalRegion to indicate whether they enter and leave regions. You can call these methods if you need to. Normally, this will be necessary if you are interoperating with unmanaged code.

CHAPTER 22 CLR Hosting and AppDomains 557