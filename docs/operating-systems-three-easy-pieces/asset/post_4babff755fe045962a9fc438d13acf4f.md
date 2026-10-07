
# DISTRIBUTED SYSTEMS

For the server, code is also generated. The steps taken on the server are as follows:

- **Unpack the message.** This step, called unmarshaling or deserialization, takes the information of the incoming message. The function identifier and arguments are extracted.
- **Call into the actual function.** Finally! We have reached the point where the remote function is actually executed. The RPC runtime calls into the function specified by the ID and passes in the desired arguments.
- **Package the results.** The return argument(s) are marshaled back in a single reply buffer.
- **Send the reply.** The reply is finally sent to the caller.

There are a few other important to consider in a stub compiler. The first is complex, i.e., how does one package and send a complex data structure? For example, when one calls the `write()` system, one passes in three arguments: an integer file descriptor, a pointer to a buffer, and a size indicating how many bytes (starting at the pointer) to be written. If an RPC package is passed a pointer, it needs to be able to figure out how to interpret that pointer, and perform the correct action. Usually this is achieved through well-known types (e.g., `buffer_t`) that is used to pass chunks of data given a size, which the RPC compiler understands, and by annotating the data structures enabling the compiler to know which bytes need to be serialized.

Another issue is the organization of the server with regards to concurrency. A simple server waits for requests in a simple loop, and handles each request at a time. However, as you might have guessed, this can be grossly inefficient; if one RPC blocks (e.g., on I/O), server resources are wasted. Most servers are constructed in sort of concurrent fashion. A common organization is a thread pool. In this organization, a finite set of threads are created when the server starts; when a message arrives, it is dispatched to one of these worker threads, which then does the work of the RPC call, eventually replying; during this time, a main thread keeps receiving other requests, and dispatches them to other workers. Such an organization enables concurrent execution within the server, thus increasing its utilization; the standard costs arise as well, mostly in programming complexity, as the RPC calls may now need to use locks and other synchronization primitives to ensure their execution correct order.

# Run-Time Library

The run-time library handles much of the heavy lifting in the RPC system; most performance and reliability issues are handled herein. We’ll now discuss some of the major challenges in building a run-time layer.

© 2008–19, ARPAC-DUSSEAU

THREE EASY PIECES

# DISTRIBUTED SYSTEMS

One of the first challenges we must overcome is how to locate a remote service. This problem, of naming, is a common one in distributed systems, and in some sense goes beyond the scope of our current discussion. The simplest of approaches are built on existing naming systems, e.g., hostnames and port numbers provided by current internet protocols. In such a system, the client must know the hostname or IP address of the machine running the RPC service, and the port number it is using (a port number is just a way of identifying a particular communication activity taking place on a machine, allowing multiple communication channels at once). The protocol must provide a mechanism to route packets to a particular address from any machine in the system. For a good discussion of naming, you'll have to look elsewhere, e.g., read about DNS and name ports on the Internet, or better yet read the excellent chapter in Saltzer and Kaashek's book [SK89].

Once a client knows which service it should talk to a remote service, which transport-level protocol should be built upon? Specifically, the RPC system should use a reliable protocol such as TCP/IP, or be built upon an unreliable communication layer as UDP/IP?

Naive would seem easy: clearly we would like a request to be reliably delivered to the remote server, and clearly we would like to reliably receive a reply. Thus we should use the reliable transport protocol such as TCP, right?

UnFortunately, RPC on top of a reliable communication layer can lead to a major inefficiency in performance. Recall from the discussion above communication layers plus timeout/retry. Thus, when the client sends an RPC request to the server, the server responds with an acknowledgment so that the request was received, the client acknowledges so that the server knows it was received. Similarly, when the server sends the reply to the client, the client acknowledges so that the server knows it was received. By building a request/response protocol (such as RPC) on top, two “extra” messages are sent.

For this reason, RPC packages are built on top of unreliable communication layers, as UDP. Doing so enables a more efficient RPC system, but does also the responsibility of providing reliability to the system. The RPC achieves the desired level of reliability by using timeout/retry and acknowledgments much like we described above. By using some form of sequence numbering, the communication layer can guarantee that each RPC takes place exactly once (in the case of no failure), or at once (in the case where failure occurs).

# Other Issues

There are other issues RPC must handle as well. For example, what happens when a remote call takes a long time to complete? Given our timeout machinery, a long-running remote might appear as a failure to a client, triggering a retry, and thus the need for some care here. One solution is to use an explicit acknowledgment

# DISTRIBUTED SYSTEMS

643

Aside: THE END-TO-END ARGUMENT

The end-to-end argument makes the case that the highest level in a system, i.e., usually the application, is ultimately the only locale within a layered system where certain functionality can be properly implemented. In their landmark example: file transfer between two machines [SRC84], Saltzer et al. argue that if you want to transfer a file from machine A to machine B, and make sure that the bytes end up on B are exactly the same as those that began on A, you must have "end-to-end" check of this; lower-level machinery, e.g., in the network or disk, provides no such guarantee.

The contrast is an approach which tries to solve the reliable-file-transfer problem by adding lower layers of the system. For example, we say we build a reliable communication protocol and use it to build our reliable file transfer. The communication protocol guarantees that every byte sent by a sender will be received in order by the receiver, using timeout/retry, acknowledgments, and sequence numbers. Unfortunately, using such a protocol does not guarantee a file transfer maybe the bytes get corrupted in sender memory before the communication takes place, or something bad happens when the receiver writes the data. In those cases, even though the bytes were delivered reliably across the network, our file transfer was ultimately unreliable. To build a reliable file transfer, one must include end-to-end checks of reliability, e.g., after the transfer is complete, read back the file on the receiver side a checksum, and compare checksum to that of the file sender. The corollary to this maxim is that sometimes lower layers provide extra functionality can indeed improve system performance or optimize a system. Thus, you should not rule out having machinery at a lower-level in a system; rather, you should carefully consider the utility of such machinery, its eventual usage in an overall system or application.

(from the receiver to sender) when the reply isn't immediately generated; this lets the client know the server received the request. Then, after some time has passed, the client can periodically ask whether the server is still working on the request; if the server keeps "yes", the client should be happy and continue to wait (after all, sometimes a procedure call can take a long time to finishing execution).

The run-time must also handle procedure calls with large arguments, larger than can fit into a single packet. Some lower-level network protocols provide such sender-side fragmentation (of larger packets into a set of smaller ones) and receiver-side reassembly (of smaller parts into one larger logical whole); if not, the RPC run-time may have to implement such functionality itself. See Birrell and Nelson's paper for details [BN84].
