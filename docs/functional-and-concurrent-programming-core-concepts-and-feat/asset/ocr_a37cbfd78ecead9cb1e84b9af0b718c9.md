Tasks are stored in immutable lists, and the lists in an immutable map. As they run, all three threads access the map concurrently, and threads T2 and T3 also safely share the list tasksB. This is done without any locking or other synchronization.

You can greatly simplify the design of your multithreaded programs by avoiding shared mutable data, first by minimizing sharing—when possible, threads are better off working on their own data—and second by making shared data immutable as often as possible. In Part I of the book, we considered some of the advantages of immutability in the context of functional programming. Immutable objects are also tremendously beneficial to concurrent programming.

On the JVM, there is technically a difference between immutable objects and objects that are never mutated, due to a special treatment of final fields. Non-final fields (var fields in Scala) may require some form of initial synchronization before they can be freely read by any thread. This synchronization tends to happen naturally in clean, simple designs.¹ Still, it is good practice, when dealing with threads, to prefer val over var—or to add the final modifier in Java—for fields that are not intended for mutation. To decide if a non-final field of a never-mutated object can safely be read by a thread requires an understanding of the Java Memory Model (JMM), a somewhat advanced topic (see Section 22.5).

# 19.2 Encapsulating Synchronization Policies

You can freely share immutable objects among threads, but mutation of shared data requires that threads coordinate through synchronization, often in the form of exclusive locks. In Listing 18.5, for example, two threads were able to correctly share—and modify—a mutable list by locking the list before every access to it. As described in Section 18.6, the choice of locking the list itself is arbitrary. You could use any other object as a lock, as long as the object is shared and all the threads agree that this is the object to lock when accessing the list.

Relying on such an agreement is error-prone. It requires that user code always locks a specific lock before accessing an object, which can be checked only by considering all uses of the object throughout a code base. This is an onerous task if done manually.² It is like requiring that all modifications to an object’s public fields maintain some invariant. This is not practical. Instead, good designs rely on data encapsulation, a key feature of object-oriented programming: Mutable fields tend to be private, and public methods are available to modify them.

You can use the same principle—encapsulation—to control inter-thread synchronization. Instead of specifying a synchronization policy that code needs to follow to

¹For instance, the program in Listing 19.1 is still correct if the map is mutable and all the val are replaced with var, as long as the map is never mutated and the variables never reassigned.

²Indeed, some static analyzers do exactly this: When a value is almost always accessed with the same object locked, any access to the value without this lock is flagged as suspicious code.