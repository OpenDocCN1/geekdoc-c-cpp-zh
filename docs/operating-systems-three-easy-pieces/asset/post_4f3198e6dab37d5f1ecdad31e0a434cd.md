
# Data Journaling

Let's look at a simple example to understand how data journaling works. Data journaling is available as a mode with the Linux ext3 file system, from which much of this discussion is based.

Say we have a canonical update again, where we wish to write the inode I[v2], bitmap B[v2], and data block (Db) to disk again. Before writing them to their final disk locations, we are now first going to write them to the log (a.k.a. journal). This is what this will look like in the log:

![](img/133d518e3f69f4caaead32c569ae6c49_595_0.png)

You can see what we have five blocks. The transaction begin (TxB) tells us about this, including information about the pending update to the file system (e.g., the final addresses of I[v2], B[v2], and Db), and some kind of transaction identifier (TID). The three blocks just contain the contents of the blocks themselves; this is known as physical logging as we are putting the physical contents of the update in the journal (an alternate idea, logical logging puts a more compact logical representation of the update in the journal, e.g., "this update updates to append data block Db to file X", which is a little more but can save space in the log and improves performance). The final block (TxE) is a marker of the end of this transaction, and will also contain the TID.

Once this transaction is safe on disk, we are ready to overwrite the old structures in the file system; this process is called checkpointing. Thus, to checkpoint the file system (i.e., bring it up to date with the pending update in the journal), we issue the writes I[v2], B[v2], and Db to their disk locations as seen above; if these writes complete successfully, we have successfully checkpointed the file system and are basically done. Our sequence of operations:

1. **Journal**: Write the transaction, including a transaction-begin block, all pending data and metadata updates, and a transaction-end block, to the log; wait for these writes to complete.
2. **Checkpoint**: Write the pending metadata and data updates to their final locations in the file system.

In our example, we write TxB, I[v2], Db, and TxE to the journal first. When these writes complete, we would complete the update by checkpointing I[v2], B[v2], and Db, to their disk locations.

Gets a little trickier when a crash occurs during the writes to the journal. Here, we are trying to write the set of blocks in the transaction (e.g., TxB, I[v2], B[v2], Db, TxE) to disk. One simple way to do this would be to issue each one at a time, waiting for each to complete, and issuing the next. However, this is slow. we'd like to issue all five blocks at once, as this would turn five writes into a single sequential write and thus be faster. However, this is unsafe, for the following reason: given such a big write, the disk internally may perform scheduling and complete small pieces of the big write in any order. Thus, the disk may write TxB, I[v2], B[v2], and TxE and only later (2) write Db. Unfortunately, if the disk loses power between (1) and (2), this is what ends up on:

| Journal | TxB | I[v2] | B[v2] | ?? | TxE |
|---|---|---|---|---|---|
| | id=1 | | | | id=1 |

Why is this a problem? The transaction looks like a valid transaction (it has a beginning and end with matching sequence numbers). Furthermore, the system can look at that fourth block and know it is wrong; after all, it is arbitrary user data. Thus, if the system reboots and recovers, it will replay this transaction, and ignorantly copy the contents of the garbage block '??' to the location Db is supposed to live. This is for arbitrary user data in a file; it is much worse if it happens to be a critical piece of file system, such as the superblock, which could render the file system unmountable.

© 2008–19, ARPACI-DUSSE

THREE
EASY
PECES

# CRASH CONSISTENCY: FSCK AND JOURNALING

ASIDE: FORCING WRITES TO DISK

To enforce ordering between two disk writes, modern file systems have to take a few extra precautions. In old times, forcing ordering between two writes, $A$ and $B$, was easy: just issue the write of $A$ to the disk, wait for the disk to interrupt the OS when the write is complete, and then issue the write of $B$.

Things slightly more complex due to the increased use of write caches within disks. With write buffering (sometimes called **immediate reporting**), a disk will inform the OS when write is complete when it simply has been placed in the disk's memory cache, and has not reached disk. If the OS issues a subsequent write, it is not guaranteed to reach the disk after the previous writes; thus ordering between writes is not preserved. One solution is to disable write buffering. However, modern systems take precautions and use **write barriers**; such a barrier, when it completes, guarantees that all writes issued before the barrier will reach disk before any writes issued after the barrier of the disk.

All of this machinery requires a great deal of trust in the correct operation. Unfortunately, recent research shows that some disk manufacturers, in an effort to deliver "higher performing" disks, explicitly ignore write-barrier requests, making the disks seemingly run faster but at the risk of incorrect operation [C+13, R+11]. As Kahan said, the fastest always beats the slow, even if it is fast.

# CRASH CONSISTENCY: FSCK AND JOURNALING

ASIDE: OPTIMIZING LOG WRITES
You might have noticed a particular inefficiency of writing to the log. Namely, the file system first has to write out the transaction-begin block and contents of the transaction; only after these writes complete can the file system send the transaction-end block to disk. The performance impact is, if you think about how a disk works: usually an extra rotation is incurred (think about why)

One of our graduate students, Vijayan Prabhakaran, had a simple idea to fix this problem [P-85]. When writing a transaction to the journal, he includes a checksum of the contents in the journal and begin end blocks. By enabling the file system to write the entire transaction at once, without incurring a wait; if recovery, the file system sees a mismatch in the checksum versus the stored checksum in the transaction, it can conclude that a crash occurred during the write and discard the file-update. Thus, with a small tweak in the write protocol and recovery system, a file system can achieve faster common-case performance; on top of that, the system is significantly more reliable, as any reads from the journal are now protected by a checksum.

This simple fix was attractive to gain the notice of Linux file system developers, who then incorporated it into the next generation Linux file system, called ext4. It now ships on millions of machines worldwide, including the Android handheld platform. Thus, every time you write to disk many Linux-based systems, a little code developed at Wisconsin makes your system a little faster and more reliable.

To avoid this problem, the file system issues the transactional block in two steps. First, it writes all blocks except the TxE block to the journal, issuing these writes all at once. When these writes complete, the journal will look like this (assuming our append workload):

| TxB id=1 | [I[v2]] | B[v2] | Db |

When those writes complete, the file system issues the write of the TxE block, leaving the journal in this final, safe state:

| TxB id=1 | [I[v2]] | B[v2] | Db | TxE id=1 |

An important aspect of this is the atomicity provided by the disk. It guarantees that the write will either happen or not; thus, to make sure the write of TxE is atomic, one should make it a single block. Thus, our current protocol to update the file system, with each of its three phases labeled:

1. **Journal**: Write the transaction, including a transaction-begin block, all pending data and metadata updates, and a transaction-end block, to the log; wait for these writes to complete.
2. **Commit**: Write the transaction commit block (TxE) to the log; wait for write to complete; transaction is said to be committed.
3. **Checkpoint**: Write the contents of the update (metadata and data) to their final locations.

# CRASH CONSISTENCY: FSCK AND JOURNALING

# Recovery

Let's now understand how a file system can use the contents of the journal to *recover* from a crash. A crash may happen at any time during this sequence. If the crash happens before the transaction is written safely to the log (i.e., Step 2 above completes), our job is easy: the pending update is simply skipped. If the crash happens the transaction has been committed to the log, but before the checkpoint is complete, the file system can *recover* the update as follows. When the system boots, the file recovery process will scan the log and look for transactions that have committed to the disk; these transactions are thus replayed (in order), with the file system again attempting to write out the blocks in the transaction to their final locations.

Note that it is fine for a crash to happen at any point during checkpointing, even after some of the updates to the final locations of the blocks have completed. In the worst case, some updates are simply performed during recovery. Because recovery is a rare operation (only taking place after an unexpected crash), a few redundant writes are nothing to worry about.

# Batch Logging Updates

You might have noticed that the basic protocol could add a lot of extra disk traffic: For example, imagine we create two files in a row, called file1 and file2, in the same directory. To create one file, one has to update a number of on-disk structures, minimally including: the inode bitmap (to allocate a new inode), the newly-created inode of the file,
