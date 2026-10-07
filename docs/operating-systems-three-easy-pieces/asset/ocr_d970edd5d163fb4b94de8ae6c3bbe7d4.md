# EVENT-BASED CONCURRENCY (ADVANCED)

> ASIDE: BLOCKING VS. NON-BLOCKING INTERFACES
Blocking (or synchronous) interfaces do all of their work before returning to the caller; non-blocking (or asynchronous) interfaces begin some work but return immediately, letting whatever needs to be done get in the background.
The usual culprit in blocking is I/O of some kind. For example, if a call must read from disk to complete, it might block, waiting for the I/O request that has been sent to the disk to return.
Non-blocking interfaces can be used in any type of programming (e.g., with threads), but are essential in the event-based approach, as a call that blocks will halt progress.

some of their descriptors are ready for reading, or ready for writing, or have an exceptional condition pending, respectively. The first nfds descriptors are checked in each set, i.e., the descriptors from 0 through nfds-1 in the descriptor sets are examined. On return, select() replaces the given set with subsets of those descriptors that are ready for the requested operation.
select() returns the number of ready descriptors in all the sets.
A couple of points about select(). First, note that it lets you whether descriptors can be read from as written to; the former lets a server determine that a new packet has arrived and is in of processing, whereas the latter lets the server know when it is OK to reply (i.e., the outbound queue is not full).
Second, the timeout argument. One common usage here is to set the timeout to NULL select to block indefinitely, until some descriptor is ready. However, more robust servers will use some kind of timeout; one common technique is to set the timeout to zero, and then use the select() to return immediately.
The poll() system call is quite similar. See its manual page, and Stevens and Rago [SR05],
Either way, these basic primitives give us a way to build a non-blocking event loop, which simply checks for incoming packets, reads from sockets with messages upon them, and replies as needed.

# 33.3 Using select()

To make this concrete, let's examine how to use select() to see which network descriptors have incoming messages upon them. Figure 33.1 shows a simple example.
This code is actually simple to understand. After initialization, the server enters an infinite loop. Inside the loop, it uses FD_ZERO() to clear the set of file descriptors, and then uses FD_SET() to include all of the file descriptors from minFD to maxFD in

© 2008–19, RPACI-DUSSEAU

THREE
EASY
PIECES