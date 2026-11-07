“Under the hood,” **async** uses a `std::promise` object from which it obtains the returned **future**. When the task completes, **async** stores the task’s result in the **promise**. **async**’s caller uses the **future** to access the result in the **promise**—in our case, a Factor-Results object. You do not need to work with the **promise** directly.

To ensure that the program does not terminate until the tasks complete and to receive the results from each task, lines 129–130 call each **future**’s get member function. If the task is still running, **get** blocks the calling thread, which waits until the task completes; otherwise, **get** immediately returns the task’s result. Function **get**’s return type is whatever the task function returns. Once the results are available, lines 129–130 pass them to function displayResults. The program’s output shows unique thread IDs, confirming that both **getFactors** tasks executed in separate **threads**.

If **async**’s task throws an exception, the **future** contains the exception rather than the task’s result, and calling **get** rethrows the exception. If multiple threads need access to an asynchronous task’s result, you can use `std::shared_future` objects.

# `std::packaged_task` vs. `std::async`

Another way to launch asynchronous tasks is `std::packaged_task`. The key differences between **async** and **packaged_task** are as follows:

+   - You must call its **get_future** member function to get the associated **future** object for obtaining the task’s results at a later time.
+   - A **packaged_task** executes on the thread that calls the task’s `operator()` function.
+   - To execute a **packaged_task** in a separate thread, you create the thread and initialize it with `std::move(yourPackagedTaskObject)`. When the thread completes, you can call **get** on the task’s **future** object to obtain the result.

# 17.11 **Thread-Safe. One-Time Initialization**

Sometimes a variable should be initialized exactly once, even when concurrent threads try to execute the variable’s initialization statement. Here, we discuss two mechanisms for one-time, thread-safe initialization of a variable.

# `static` Local Variables

When a function defines a `static` local variable and concurrent threads execute that function, the C++ standard specifies that the variable’s initialization “is performed the first time control passes through its declaration.” So, the first thread that executes the `static` local variable’s declaration performs the initialization. All other threads attempting to execute the static variable’s declaration are blocked until the first thread completes the vari-

+   81. “`std::shared_future`.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/thread/shared_future.
+   
+   82. “`std::packaged_task`.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/thread/packaged_task.
+   
+   83. C++ Standard, “8.8 Declaration Statement.” Accessed April 18, 2023. https://timsong-cpp.github.io/cppwp/n4861/stmt.dcl#4.
+   
+   84. “Storage Class Specifiers—static Local Variables.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/language/storage_duration#Static_local_variables.