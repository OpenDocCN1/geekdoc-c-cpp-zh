
Worse, the file system would end up quite fragmented, as the free space was not carefully managed. The free list would end up pointing to a bunch of blocks spread across the disk, and as files allocated, they would simply take the next free block. The result was a logically contiguous file would be accessed by going back and forth across the disk, reducing performance dramatically.

For example, the following data block region, which contains four files (A, B, C, and D), each of size 2 blocks:

| A1 | A2 | B1 | B2 | C1 | C2 | D1 | D2 |

If B and D are deleted, the resulting layout is:

| A1 | A2 | C1 | C2 |

As you can see, the free space is fragmented into two chunks of two blocks, instead of one contiguous chunk of four. Let's say you now wish to allocate file E, of size four blocks:

| A1 | A2 | E1 | E2 | C1 | C2 | E3 | E4 |

You can see that: E spread across the disk, and as a result, accessing E, you don't get peak (sequential) performance from the disk. Rather, you first read E1 and E2, then, seek E3 and E4. This fragmentation problem happened all the time in the UNIX file system, and it hurt. A side note: this problem is exactly what disk defragmentation tools help with; they reorganize disk to place files continuously and make free space for one or a few contiguous regions, moving data around and then rewriting inodes to reflect the changes.

One problem: the original block size was too small (512 bytes). Thus, transferring data from the disk was inherently inefficient. Smaller blocks were good because, they minimized internal fragmentation (waste within the block), but for transfer as each block might require a positioning overhead to it. Thus, the problem:

## THE CRUX: TO ORANIZE ON-DISK DATA TO IMPROVE PERFORMANCE

How can we organize file system data structures to improve performance? What types of allocation policies do we need on top of these data structures? How do we make the file system "disk aware"?

## LOCALITY AND THE FAST FILE SYSTEM

### 41.2 FFS: Disk Awareness Is The Solution

A group at Berkeley decided to build a better, faster file system, which they cleverly called Fast File System (FFS). The idea was to design the file system structures and allocation policies to be "disk aware" and thus improve performance, which is exactly what they did. FFS thus ushered in a new era of file system research; by keeping the same interface to the file system (the same APIs opening(), read(), close(), and other file system calls) but changing the internal implementation, paved the path for new file system construction, which continues today. Virtually all modern file systems adhere to the existing interface (and thus preserve compatibility with applications) while changing their internals for performance, reliability or other reasons.

### 4.3 Organizing Structure: The Cylinder Group

The first step was to change the on-disk into cylinder groups. A single cylinder is a set of tracks on different surfaces of a hard drive that are the same distance from the center of the device; it is called a cylinder because it resembles the so-called geometrical shape. FFS aggregates consecutive cylinders into a group, and thus the entire disk can be viewed as a collection of cylinder groups. Here is a simple example, showing the outer tracks of a drive with platters, and a cylinder group that consists of three cylinders:

![](img/133d518e3f69ccaaead32c69ae576_0.png)

Note that modern drives do not export information for the file system to truly whether a particular cylinder is in use; as discussed previously, thus modern systems (such as Linux ext2, ext3, and ext4) organize the drive into block groups, each of which is just a consecutive portion of the disk's address space. The picture below illustrates an example where blocks are organized into different block group (note that groups would consist of more blocks):

| Group 0 | Group 1 | Group 2 |
| --- | --- | --- |
| | | |

Whether you call cylinder groups or block groups, these groups are the central mechanism that FFS uses to improve performance. Critically, by placing files within the same group, FFS can ensure that accessing one after the other will not result in seeks across the disk.

To use these groups to store files and directories, FFS needs to have the ability to place files and directories into a group, and track all necessary information about them. To do so, FFS includes all the structures you might expect a file system to have within each group, e.g., space for inodes, data blocks, and some structures to track whether each of those are allocated or free. Here is a depiction of what FFS keeps within a single cylinder group:

| ib db | Inodes | Data |
| --- | --- | --- |

Let's now examine the components of this single cylinder group in detail. FFS keeps a copy of the super block (S) in each group for reliability reasons. The super block is needed to mount the file system; by keeping multiple copies, if one becomes corrupt, you can still mount and access the file system using a working replica.

Within each group, FFS needs to track whether the inodes and data blocks of the group are allocated. A per-group inode bitmap (ib) and data bitmap (db) serve this role for inodes and data blocks in each group. Bitmaps are an excellent way to manage free space in a file system because it is easy to find a large chunk of free space and allocate it to a file, avoiding some of the fragmentation problems of the free list in the old file system.

Finally, the inode and data block regions are just like those in the previous very-simple file system (VSFS). Most of each cylinder group, as usual, is comprised of data blocks.

### ASIDE: FFS FILE CREATION

As an example, think about what data structures must be updated when a file is created; assume, for that example, that the user creates a new file /foo/bar.txt and that the file is one block long (4KB). The file is new, and needs a new inode; thus the inode bitmap and the newly-allocated inode must be written to. The file also has a data bitmap and a data block which will (eventually) be written to. Hence, let us four writes to the current cylinder group take place (recall that these writes may be buffered in memory for a while before they take place). But this is not all! In particular, when creating a file, you must also place the file in the file system hierarchy; the directory must be updated. Specifically, the parent directory must be updated to add the entry for bar.txt; this update may fit in an existing data block of foo or a new block to be allocated (with associated data bitmap). The inode of foo must be updated, to reflect the new length of the directory as well as update time fields (such as last-modified time). Overall, it is a lot of work just to create a new file! Perhaps next time you do so, you should be more careful, or at least understand that it works so well.

### 4.4 Policies: How To Allocate Files and Directories

With this group structure in place, FFS has now to decide how to place files and directories and metadata on disk to improve performance. The basic mantra is simple: keep related together (and its correlates, unrelated stuff apart).

Thus, obey the mantra, FFS has to decide what is "related" and place it within the same group; conversely, unrelated items should be placed into different block groups. To achieve this, FFS makes one of a few placement heuristics.

The first is the placement of directories. FFS employs a simple approach: find the cylinder group with a low number of allocated inodes (to balance directories across groups) and a high number of free inodes (to be able to allocate a bunch of files); and put the directory data and inode in that group. Of course, other heuristics could be used (e.g., taking into account the number of free data blocks).

For files, FFS does two things. First, it makes sure (in the general case) to allocate the blocks of a file in the same group as its inode, preventing seeks between inode and data (as in the file system). Second, it places all files that are in the same directory in the cylinder group they are in. If a user creates four files, /a/b, /a/c, /a/d, and b/f, FFS would try to place the first three near one another (same group) and the fourth far away (in some other group).
