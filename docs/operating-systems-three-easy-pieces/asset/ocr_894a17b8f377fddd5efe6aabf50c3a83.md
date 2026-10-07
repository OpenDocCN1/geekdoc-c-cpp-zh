# CRASH CONSISTENCY: FSCK AND JOURNALING

mencing a search-the-entire-house-for-keys recovery algorithm, starting in the basement and working your way through every room. It works but is wasteful. Thus, disks (and RAIDs) grew, researchers and practitioners started to look for other solutions.

# 42.3 Solution #2: Journaling (or Write-Ahead Logging)

Probably the most popular solution to the consistent update problem is to steal an idea from the world of database management systems. That ideal, known as write-ahead logging, was invented to address exactly this type of problem. In file systems, we usually call write-ahead journaling for historical reasons. The first file system to do this was Cedar ext3 and ext4, reisers, IBM's JFS, SCI's XFS, and Windows NTFS.

The basic idea is as follows. When updating the disk, before writing the structures in place, first write down little note (somewhere else on the disk, in a well-known location) describing what you are about to do. Writing this is the “write ahead” part, and we write it to a structure that we organize as a “log”; hence, write-ahead journaling.

By writing the note, you are guaranteeing that if a crash takes during the update (overwrite) of the structures you are updating, you can go back and look at the note and try again; thus, you will know exactly what to fix (and how to fix it) after a crash, instead of having to scan the entire disk. By design, journaling adds a bit of work during updates to reduce the amount of work required during recovery.

We'll describe how Linux ext3, a popular journaling file system, incorporates journaling into the file system. Most of the on-disk structures are divided into block groups, and each block group contains an inode bitmap, data bitmap, inodes, and data blocks. The new key structure is the journal itself, which occupies some small amount of space within the partition or on another device. Thus, an ext2 file system (without journaling) looks like this:

| Super | Group 0 | Group 1 | ... | Group N |

Assuming the journal is placed within the file system image (though sometimes it is on a separate device, or as a file within the file system), ext3 file system with a journal looks like this:

| Super Journal | Group 0 | Group 1 | ... | Group N |

The real difference is just the presence of the journal, and of course, how it is used.

© 2008–19, ARPACI-DUSSEAU

THREE
EASY
PIECES