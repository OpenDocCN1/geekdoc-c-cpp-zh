# Chapter 23. Improving throughput by using tasks

After completing the chapter, you will be able to:

+   - Describe the benefits of implementing parallel operations in an application.
+   - Use the *Task* class to create and run parallel operations in an application.
+   - Use the *Parallel* class to parallelize some common programming constructs.
+   - Cancel long-running tasks and handle exceptions raised by parallel operations.

In the bulk of the preceding chapters in this book, you’ve learned how to use C# to write programs that run in a single-threaded manner. By *single-threaded*, I mean that at any one point in time, a program has been executing a single instruction. This might not always be the most efficient approach for an application to take. If you have the appropriate processing resources available, some applications might run more quickly if you divide them into parallel paths of execution that can run concurrently. This chapter is concerned with improving throughput in your applications by maximizing the use of available processing power. Specifically, in this chapter you will learn how to use *Task* objects to apply effective multitasking to computationally intensive applications.

# Why perform multitasking by using parallel processing?

There are two primary reasons why you might want to perform multitasking in an application:

+   - **To improve responsiveness** A long-running operation may involve tasks that do not require processor time. Common examples include I/O bound operations such as reading from or writing to a local disk or sending and receiving data across a network. In both of these cases, it does not make sense to have a program burn CPU cycles waiting for the operation to complete when the program could be doing something more useful instead (such as responding to user input). Most users of mobile devices take this form of responsiveness for granted and don’t expect their tablet to simply halt while it is sending and receiving email, for example. Chapter 24, “Improving response time by performing asynchronous operations,” discusses these features in more detail.

+   - **To improve scalability** If an operation is CPU bound, you can improve scalability by making efficient use of the processing resources available and using these resources to reduce the time required to execute the operation. A developer can determine which operations include tasks that can be performed in parallel and arrange for these elements to be run