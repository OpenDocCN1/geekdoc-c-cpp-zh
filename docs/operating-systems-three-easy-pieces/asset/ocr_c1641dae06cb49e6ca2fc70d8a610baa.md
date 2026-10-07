# THE ANDREW FILE SYSTEM (AFS)

file, i.e., the file that remains on the server for others to see. The result is a file that was generated in its entirety either by one client or the other. Note the difference from a block-based protocol like NFS: in NFS, writes of individual blocks are flushed out to the server as each client is updating the file, and thus the final file on the server could end up as a mix of updates from both. In many cases, a mixed file output would not make sense, i.e., imagine a JPEG image modified by two clients in pieces; the resulting of writes would not likely constitute a JPEG.

A timeline showing a few of these different scenarios can be seen in Figure 50.3. The columns show the behavior of two processes (P1 and P2) on their cache state, one process (P3) on Client2 and its cache state, all operating on a single file called imaginatively. For the server, the figure simply shows the contents of the file after the operation on the left has completed. Read through it and if you can understand why each reads the results that it does. A commentary on the right will help you get stuck.

# 50.6 Crash Recovery

From the description above, you might sense that crash recovery is more involved than with NFS. You would be right. For example, there is a period of time when a server (S) is not able to contact a client (C1), while the client (C1) is rebooting. While C1 is not available, S might have tried to send it or more callback messages; for example, imagine C1 had file F cached on its local disk, and C2 (another client) updated F, causing S to send messages to all clients caching the file to remove it from their caches. C1 might miss these critical messages when it is rebooting, upon joining the system, C1 should treat all of its cache contents as suspect. Thus, upon the next access to file, C1 should first ask the server (with a TestAuth protocol) whether its cache copy of file F is still valid; if so, C1 can use it; if not, C1 could fetch the newer version from the server.

Server recovery after a crash is also more complicated. The problem is that all crashes are kept in memory; thus, when a server boots, it has no idea which client has files. Thus, upon server restart, each client must realize that the server crashed and treat all of their cache contents as suspect, and (as above) reestablish validity of a file before using it. Thus, a crash is a big event, one must ensure that each client is aware of the crash in a timely manner, or risk losing files. There are many ways to implement recovery; for example, having the server send a message (“don’t trust your cache contents!” to each client when it is up and running again, or by having clients check that the server is alive periodically (with a heartbeat message, as it is called). As you can see, there is a cost to building a more scalable and sensible caching model; with NFS, clients hardly noticed a crash.

OPERATING SYSTEMS
[VERSION 1.01]

WWW.OSTEP.ORG