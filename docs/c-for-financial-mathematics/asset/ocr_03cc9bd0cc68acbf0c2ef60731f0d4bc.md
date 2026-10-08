# 20.4.2 How Pipeline is implemented

Pipeline is not a C++ standard class. However, it is implemented using the standard `condition_variable` class.

The `condition_variable` class is designed to enable two threads to send signals to each other about when they should start processing. If a thread finds that it has no work to do, it should call `wait` on a condition variable. This method call will not return until another thread calls `notify_all` on the same condition variable. This basic mechanism allows one thread to pause its execution while it waits for another thread to complete a task.

The usual way of working with a `condition_variable` is to test the value of some variable to see if there is any work to do. If there is no work to do, call `wait`, otherwise perform the necessary work.

Meanwhile another thread will update the variable to indicate that there is some work to do and then call `notify_all`. This wakes up the waiting threads which check the variable again and, observing that there is now some work to do, get on and perform the necessary work.

For this pattern to work, we will need to use a `mutex` to ensure that we synchronise the use of any shared variables `workAvailable` correctly. In general whenever you use a `condition_variable` you will have an associated `mutex`. You should hold the `unique_lock<mutex>` whenever you call `wait` or `notify_all`. You should also hold such a lock whenever you use the variables that you are using to send work between the two threads.

The full process is illustrated in Figure 20.1. In this diagram Thread 1 has to wait for Thread 2 to complete some interesting task before beginning work itself. Thread 2 communicates that work has been done by changing the value of a boolean variable called `workAvailable` from false to true. The locks and condition variables are used as described above to ensure that Thread 1 will pause its execution until there is work available and will then commence processing.

This diagram is certainly complex. In practice, the situation is not as difficult to work with as it seems. This is because one always uses condition variables in essentially the same way with the same sequence of calls. Here is a summary of how to use a `condition_variable`.

+   - Whenever you use a `condition_variable` you should also create a `mutex` to guard the data.
- Test if the condition is met in a `while` loop. You will want to lock the `mutex` while testing your condition.
- Change the data that determines whether your condition passes before calling `notify_all`. Hold the lock while modifying the data: You should keep holding it until you have called `notify_all`.
- If you were to release the lock before calling `wait` it is possible that the condition may change just before you start waiting. As a result you must