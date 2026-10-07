# FILE SYSTEM IMPLEMENTATION

# ASIDE: LINKED-BASED APPROACHES

Another simpler approach in designing inodes is to use a linked list. Thus, inside an inode, instead of having multiple pointers, you just need to point to the first block of the file. To handle larger files, add another pointer at the end of that data block, and so on, and you can support large files.

As you might have guessed, linked file allocation performs poorly for some workloads; but thinking about the last block of a file, for example, or just doing random access. Thus, to make linked allocation work better, some systems will use an in-memory table of link information, instead of storing the next pointers with the data blocks themselves. The table is indexed by the address of a data block $D$; the content of an entry is simply $D$'s next pointer, the address of the next block follows $D$. A null-value could be too (indicating an end-of-file), or some other marker to indicate that a block is free. Having such a table of next pointers makes it so that a linked allocation scheme can effectively do random access, by first scanning through the (in memory) table to find the desired block, and then accessing (on disk).

Does such a sound familiar? What we have described the basic structure of what is known as the file allocation system, before NTFS [C94], is based on a simple linked-based allocation scheme. There are no differences from a standard Unix file system too; there are no inodes per se, but rather directory entries which store metadata about a file and refer directly to the first block of said file, which makes creating hard links impossible. See Brouwer [B02] for more of the in details

You might be wondering exactly directories are stored. Often, file systems treat directories as a special type of file. A directory has an inode, in the inode table (with the type field of the inode marked as “directory” instead of “regular file”). The directory has data blocks pointed by the inode (and perhaps, indirect blocks); these data blocks live in the data block region of our file system. On-disk structure remains unchanged.

We should also note again that this simple list of directory entries is not the only way to store such information. For example, XFS [S+96] stores directories in B-tree form, making file create operations (which have to ensure that a file name has not been used before creating) faster than systems with simple lists that must be scanned in their entirety.

© 2008–19

# THREE EASY PIECES