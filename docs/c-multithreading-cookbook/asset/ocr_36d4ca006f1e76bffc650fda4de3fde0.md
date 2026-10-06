# Advanced Thread Management

One thing that is common for such mechanisms is abstraction of the root object that is responsible for managing its tasks. This is very important in order to maintain correct synchronization and exclusive access. Such an object—manager—should create and manage tasks, ensuring that the necessary resources are available. It must also control task execution in order to ensure that no two or more tasks perform invalid or unsynchronized operations. It should also destroy tasks and release used resources correctly for future use.

One of these abstractions is a pool of threads for executing tasks in parallel. When designing applications with complex or important concurrent operations, users must involve some type of thread hierarchy—where one thread is more important than the other threads and, in some way, it manages the others. In such situations, users must take care of used system resources, the correct way of granting exclusive access, synchronization, and so on. For all these reasons, the user should first design a smart object that will be able to satisfy all the above requirements, while at the same time, provide comfortable development.

# Using thread pools

Here we will explain a thread pool, which can be represented as a list of worker threads that, when available, will execute the required tasks. This is good when an application wants to reduce the high number of threads and provide management for working threads. Another scenario where the application benefit is when there is a large number of threads responsible for small tasks. In such situations, the overhead for creation and destruction of a large number of threads is significant, and should be avoided with a small number of threads that will execute the entire work.

We see a typical thread pool implementation in the following diagram:

![](bbox=[0.181, 0.555, 0.816, 0.856])