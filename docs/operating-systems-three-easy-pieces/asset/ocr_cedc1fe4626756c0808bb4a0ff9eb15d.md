# SUN’S NETWORK FILE SYSTEM (NFS)

> TIP: PERFECT IS THE ENEMY OF THE GOOD (VOLTAIRE’S LAW)
Even when you design a beautiful system, sometimes the corner cases don't work out exactly as you might like. Take the mkdir example above; one could mkdir to have different semantics, making it idempotent (think about how much you might do so); however, why bother? The NFS design philosophy covers most the important cases, and overall makes the system design clean and simple with regards to failure. Thus, accepting that life isn't perfect and still building the system is a sign of good engineering. Apparently, this wisdom is attributed to Voltaire, saying “a wise Italian says that the best is the enemy of the good” [V2], and then we call it Voltaire’s Law.

# 49.8 Improving Performance: Client-side Caching

Distributed file systems are good for a number of reasons, but sending all read and write requests across the network can lead to a big problem: the network isn't fast, as fast as local memory or disk. Thus, another problem: how can we improve the performance of a distributed file system?

The answer, as you might guess from reading the big words in the sub-heading above, is client-side caching. The NFS client-side file system caches data (and metadata) that it has from server in client memory. Thus, while the first access is expensive (ie., it requires network communication), subsequent accesses are served quickly out of client memory.

The cache also serves as a temporary buffer for writes. When a client application writes to a file, the client buffers the data in client memory (in the same cache as it reads from the file server) before writing the data out to the server. Such buffering is useful because it decouples write latency from actual write performance, i.e., the application's call to write succeeds immediately (and just puts the data in the client-side file system's cache); only later does the data get written to the file server.

NFS, clients cache data and performance is usually great and we are done, right? Unfortunately, not quite. Adding caching into any sort of system with multiple client caches introduces a big and interesting challenge which we will refer to as the cache consistency problem.

# 49.9 The Cache Consistency Problem

The cache consistency problem is best illustrated with two clients and a single server. Imagine client C1 reads a file F, and keeps a copy of the file in its local cache. Now a different client, C2, overwrites the file F, thus changing its contents; let's call the new version of the file F