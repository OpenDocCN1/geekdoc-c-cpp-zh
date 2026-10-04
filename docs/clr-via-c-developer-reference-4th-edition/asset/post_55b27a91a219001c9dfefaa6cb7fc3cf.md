
budget, garbage collector again decides to collect only generation 0, ignoring the unreachable objects in generation 1 (objects B and G). After the collection, the heap looks like Figure 21-9.

| A | B | D | F | G | I | K | N | O |
|---|---|---|---|---|---|---|---|---|
| Generation 1 | | Generation 0 | | | | | | |

**Figure 21-9** After three collections, generation 0 survivors are promoted to generation 1 (growing the size of generation 1 again); generation 0 is empty.

In Figure 21-9, we see that generation 1 is growing slowly. In fact, let's say that generation 1 has grown to the point in which all of the objects in it occupy its full budget. At this point, the application continues running (because a garbage collection finished) and starts allocating objects P through S, which fill generation 0 up to its budget. The heap now looks like Figure 21-10.

| A | B | D | F | G | I | K | N | O | P | Q | R | S |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Generation 1 | | Generation 0 | | | | | | | | | | |

**Figure 21-10** New objects are allocated in generation 0; generation 1 has more garbage.

When the application attempts to allocate object T, generation 0 is full, and a garbage collection must start. This time, however, the garbage collector sees that the objects in generation 1 are occupying so much memory that generation 1's budget has been reached. After several generation 0 collections, it's likely that a number of objects in generation 1 have become unreachable (as in our example). So this time, the garbage collector decides to examine all of the objects in generation 1 and generation 0. After both generations have been collected, the heap now looks like Figure 21-11.

| D | F | I | N | O | Q | S |
|---|---|---|---|---|---|---|
| Generation 2 | Generation 1 | | Generation 0 | | | |

**Figure 21-11** After four collections: generation 1 survivors are promoted to generation 2, generation 0 survivors are promoted to generation 1, and generation 0 is empty.

As before, any objects that were in generation 0 that survived the collection are now in generation 1; any objects that generation 0 is empty immediately after a garbage collection and is where new objects will be allocated. Objects in generation 2 are objects that the garbage collector has examined two or more times. There might have been several collections, but the objects in generation 1 are examined only when generation 1 reaches its budget, which usually requires several garbage collections of generation 0.

The managed heap counts only three generations: generation 0, generation 1, and generation 2; there is no generation 3. When the CLR initializes, it selects budgets for all generations. However, the CLR's garbage collector is a self-tuning collector. This means that the garbage collector learns about your application's behavior whenever it performs a garbage collection. For example, if your application constructs a lot of objects and uses them for a short period of time, it's possible that garbage collection generation 0 will reclaim most of memory. In fact, it's possible the memory for all objects in generation 0 can be reclaimed.

If the garbage collector sees that there are very few surviving objects after collection generation 0, it might decide to reduce the budget of generation 0. This reduction in the allocated space will mean that garbage collections occur more frequently but will require less work for the garbage collector, so your process's working set will be small. In fact, if all objects in generation 0 are garbage the collector does not have to compact any; it can simply set NextObj back to the beginning of generation 0, and then the garbage collector is performed. This is a fast way to reclaim memory!

> Note: The garbage collector works well for threads that idle at the top of their stack most of the time. Then, when the thread has something to do, it wakes up, creates a bunch of short-lived objects, returns, and then goes back to sleep. Many applications follow this architecture. For example, GUI applications use the GUI thread sitting in a message loop of its life. Occasionally, the user generates some input (like a touch, mouse, or keyboard event), the thread wakes up, processes the input and returns back to the message pump. Objects created by this process are probably garbage.

Similarly, server applications tend to have pool threads sitting in the pool waiting for client requests to come in. When a client request comes in, new objects are created to perform work on behalf of the client request. When the result is sent back to the client, the thread returns to the thread pool and all the objects created are garbage now.

On the other hand, if the garbage collector collects generation 0 and sees that there are a lot of objects, not a lot of memory was reclaimed in the garbage collection. In this case, the garbage collector will grow generation 0's budget. By the way, fewer collections will occur, when they do, a lot more memory should be reclaimed. By the way, if insufficient memory has been reclaimed after a collection, the garbage collector will perform a full collection before throwing an OutOfMemoryException.

Throughout this discussion, I've been talking about how the garbage collector dynamically modifies generation 0's budget after every collection. But the garbage collector also modifies the budgets of generation 1 and generation 2 by using similar heuristics. When these generations are garbage collected, the collector again sees how much memory is reclaimed and how many objects survived. Based on the garbage collector's findings, it might grow or shrink the thresholds of these generations

![](img/0ce3b788d061e3d3095fa554b1a34adf_542_0.png)

## Garbage Collection Triggers

As you know, the CLR triggers a GC when it detects generation 0 has filled. This is the most common trigger; however, there are additional triggers as listed:

- Code explicitly calls System.GC Collect Method can explicitly request that the CLR perform a collection. Although Microsoft strongly discourages such requests, at times it might make sense to allow an application to force a collection. I discuss this in the "Forcing Garbage Collections" section later in this chapter.
- Windows is reporting low memory: The CLR internally uses the Win32 MemoryResourceNotification and QueryMemoryNotification functions to monitor memory. If Windows reports low memory, the CLR will force a garbage collection in an effort to free up objects to reduce the size of a working set.
- The CLR is unloading an AppDomain: When an AppDomain unloads, the CLR considers nothing in the AppDomain to be a root, and a garbage collection of all generations is performed. I'll discuss AppDomains in Chapter 22, "CLR Hosting and AppDomains."
- The CLR is shutting down: The CLR shuts down when a process terminates normally (as opposed to an external shutdown via Task Manager, for example). During this shutdown, the CLR considers objects in the process to be a root; it allows objects a chance to clean up the CLR does not attempt to compact or free memory while the process is terminating, and Windows will reclaim all of the processes.

## Large Objects

There is one more performance improvement you might want to be aware of. The CLR considers each single object to be either a small object or a large object. So far, in this chapter, I've been focusing on small objects. Today, a large object is 85,000 bytes or more in size. The CLR treats large objects slightly differently than how it treats small objects:

- Large objects are not allocated within the same address space as small objects; they are located elsewhere within the process address space.
- Today, the GC doesn't compact large objects because of the time it would require to move them in memory. For this reason, address space fragmentation can occur between large objects within the process. In a future version of the CLR, large objects may participate in compaction.

> 4 In the future, the CLR could change the number of bytes required to consider an object to be a large object. Do not count 85,000 being a constant.
