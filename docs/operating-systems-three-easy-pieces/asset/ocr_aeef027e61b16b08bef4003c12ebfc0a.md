582

LOG-STRUCTURED FILE SYSTEMS

thus make blocks on disk free again for use in subsequent writes. Note that the process of cleaning is a form of garbage collection, a technique that arises in programming languages that automatically free unused memory for programs.

Earlier we discussed segments as important as they are the mechanism that enables large writes to disk in LFS. As it turns out, they are also quite integral to effective cleaning. Imagine what would happen if the LFS cleaner simply went through and single data blocks, nodes, etc., during cleaning. The result: a file system with number of holes mixed between old segments. Performance would drop considerably, as LFS would not be able to find a contiguous region to write sequentially and with high performance.

Instead, the LFS cleans on a segment-segment basis, thus clearing up chunks of space for subsequent writing. The basic process works as follows: Periodically, the LFS reads a number of old (partially-filled) segments, determines which blocks are live within these segments, and writes a new set of segments with the live blocks within them, freeing the old ones for writing. Specifically, we expect the cleaner to read into M existing segments, pack their content into N segments (where N < M), and then write the N segments to disk in new locations. The old M segments are freed and can be used by the file system for subsequent writes.

We are now left with two problems, however. The first is mechanism: how can LFS tell which blocks within a segment are live, and which are dead? The second is policy: often should the cleaner run, and which segments should it clean?

# 43.10 Determining Liveness

We address the mechanism first. Given a data block D within an disk segment S, LFS must be able to determine whether D is live. To do so, LFS adds a little extra information to each segment that describes each block. Specifically, LFS includes, for each block D, its inode (which file it belongs to) and its offset (which block of the file is). This information is recorded in a structure at the head of the segment known as the segment summary

Given this, it is straightforward to determine whether a block is live or dead. For a block located at address A, look at the segment summary and find its inode N and offset T. Next, look in the map to find N lives and read from disk (perhaps it is already in memory, which is even better). Finally, using the offset T, look in the node (or some indirect block) to see where the index thinks the Tth block of this file is on disk. If it points to disk address A, LFS can conclude that the block D is live. If it points anywhere else, LFS can conclude that D is not in use (i.e., it is dead) and thus that this version is no longer needed. Here is a pseudocode summary:

OPERATING SYSTEMS [Version 1.01]

WWW.OSTEP.ORG