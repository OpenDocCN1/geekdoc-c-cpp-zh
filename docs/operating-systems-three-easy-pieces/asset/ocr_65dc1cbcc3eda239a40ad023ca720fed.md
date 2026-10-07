# LOG-STRUCTURED FILE SYSTEMS.

# 43.9 A New Problem: Garbage Collection

You may have noticed another problem with LFS: it repeatedly writes the latest version of a file (including its inode and data) to new locations on disk. This process, while efficient, implies that LFS leaves old versions of file structures scattered throughout the disk. We (rather unceriously) call these old versions garbage.

For example, let's imagine the case where we have an existing file referred to by inode $k_i$, which points to a single data block $D_0$. We now update that block, generating both a new inode and a new data block. The resulting on-layout of LFS would look something like this (note we omit the imap and other structures for simplicity; a new chunk of image would also have to be written to disk to point to the new inode):

![](bbox=[0.178, 0.373, 0.8, 0.453])

In the diagram, you can see that both the inode and data block have two versions on disk (one on the left and one on the right). The current and live (by the simple act of (logically) updating a data block, a number of new structures must be persisted by LFS, leaving old versions of said blocks on the disk.

As another example, imagine we append a block to that original k. In this case, a new version of the inode is generated, the old data block is still pointed to by the inode. Thus, it is still live and much part of the current file system:

![](bbox=[0.178, 0.626, 0.8, 0.715])

So what should we do with these older versions of inodes, data blocks, and so forth? Could we keep those old versions around and allow users to restore old file versions (for example, if they accidentally overwrite or delete a file, it could be quite nice to do so); such a file system is known as a *versioning file system* because it keeps track of the different versions of a file.

However, LFS instead keeps only the latest live version of a file; thus (in the background), LFS must periodically free these old dead versions of file data, inodes, and other structures, *clean* them; cleaning should

© 2008–19, ARPACI-DUSAU

THREE EASY PIECES