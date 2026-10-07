
- Just the data block (Db) is written to disk. In this case, the data is on disk, but there is no inode that points to it and no bitmap that says the block is allocated. Thus, it is as if the write never occurred. This case is not a problem at all, from the perspective of file-system crash consistency¹.

- Just the updated inode (Il(v2)) is written to disk. In this case, the inode points to the disk address (5) where Db was about to be written, but Db has not yet been written there. Thus, if we trust our pointer, we will read garbage data from the disk (the contents of disk address 5).

Further, we have a new problem, which we call a file-system consistency issue. The on-disk bitmap telling us that data block 5 has not been allocated, but the inode is saying that it has. The disagreement between the bitmap and the inode is an inconsistency in the data structures of the file system; to use the file system, we must somehow resolve this problem (more on that below).

- Just the updated bitmap (Bv2)) is written to disk. In this case, the bitmap indicates that block 5 is allocated, but there is no inode that points to it. The file system is inconsistent again; if left unresolved, this would result in a space leak, as block 5 would never be used by the file system.

There are also three crash scenarios in this attempt to write three blocks to disk. In two succeed and the last one fails:

- The inode (Il(v2)) and bitmap (Bv2)) are written to disk, but not data (Db). In this case, the file system metadata is completely consistent: the inode has pointer to block 5, the bitmap indicates that 5 is in use, and thus everything OK from the perspective of the file system's metadata. There is one problem: 5 has garbage in it.

- The inode (Il(v2)) and the data block (Db) are written, but not the bitmap (Bv2). In this case, we have the inode pointing to the correct data on disk, but again have an inconsistency between the inode and the old version of the bitmap (B1). Thus, then we again need to resolve the problem before using the file system.

- The bitmap (Bv2) and data block (Db) are written, but not the inode (Il(v2)). In this case, we again have an inconsistency between the inode and the bitmap. However, even though the block was written and the bitmap indicates its usage, we have no idea which file it belongs to, as no inode points to it.

> ¹However, it might be a problem for the user, who just lost some data!

## CRASH CONSISTENCY: FSCK AND JOURNALING

## The Crash Consistency Problem

Hopefully, from these crash scenarios, you can see the problems that can occur on our on-disk file system image because of crashes: we can have inconsistency in file system data structures; we have space leaks; we can return garbage data to a user; and so forth. What we like to do is ideally keep the file system from one consistent state (e.g., before the file appended) to another atomically (e.g., after the inode, bitmap, and new data block have been written to disk). Unfortunately, we can't do this reliably because the disk only commits one write at a time, and crashes or power loss may occur between these updates. We call this general problem the crash-consistency problem (we could also call it the consistent-update problem).

## 42.2 Solution #1: The File System Checker

Early file systems use a simple approach to crash consistency. Basically, they decided to let inconsistencies happen and then fix them later (rebooting). An example of this lazy approach is found in a tool that does: *fck*. fck is a UNIX tool for finding inconsistencies and repairing them [MK86]; similar tools to check and repair a disk partition exist on different systems. Not that such an approach can't fix all problems, like where the inode points to garbage data. The only goal is to make the file system metadata internally consistent.

The tool *fck* operates in a number of phases, as summarized in Mkusik and Kowalski [MK96]. It runs before *fck* assumes that no other file system activity is on-going (while it runs); once finished, the on-disk file system should be consistent and fully accessible to users.

Here is a basic summary of what *fck* does:

- **Superblock**: *fck* first checks if the superblock looks reasonable, mostly doing sanity checks such as making sure the file system size is greater than the number of blocks that have been allocated. Usually all of these sanity checks is to find a suspect (corrupt) superblock; in this case, the system (or administrator) may decide to use an alternate copy of the superblock.
- **Free blocks**: Next, scans the inodes, indirect blocks, double indirect blocks, etc., to build an understanding of which blocks are currently allocated within the file system. It uses this knowledge to perform a correct version of the allocation bitmaps; thus, if there is any inconsistency between bitmaps and inodes, it is resolved by trusting the information within inodes. The same type of check is performed for all the inodes, making sure that all inodes look like they are used as much in the inode bitmaps.

> ²Pronounced either "eff-ess-check-kay", "eff-ess-check", or, if you don't like the tool, "eff-s". Yes, serious professional people use this term.

© 2008–19, ARPACI-DUSSEAU

THREE
EASY
PIECES

## CRASH CONSISTENCY: FSCK AND JOURNALING

- **Inode state**: In journaling, each inode is checked for corruption. For example, journaling makes that each inode has a valid field.
- **Inode links**: In journaling, each inode has a link count.
- **Duplicates**: In journaling, the system checks for duplicate inodes.
- **Bad blocks**: In journaling, each block is checked for bad blocks.

## 42.3 Solution #2: Journaling (or Write-Ahead Logging)

Probably the most popular solution to the consistent update problem is to steal an idea from the world of database management systems. That ideal, known as write-ahead logging, was invented to address exactly this type of problem. In file systems, we usually call write-ahead journaling for historical reasons. The first file systems to do this were JFS, XFS, and Windows NTFS.

The basic idea is as follows: When updating the disk, before writing the structures in place, first write down note (somewhere else on the disk, in a well-known location) describing what you are about to do. Writing this is the "write ahead" part, and we write it to a structure that we organize as a "log"; hence, write-ahead journaling.

By writing the note, you are guaranteeing that if a crash takes during the update (overwrite) of the structures you are updating, you can go back and look at the note and try again; thus, you will know exactly what to fix (and how to fix it) after a crash, instead of having to scan the entire disk. By design, journaling adds a bit of work during updates to reduce the amount of work required during recovery.

We'll describe how Linux ext3, a popular journaling file system, incorporates journaling into the file system. Most of the on-disk structures are divided into block groups, and each block group contains an inode bitmap, data bitmap, inodes, and data blocks. The new key structure is the journal itself, which occupies some small amount of space within the partition or on another device. Thus, an ext2 file system (without journaling) looks like this:

| Super | Group 0 | Group 1 | ... | Group N |

Assuming the journal is placed within the file system image (though sometimes it is on another device, or as a file within the file system), ext3 file system with a journal looks like this:

| Super Journal | Group 0 | Group 1 | ... | Group N |

The real difference is just the presence of the journal, and of course, how it is used.
