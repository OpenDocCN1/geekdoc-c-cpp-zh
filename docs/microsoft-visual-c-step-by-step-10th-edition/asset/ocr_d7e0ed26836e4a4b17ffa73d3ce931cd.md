```
{
  // Code that requires exclusive access to a shared resource
  ...
}
```

The lock object attempts to obtain a mutual-exclusion lock over the specified object (you can actually use any reference type, not just object), and it blocks execution if this same object is currently locked by another thread. When the thread obtains the lock, the code in the block following the lock statement runs. At the end of this block, the lock is released. If another thread is blocked waiting for the lock, it can then grab the lock and continue its processing.

# Synchronization primitives for coordinating tasks

The lock keyword is fine for many simple scenarios, but in some situations, you might have more complex requirements. The System.Threading namespace includes some additional synchronization primitives that you can use to address these situations. These synchronization primitives are classes designed for use with tasks; expose locking mechanisms that restrict access to a resource while a task holds the lock.

These primitives support a variety of locking techniques that you can use to implement different styles of concurrent access, ranging from simple exclusive locks (where a single task has sole access to a resource), to semaphores (where multiple tasks can access a resource simultaneously but in a controlled manner), to reader/writer locks (which enable different tasks to share read-only access to a resource while guaranteeing exclusive access to a thread that needs to modify the resource). For more information and examples, the following sections summarize some of these primitives. For the documentation provided with Visual Studio 2022.

> Note .NET Framework has included a respectable set of synchronization primitives since its initial release. The following list describes only the most recent primitives included in the System.Threading namespace. There is some overlap between the new primitives and those provided