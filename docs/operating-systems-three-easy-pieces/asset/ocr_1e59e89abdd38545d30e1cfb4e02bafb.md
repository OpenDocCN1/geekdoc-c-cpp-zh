# CRASH CONSISTENCY: FSCK AND JOURNALING

journaling), and it is nearly the same, except that user data is not written to the journal. Thus, when performing the same update as above, the following information would be written to the journal:

| Journal | TxB | I[v2] | B[v2] | TxE |
| --- | --- | --- | --- | --- |

The data block Db, previously written to the log, would instead be written to the file system, avoiding the extra write; given that most I/O traffic to the disk is data, not writing twice substantially reduces the I/O load of journaling. The modification does raise an interesting question, though: when should we write data blocks to disk?

Let's again consider our example of a to understand the problem better. The update consists of three blocks: I[v2], B[v2], and Db. The first two are metadata and will be logged and check-pointed; the latter will only be written to the file system. When should we write Db to disk? Does it matter?

As turns out, the ordering of the data write matters for journaling. For example, if we write Db to disk after the action(containing I[v2] and B[v2]) completes? Unfortunately, this approach has: the file system is consistent but I[v2] may end up pointing to garbage data. Specifically, consider the case where I[v2] and B[v2] are written but Db did not. The file system will then try to recover. Because Db is not in the log, the file system will then writes to I[v2] and B[v2], and produce a consistent file system (from the perspective of file-metadata). However, I[v2] will be pointing to garbage data, i.e., whatever was on the disk that Db was headed.

To ensure this does not arise, some file systems (e.g., Linux ext3) write data blocks (of regular files) to the first disk, before related metadata is written to disk. Specifically, the protocol is as follows:

+   1. **Data write**: Write data to final location; wait for completion (the wait is optional; see below for details)
2. **Journal metadata write**: Write the begin block and metadata to the log; wait for write to complete.
3. **Journal commit**: Write the transaction commit to the log; wait for the write to complete; the transaction (including data) is now committed.
4. **Checkpoint metadata**: Write the contents of the metadata update to their final locations within the file system.
5. **Free**: Later, mark the transaction in journal superblock.

By forcing the data write first, a file system can never point to garbage. Indeed, this rule of "write the pointed-to object before that points to it" is at the core of crash consistency, and is eventually followed by other crash consistency schemes [GP94] (see below for details).

OPERATING SYSTEMS
[Version 1.01]

WWW.OSTEP.ORG