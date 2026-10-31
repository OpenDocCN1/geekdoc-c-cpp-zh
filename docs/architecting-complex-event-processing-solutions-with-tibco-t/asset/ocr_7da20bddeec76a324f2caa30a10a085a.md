# Locking Requires Programming Discipline

Because objects are not physically locked, making effective use of locks requires programming discipline. Every thread that requires access to an object requiring locking must obtain a lock. All it takes is one omission and the locking scheme breaks down. For this reason, it is good practice to clearly identify objects that require locking in their description and in accompanying design documentation.

# Avoiding Deadlocks

A deadlock can arise when two agents are each waiting for a lock that is presently being held by the other. Here is an example.

+   - Agent X has locked object A and is trying to lock object B; meanwhile,
+   - Agent Y has locked object B and is trying to lock object A.

This situation is commonly referred to as a deadly embrace. There are three approaches for dealing with this situation, all of which should be routinely employed.

+   - If there is a natural hierarchy to the objects, lock in top-to-bottom order.
+   - Before locking, obtain the extID of all objects that require locking. Sort the extID list with the primary sort using the object hierarchy and the secondary sort using the values of the extID. After the sort, obtain locks in the sort order. This minimizes the likelihood of a deadly embrace.
+   - Always use a timeout on the lock call, and provide exception handling for the timeout scenario.

# Locking and Data Structures

The design of concept data structures can have a significant impact on the complexity of locking. Consider a shipping application in which packages are loaded into containers that are, themselves, loaded onto planes. Two possible data (concept) structures for representing packages, containers, and planes are shown in Figure 14-5. The natural structure is the one that arises from a classical object-oriented modeling approach, and it is the one most people would consider to be representative of the situation.