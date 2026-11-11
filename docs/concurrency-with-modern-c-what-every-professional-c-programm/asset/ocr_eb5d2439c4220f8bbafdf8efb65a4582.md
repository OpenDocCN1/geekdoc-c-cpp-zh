# 15.1.0.5.1 Tagged state reference

You can use the address's low bits to add a tag to each node indicating how often the node has been successfully modified. The result is that compare and swap (CAS) member function eventually fails, although the check returns true. This idea does not solve the issue because the tag bits may eventually wrap around. Architectures that support a double word CAS operation can have a bigger counter.

Tagged state reference are typical used in transactional memory.

The following three techniques are based on the idea of deferred reclamation.

# 15.1.0.5.2 Garbage Collection

Garbage collection guarantees that the variables are only deleted if it is not needed anymore. This sounds promising but has a significant drawback. Most garbage collectors are not lock-free. Therefore, even if you have a lock-free data structure, the overall system won't be lock-free.

# 15.1.0.5.3 Hazard Pointers

From Wikipedia: Hazard Pointers:

Each thread keeps a list of hazard pointers in a hazard-pointer system, indicating which nodes the thread is currently accessing. (In many systems, this "list" may be possibly limited to only one or two elements.) Nodes on the hazard pointer list must not be modified or deallocated by any other thread. (...) When a thread wishes to remove a node, it places it on a list of nodes "to be freed later", but does not deallocate the node's memory until no other thread's hazard list contains the pointer. A dedicated garbage-collection thread can do this manual garbage collection (if the list "to be freed later" is shared by all the threads); alternatively, cleaning up the "to be freed" list can be done by each worker thread as part of an operation such as "pop".

# 15.1.0.6 RCU

RCU stands for Read Copy Update and is a synchronization technique for almost read-only data structures. RCU was created by Paul McKenney and has been used in the Linux Kernel since 2002.

The idea is quite simple and follows the acronym. To modify data, you make a copy of the data and modify that copy. In contrast, all readers work with the original data. If there is no reader, you can safely replace the data structure with its copy.

For more details about RCU, read the article What is RCU, Fundamentally?²³ by Paul McKenney.

![](bbox=[0.12, 0.73, 0.21, 0.77])

# Two new proposals

As part of a concurrency toolkit, there are two proposals for future C++ standards: the proposal P0233r0¹ for hazard pointers and the proposal P0461R0² for RCU.