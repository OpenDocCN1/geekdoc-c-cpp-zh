At this point, each thread is waiting on the other thread before proceeding, so each thread is blocked, leading to an overall deadlock in the execution of that code.

# Uncertainty

The problem with code that is not atomic or causes deadlocks is that it depends on the order in which processor instructions across multiple threads occur. This dependency introduces uncertainty concerning program execution. The order in which one instruction will execute relative to an instruction in a different thread is unknown. Many times, the code will appear to behave uniformly, but occasionally it will not, and this is the crux of multithreaded programming. Because such race conditions are difficult to replicate in the laboratory, much of the quality assurance of multithreaded code depends on long-running stress tests, specially designed code analysis tools, and a significant investment in code analysis/reviews.

# Running and Controlling a Separate Thread

The operating system implements threads and provides various unmanaged APIs to create and manage those threads. The CLR wraps these unmanaged threads and exposes them in managed code via the System.Threading.Tasks.Task class, which represents an asynchronous operation. However, a Task does not map directly to an unmanaged thread. Rather, the Task provides a degree of abstraction to the underlying unmanaged thread construct.

Creating a thread is a relatively expensive operation. Therefore, whenever you can reuse a thread between two or more sets of instructions (rather than re-creating the thread for each set) the overall execution is potentially more efficient. In .NET Framework 4, instead of creating an operating system thread each time a Task is created, the Task requests a thread from the thread pool. The thread pool evaluates whether to create an entirely new thread or to allocate an existing thread (such as one that previously finished executing) to the Task request.