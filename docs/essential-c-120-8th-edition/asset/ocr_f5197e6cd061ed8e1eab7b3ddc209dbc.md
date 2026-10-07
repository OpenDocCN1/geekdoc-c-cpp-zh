# Chapter 22: Thread Synchronization

instance itself can block using this keyword, the caller that created the instance can pass instance to a synchronization lock.

As a result, two different synchronization blocks that synchronize two entirely different sets of data could potentially block each other. Although unlikely, sharing the same synchronization target could have an unintended performance impact and, in extreme cases, could even cause a deadlock. Instead of locking on this or even typeof(type), it is better to define a private, read-only field on which no one will block the class that has access to it.

Another lock to avoid is string because of the risk associated with string interning. If the same string constant appears within multiple locations, it is likely that all locations refer to the same instance, making the scope of the lock broader than expected.

In summary, you should use a per-synchronization context instance of type object for the lock target.

> Guidelines
AVOID locking on this, System.Type, or a string.
DO declare a separate, read-only synchronization variable of type object for the synchronization target.

# Avoid Synchronizing with MethodImplAttribute

One synchronization mechanism introduced in .NET 1.0 was the MethodImplAttribute. Used in conjunction with the MethodImplOptions.synchronized method, this attribute marks a method as synchronized, so that only one thread can execute the method at a time. To achieve this, the JIT essentially treats the method as though it is surrounded by lock(this) or, in the case of a static method, locks on the type. Such an implementation means that, in fact, the method and all methods on the same class, decorated with the attribute and enum parameter, are synchronized—rather than each method being synchronized relative to itself. In other words, given two or one of them will be able to execute at a time, and the method that is executing will block all calls by other threads to or