classes is “static methods may be called from any thread, but instance methods may be called only from the thread that allocated the instance.”

A **task** is a unit of potentially high-latency work that produces a resultant value or desired side effect. The distinction between tasks and threads is as follows: A task represents a job that needs to be performed, whereas a thread represents the worker that does the job. A task is useful only for its side effects and is represented by an instance of the `Task` class. A task used to produce a value of a given type is represented by the `Task<T>` class, which derives from the nongeneric `Task` type. These can be found in the `System.Threading.Tasks` namespace.

A **thread pool** is a collection of threads, along with logic for determining how to assign work to those threads. When your program has a task to perform, it can delegate a worker thread from the pool, assign the thread to perform the task, and then de-allocate it when the work completes, thereby making it available the next time additional work is requested.

# BEGINNER TOPIC

# **The Why and How of Multithreading**

There are two principal scenarios for multithreading: enabling multitasking and dealing with latency.

Users think nothing of running dozens of processes at the same time. They might have presentations and spreadsheets open for editing while at the same time they are browsing documents on the Internet, listening to music, receiving instant messages and email arrival notifications, and watching the little clock in the corner. Each of these processes has to continue to do its job even though it is not the only task the machine has to attend to. This kind of multitasking is usually implemented at the process level, but there are situations in which you want to do this sort of multitasking within a single process.

For the purposes of this book, however, we will mostly be considering multithreading as a technique for dealing with latency. For example, to import a large file while simultaneously allowing a user to click Cancel, a developer creates an additional thread to perform the import. By performing the import on a different thread, the user can request cancellation instead of freezing the user interface until the import completes.