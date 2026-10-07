
# THE ANDREW FILE SYSTEM (AFS)

file, i.e., the file that remains on the server for others to see. The result is a file that was generated in its entirety either by one client or the other. Note the difference from a block-based protocol like NFS: in NFS, writes of individual blocks are flushed out to the server as each client is updating the file, and thus the final file on the server could end up as a mix of updates from both. In many cases, a mixed file output would not make sense, i.e., imagine a JPEG image modified by two clients in pieces; the resulting of writes would not likely constitute a JPEG.

A timeline showing a few of these different scenarios can be seen in Figure 50.3. The columns show the behavior of two processes (P1 and P2) on their cache state, one process (P3) on Client2 and its cache state, all operating on a single file called imaginatively. For the server, the figure simply shows the contents of the file after the operation on the left has completed. Read through it and if you can understand why each reads the results that it does. A commentary on the right will help you get stuck.

## 50.6 Crash Recovery

From the description above, you might sense that crash recovery is more involved than with NFS. You would be right. For example, there is a period of time when a server (S) is not able to contact a client (C1), while the client (C1) is rebooting. While C1 is not available, S might have tried to send it or more callback messages; for example, imagine C1 had file F cached on its local disk, and C2 (another client) updated F, causing S to send messages to all clients caching the file to remove it from their caches. C1 might miss these critical messages when it is rebooting, upon joining the system, C1 should treat all of its cache contents as suspect. Thus, upon the next access to file, C1 should first ask the server (with a TestAuth protocol) whether its cache copy of file F is still valid; if so, C1 can use it; if not, C1 could fetch the newer version from the server.

Server recovery after a crash is also more complicated. The problem is that all crashes are kept in memory; thus, when a server boots, it has no idea which client has files. Thus, upon server restart, each client must realize that the server crashed and treat all of their cache contents as suspect, and (as above) reestablish validity of a file before using it. Thus, a crash is a big event, one must ensure that each client is aware of the crash in a timely manner, or risk losing files. There are many ways to implement recovery; for example, having the server send a message (“don’t trust your cache contents!” to each client when it is up and running again, or by having clients check that the server is alive periodically (with a heartbeat message, as it is called). As you can see, there is a cost to building a more scalable and sensible caching model; with NFS, clients hardly noticed a crash.

| Workload | NFS | AFS | AFS |
|---|---|---|---|
| 1. Small file, sequential read | $N_s \cdot L_{net}$ | $N_s \cdot L_{net}$ | 1 |
| 2. Small file, sequential re-read | $N_s \cdot L_{mem}$ | $N_s \cdot L_{mem}$ | 1 |
| 3. Medium file, sequential read | $N_m \cdot L_{net}$ | $N_m \cdot L_{net}$ | 1 |
| 4. Medium file, sequential re-read | $N_m \cdot L_{mem}$ | $N_m \cdot L_{mem}$ | 1 |
| 5. Large file, sequential read | $N_L \cdot L_{net}$ | $N_L \cdot L_{net}$ | 1 |
| 6. Large file, sequential re-read | $N_L \cdot L_{disk}$ | $N_L \cdot L_{disk}$ | $L_{disk}$ |
| 7. Large file, single read | $L_{net}$ | $L_{net}$ | $N_L$ |
| 8. Small file, sequential write | $N_s \cdot L_{net}$ | $N_s \cdot L_{net}$ | 1 |
| 9. Large file, sequential write | $N_L \cdot L_{net}$ | $N_L \cdot L_{net}$ | 1 |
| 10. Large file, sequential overwrite | $N_L \cdot L_{net}$ | $2 \cdot L_{net}$ | 2 |
| 11. Large file, single write | $L_{net}$ | $2 \cdot L_{net}$ | $2 \cdot N_L$ |

Figure 50.4: Comparison: AFSv2 vs. NFS

## 50.7 Scale And Performance Of AFSv2

With the new protocol in place, AFSv2 was measured and found to be much more scalable than the original version. Indeed, each server could support about 50 clients (instead of 20). A further benefit was that client-side performance often came quite to local performance, because in the same case, all file accesses went to the local disk cache (and, potential local memory). Only when a local client created a new file or wrote to an existing one there was a need to send a message to the server and then update the file with new contents.

We also gain some perspective on NFS performance by comparing common file-system access scenarios with NFS. Figure 50.4 (page 675) shows the results of our qualitative comparison.

In the experiment, we assume typical read and write patterns analytically, for files of different sizes. Small files have $N_s$ blocks in memory; medium files have $N_m$ blocks; we assume that medium and large files fit into the memory of a client; large files fit on a local disk but not in memory.

We also, for the sake of analysis, an access across the network to the file block takes $L_{net}$ time units. Access to local memory takes $L_{mem}$, and access to local disk takes $L_{disk}$. The general assumption is $L_{net} > L_{disk} > L_{mem}$.

Finally, we assume that the first access to a file does not hit in its caches. Subsequent accesses (i.e., "re-reads") we will hit in caches, if the relevant cache has enough capacity to hold the file.

The columns of the figure show the time a a particular operation (e.g., a sequential read) takes. The right-most column displays the ratio of AFS to NFS. We make the following observations. First, in many cases, AFS is similar to NFS. You might think AFS would be slower, because it writes to disk. However, realize that it is writing to a local file system; those writes are first committed to the page cache, and only later (in the background) to disk, and AFS reaps the benefits of the client-side OS infrastructure to improve performance.

Second, an interesting difference arises during a large-file re-read (Workload 6). Because AFS has a local disk cache, it will access local disk. NFS, in contrast, can only cache in client memory; thus it will need to fetch the entire file from the remote server.

Third, note that sequential writes (of new files) perform similarly on both systems (8,9). AFS, in this case, will write to the local cache when the file is closed; you might think AFS would be slower, because it writes all data to disk. However, NFS will buffer writes in memory, before forcing some blocks to the server to client-side memory pressure, but definitely writing them to the server when the file is closed, to preserve flush-on-consistency.

Fourth, note that AFS performs worse on a sequential overwrite (Workload 10). Thus far, we have assumed that the wo are creating a new file; in this case, the file exists, and is overwritten. Overwriting is a particularly bad case for AFS, because the client fetches the old file in its entirety; to subsequently overwrite it. NFS, in contrast, will simply overwrite blocks and avoid the initial (useless) read.

Finally, workloads that access a small subset of data within large files perform much better than NFS (Workloads 7, 11). In these cases, the AFS protocol fetches the entire file when the file is opened; unfortunately, only a small read or write is performed. Even worse, if the file is modified, the entire file is written back to the server, doubling the per-operation cost. Thus, AFS is faster than NFS in this case by a factor of local disk.
