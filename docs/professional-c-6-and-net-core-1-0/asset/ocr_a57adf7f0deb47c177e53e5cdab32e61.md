# 21
Tasks and Parallel Programming

# What’s In This Chapter?

+   - An overview of multi-threading
+   - Working with the `Parallel` class
+   - Working with Tasks
+   - Using the Cancellation framework
+   - Using the Data Flow Library

# Wrox.com Code Downloads for This Chapter

The wrox.com code downloads for this chapter are found at www.wrox.com/go/professionalcsharp6 on the Download Code tab. The code for this chapter is divided into the following major examples:

+   - Parallel
+   - Task
+   - Cancellation
+   - DataFlow

# Overview

There are several reasons for using multiple threads. Suppose that you are making a network call from an application that might take some time. You don’t want to stall the user interface and force the user to wait idly until the response is returned from the server. The user could perform some other actions in the meantime or even cancel the request that was sent to the server. Using threads can help.

For all activities that require a wait—for example, because of file, database, or network access—you can start a new thread to fulfill other activities at the same time. Even if you have only processing-intensive tasks to do, threading can help. Multiple threads of a single process can run on different CPUs, or, nowadays, on different cores of a multiple-core CPU, at the same time.

You must be aware of some issues when running multiple threads, however. Because they can run during the same time, you can easily get into problems if the threads access the same data. To avoid that, you must implement synchronization mechanisms.

Since .NET 4, .NET has offered an abstraction mechanism to threads: tasks. Tasks allow building relations between tasks—for example, one task should continue when the first one is completed. You can also build a hierarchy consisting of multiple tasks.