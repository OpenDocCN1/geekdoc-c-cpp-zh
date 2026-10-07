# CRASH CONSISTENCY: FSCK AND JOURNALING

the file, Da), and all three other direct pointers are set to null (indicating that they are not used). Of course, real inodes have many more fields; see previous chapters for more information.

When we append to the file, we are adding a new data block to it, and thus must update three-disk structures: the inode (which must point to the new block and record the new larger size due to the append), the new data block Db, and a new version of the data bitmap (call it B[v2]) to indicate that the new data block has been allocated.

Thus, in the memory of the system, we have three blocks which must write to the disk. The updated inode (inode version 2, or I[v2] for short) now looks like:

```
owner           : remzi
permissions     : read-write
size            : 2
pointer         : 4
pointer         : 5
pointer         : null
pointer         : null
```

The updated bitmap (B[v2]) now looks like this: 0000110. Finally, there is the data block (Db), which is just filled with whatever it users puts into files. Stolen music permits?

What we would like is for the final on-disk image of the file system to look like:

| Bitmaps | Inodes | Data Blocks |
| --- | --- | --- |
| Inode Data | Iv2 | Da Db |
| 0 1 2 3 4 5 6 7 | 0 1 2 3 4 5 6 7 |

To achieve this transition, the file system must perform three separate writes to the disk, one for the inode (I[v2]), bitmap (B[v2]), and data block (Db). Note that these writes usually don't happen immediately when the user issues a write() system call; rather, the dirty inode, or buffer cache, and new data will sit in main memory first time; then, when the file system finally decides to write them (after 5 seconds or 30 seconds), the file system will issue the requisite requests to the disk. Unfortunately, a crash may occur and interfere with these updates to the disk. In particular, if a crash happens after one or two of these writes have been taken, but not all, the file system could be left in a funny state.

# Crash Scenarios

To understand the problem, let's look at some example crash scenarios. Imagine only a single write succeeds; there are three possible outcomes, which we list here: