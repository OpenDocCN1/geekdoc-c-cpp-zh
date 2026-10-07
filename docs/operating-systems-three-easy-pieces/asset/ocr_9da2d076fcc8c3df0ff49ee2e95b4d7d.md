# CRASH CONSISTENCY: FSCK AND JOURNALING

| TxB | Journal Contents (metadata) | TxE | File System Data |
| --- | --- | --- | --- |
| issue | issue | | complete |
| complete | complete | | |
| | | issue | |
| | | complete | |

Figure 42.2: Metadata Journaling Timeline

that data write can logically be issued at the same time as the writes to the transaction begin and the contents of the journal; however, it must be issued and complete before the transaction end has issued.\ Finally, note that the completion time marked for each in the timelines is arbitrary. In a real system, completion time is determined by the I/O subsystem which may reorder writes to improve performance. The only guarantees about ordering that we have those that must be enforced for proper correctness (and are shown with the horizontal dashed lines in the figures).

# 42.4 Solution #3: Other Approaches

We've described two options in keeping file system metadata consistent: a lazy approach based on *fsck*, and a more active approach known as journaling. However, these are not the only approaches. One approach, as Soft Updates [GP94], was introduced by Ganger and Patti. This approach carefully orders all writes to the file system to ensure that the on-disk structures are never left in an inconsistent state. For example, by writing a pointed-to data block *before* the inode that it points to, we can ensure that the inode never points to garbage; similar rules can be derived for all the structures of the file system. Implementing Soft Updates can be a challenge; however, the journaling described above can be implemented with relatively little knowledge of each file system structure and Soft Updates requires intricate knowledge which adds fair amount complexity. Another approach is known as *copy-on-write* (COW), and is used in a number of popular file systems, using Sun's ZFS [B07]. This technique never overwrites files or directories in place; rather places new updates to previously unused locations on disk. After a number of updates are completed, COW systems flip the root structure of the file system to include pointers to the newly updated structures. Doing so makes the file system consistent straightforward. We'll learn-

2008–19, ARPACI-DUSSE

THREE EASY PIECES

*Next*