
# Case 1: Request Lost

| Client | Server |
| --- | --- |
| [send request] -> X | (no mesg) |

# Case 2: Server Down

| Client | Server |
| --- | --- |
| [send request] -> X | (down) |

# Case 3: Reply lost on way back from Server

| Client | Server |
| --- | --- |
| [send request] | [recv request] [handle request] [send reply] <- X

Figure 49.6: The Three Types Of Loss

In this way, the client can handle all timeouts in a unified way. If a WRITE request was simply lost (Case 1 above), the client will retry it, the server will perform the write, and all will be well. The same will happen if the server happened to be down when the request was sent, but back up and running when the second request is sent, and all works as desired (Case 2). Finally, the server may receive the WRITE request, issue the write to its disk, and send a reply. This reply may get lost (Case 3), again causing the client to re-send the request. When the server receives the request again, it will simply do the exact same thing; write the data to its disk and that has no done. If the client receives the reply, all is again well, and the client has handled both message loss and server failure in a uniform manner. Neat!

A small aside: some operations are made idempotent. For example, when you try to make a directory that already exists, you are informed that the mkdir request has failed. Thus, in NFS, if the server receives a MKDIR protocol message and executes successfully but the reply is lost, the client may repeat it and encounter that failure when in fact the operation at first succeeded and then only failed on the retry. Thus, life is not perfect.

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

# SUN’s Network File System (NFS)

| C1 | C2 | C3 |
|---|---|---|
| cache: [Fv1] | cache: [Fv2] | cache: empty |

| Server S |
| disk: [Fv1] at first | [Fv2] eventually |

Figure 49.7: The Cache Consistency Problem

(version, 2), and the old version [Fv1] so we can keep the two distinct (but of course the file has the same name, just different contents). Finally, there is a third client, C3, which has not accessed the file F.

You can probably see the problem is using (Figure 49.7). In fact, there are two subproblems. The first subproblem is that the client C2 may write in its cache for a time before propagating them to the server; in this case, while [Fv2] sits in its memory, any access of F from another client (say C3) will fetch the old version of the file [Fv1]). Thus, by buffering writes to the client, other clients get stale versions of the file, which may be undesirable; indeed, imagine the case you log into cache C2, update F and then log into C3.

The second subproblem is that the client C2 may write in its cache for a time before propagating them to the server; in this case, while [Fv2] sits in its memory, any access of F from another client (say C3) will fetch the old version of the file [Fv1]). Thus, by buffering writes to the client, other clients get stale versions of the file, which may be undesirable; indeed, imagine the case you log into cache C2, update F and then log into C3.

# SUN’s Network File System (NFS)

go to the server and retrieve the latest version. If, on the other hand, the client sees that it has the latest version, it will go ahead and use the cached, increasing performance.

When the original team at Sun implemented this, they realized a new problem; suddenly, the NFS server was flooded with GETATTR requests. A client thus bumbers “has anyone changed this file?” when most of the time no one had.

To remedy this situation, **attribute cache** was added to each client. A client would still validate the cache before accessing it, but most would look [in] the cache to fetch the attributes. The attributes for a particular file were placed in the cache when the file was first accessed, and would timeout after a certain amount of time (say 3 seconds). During, those three seconds, all file accesses would determine that it was OK to use the cached file and do so with no network communication with the server.

# SUN’s Network File System (NFS)

go to the server and retrieve the latest version. If, on the other hand, the client sees that it has the latest version, it will go ahead and use the cached, increasing performance.

When the original team at Sun implemented this, they realized a new problem; suddenly, the NFS server was flooded with GETATTR requests. A client thus bumbers “has anyone changed this file?” when most of the time no one had.

To remedy this situation, **attribute cache** was added to each client. A client would still validate the cache before accessing it, but most would look [in] the cache to fetch the attributes. The attributes for a particular file were placed in the cache when the file was first accessed, and would timeout after a certain amount of time (say 3 seconds). During, those three seconds, all file accesses would determine that it was OK to use the cached file and do so with no network communication with the server.

# 49.10 Assessing NFS Cache Consistency

A few words about NFS cache consistency. The flush-on-close behavior was added to “make sense”, but introduced a certain performance problem. Specifically, if a temporary or short-lived file was created on the client and then deleted, it would still be forced to the server. A mere ideal implementation might keep short-lived files in memory until they are deleted and remove the server interaction entirely, perhaps increasing performance.

More importantly, the addition of an attribute cache into NFS made it very hard to understand or reason about exactly what version of a file one was getting. Sometimes you get the latest version; sometimes you would get an old version simply because your attribute cache hadn't yet timed out and the client was happy to give you what was in client memory. This was fine most of the time, and it (and still does!) occasionally led to odd behavior.

And we have described the oddity that client caching. It serves as an interesting example where details of an implementation serve to define user-observable semantics, instead of the other round.

# 49.11 Implications on Server-Side Write Buffering

Our focus has so far been on client caching, and that is where most of the interesting issues arise. However, NFS servers tend to be well-equipped machines with a lot of memory too, and they have caching
