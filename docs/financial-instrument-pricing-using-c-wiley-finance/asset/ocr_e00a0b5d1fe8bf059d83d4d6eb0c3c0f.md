![](bbox=[0.463, 0.105, 0.553, 0.366])

**FIGURE 29.4**  Sequential computation

+   3. *Orchestration*: data access, communication and synchronisation of processes.
+   4. *Mapping*: bind processes to processors.

This is an iterative (sometimes combined with trial-and-error experimentation) process and we can spend much time making the program correct, free of race conditions and improving its speedup.

# 29.4 FUTURES AND PROMISES

These terms originated in the late 1970s. Futures and promises are constructs for synchronising program execution in programming languages. They describe an object that acts as a proxy for a result that is initially unknown (the terms *delayed* and *deferred* are also used). The result is unknown because the computation of the value has not yet completed.

More precisely, a *future* represents a read-only placeholder view of a variable while a *promise* is a writable, single-assignment entity that sets the value of the future. In short, the future is the value and a promise is the (asynchronous) function that sets the value. We can define a future without specifying which specific promise will set its value. Different possible promises may set the future’s value; however, *the value can only be set once*. It is possible to associate a future and a promise, as we shall see.

There is quite a bit of functionality to introduce. To this end, the class template
`std::future` has functionality for the following:

+   1. Create a future to hold the result of an asynchronous operation that is created using `std::async`, `std::packaged_task` or `std::promise`.
+   2. We can use several methods to query, wait for or extract a value from the `std::future`.
+   3. The asynchronous operation can modify *shared state* (which is linked to the created `std::future`) when it is ready to send the result to the creator.